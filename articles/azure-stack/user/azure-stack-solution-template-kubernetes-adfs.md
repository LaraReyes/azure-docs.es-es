---
title: Implementación de Kubernetes en Azure Stack con los Servicios de federación de Active Directory (AD FS) | Microsoft Docs
description: Obtenga información sobre cómo implementar Kubernetes en Azure Stack con los Servicios de federación de Active Directory (AD FS).
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2019
ms.author: mabrigg
ms.reviewer: waltero
ms.lastreviewed: 01/16/2019
ms.openlocfilehash: df84562c3ff95ac6fef65ea7c9911d5e12e558ef
ms.sourcegitcommit: 947b331c4d03f79adcb45f74d275ac160c4a2e83
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/05/2019
ms.locfileid: "55744970"
---
# <a name="deploy-kubernetes-to-azure-stack-using-active-directory-federated-services"></a>Implementación de Kubernetes en Azure Stack con los Servicios de federación de Active Directory

*Se aplica a: Sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

> [!Note]  
> Kubernetes en Azure Stack está en versión preliminar. El escenario sin conexión de Azure Stack no es compatible actualmente con la versión preliminar.

Puede seguir los pasos descritos en este artículo para implementar y configurar los recursos de Kubernetes. Siga estos pasos cuando los Servicios de federación de Active Directory (AD FS) sean su servicio de administración de identidad.

## <a name="prerequisites"></a>Requisitos previos 

Para empezar, asegúrese de tener los permisos adecuados y de que la instancia de Azure Stack está lista.

1. Genere un par de claves SSH pública y privada para iniciar sesión en la máquina virtual de Linux en Azure Stack. Necesita la clave pública al crear el clúster.

    Para obtener instrucciones sobre cómo generar una clave, consulte [SSH Key Generation](https://github.com/msazurestackworkloads/acs-engine/blob/master/docs/ssh.md#ssh-key-generation) (Generación de claves SSH).

1. Compruebe que tiene una suscripción válida en el portal del inquilino de Azure Stack y que tiene suficientes direcciones IP públicas disponibles para agregar nuevas aplicaciones.

    No se puede implementar el clúster en una suscripción de **administrador** de Azure Stack. Debe usar una suscripción de **Usuario**. 

1. Si no tiene un clúster de Kubernetes en Marketplace, póngase en contacto con su administrador de Azure Stack.

## <a name="create-a-service-principal"></a>Creación de una entidad de servicio

Deberá trabajar con el administrador de Azure Stack para que configure la entidad de servicio cuando se use AD FS como solución de identidad. La entidad de servicio permite que la aplicación acceda a los recursos de Azure Stack.

1. El administrador de Azure Stack le proporciona un certificado e información de la entidad de servicio. Dicha información debe verse así:

    ```Text  
        ApplicationIdentifier : S-1-5-21-1512385356-3796245103-1243299919-1356
        ClientId              : 3c87e710-9f91-420b-b009-31fa9e430145
        Thumbprint            : 30202C11BE6864437B64CE36C8D988442082A0F1
        ApplicationName       : Azurestack-MyApp-c30febe7-1311-4fd8-9077-3d869db28342
        PSComputerName        : azs-ercs01
        RunspaceId            : a78c76bb-8cae-4db4-a45a-c1420613e01b
    ```

2. Asigne un rol de colaborador en su suscripción a la nueva entidad de servicio. Para obtener instrucciones, consulte la sección sobre cómo [asignar un rol](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#assign-role-to-service-principal#assign-role-to-service-principal).

3. Cree un almacén de claves para almacenar el certificado de la implementación.

    - Necesita la siguiente información:

        | Valor | DESCRIPCIÓN |
        | ---   | ---         |
        | Azure Resource Manager Endpoint | Microsoft Azure Resource Manager es una plataforma de administración que permite a los administradores implementar, administrar y supervisar recursos de Azure. Azure Resource Manager puede controlar estas tareas como grupo, en vez de individualmente, en una sola operación.<br>El punto de conexión del Kit de desarrollo de Azure Stack (ASDK) es `https://management.local.azurestack.external/`.<br>El punto de conexión en los sistemas integrados es `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`. |
        | Id. de suscripción | El [identificador de suscripción](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview#subscriptions) es su forma de tener acceso a las ofertas de Azure Stack. |
        | Nombre de usuario | Nombre del usuario. |
        | Nombre del grupo de recursos.  | Nombre del nuevo grupo de recursos, también puede seleccionar uno existente. El nombre del recurso debe ser alfanumérico y estar en minúsculas. |
        | Nombre del almacén de claves | Nombre del almacén.<br> Patrón de expresión regular: `^[a-zA-Z0-9-]{3,24}$`. |
        | Ubicación del grupo de recursos | Ubicación del grupo de recursos. Esta es la región que elige para la instalación de Azure Stack. |

    - Abra PowerShell con un símbolo del sistema con privilegios elevados. Ejecute el siguiente script con sus valores de parámetros:

    ```PowerShell  
        $armEndpoint="<Azure Resource Manager Endpoint>"
        $subscriptionId="<Your Subscription ID>"
        $username="<your user name >"
        $resource_group_name = "<the resource group name >"
        $key_vault_name = "<keyvault name>"
        $resource_group_location="<resource group location>"
        
        # Login Azure Stack Environment
        Add-AzureRmEnvironment -ARMEndpoint $armEndpoint -Name t
        $mycreds = Get-Credential
        Login-AzureRmAccount -Credential $mycreds -Environment t -Subscription $subscriptionId
        
        # Create new Resource group and key vault
        New-AzureRmResourceGroup -Name $resource_group_name -Location $resource_group_location -Force
        
        # Note, Do not omit -EnabledForTemplateDeployment flag
        New-AzureRmKeyVault -VaultName $key_vault_name -ResourceGroupName $resource_group_name -Location $resource_group_location -EnabledForTemplateDeployment
        
        # Obtain the security identifier(SID) of the active directory user
        $adUser = Get-ADUser -Filter "Name -eq '$username'" -Credential $mycreds
        $objectSID = $adUser.SID.Value
        # Set the key vault access policy
        Set-AzureRmKeyVaultAccessPolicy -VaultName $key_vault_name -ResourceGroupName $resource_group_name -ObjectId $objectSID -BypassObjectIdValidation -PermissionsToKeys all -PermissionsToSecrets all
    ```

4. Cargue el certificado en la instancia de Key Vault.

    - Necesita la siguiente información:

        | Valor | DESCRIPCIÓN |
        | ---   | ---         |
        | Ruta de acceso del certificado | Nombre de dominio completo o ruta de acceso al certificado. |
        | Contraseña del certificado | Contraseña del certificado. |
        | Nombre del secreto | Secreto que se generó en el paso anterior. |
        | Nombre del almacén de claves | Nombre del almacén de claves creado en el paso anterior. |
        | Azure Resource Manager Endpoint | El punto de conexión del Kit de desarrollo de Azure Stack (ASDK) es `https://management.local.azurestack.external/`.<br>El punto de conexión en los sistemas integrados es `https://management.<location>.ext-<machine-name>.masd.stbtest.microsoft.com/`. |
        | Id. de suscripción | El [identificador de suscripción](https://docs.microsoft.com/azure/azure-stack/azure-stack-plan-offer-quota-overview#subscriptions) es su forma de tener acceso a las ofertas de Azure Stack. |

    - Abra PowerShell con un símbolo del sistema con privilegios elevados. Ejecute el siguiente script con sus valores de parámetros:

    ```PowerShell  
        
    # upload the pfx to key vault
    $tempPFXFilePath = "<certificate path>"
    $password = "<certificate password>"
    $keyVaultSecretName = "<secret name>"
    $keyVaultName = "<keyvault name>"
    $armEndpoint="<Azure Resource Manager Endpoint>"
    $subscriptionId="<Your Subscription ID>"
    # Login Azure Stack Environment
    Add-AzureRmEnvironment -ARMEndpoint $armEndpoint -Name t
    $mycreds = Get-Credential
    Login-AzureRmAccount -Credential $mycreds -Environment t -Subscription $subscriptionId
    
    $certContentInBytes = [io.file]::ReadAllBytes($tempPFXFilePath)
    $pfxAsBase64EncodedString = [System.Convert]::ToBase64String($certContentInBytes)
    $jsonObject = @"
    {
    "data": "$pfxAsBase64EncodedString",
    "dataType" :"pfx",
    "password": "$password"
    }
    "@
    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    $keyVaultSecret = Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret 
    ```

## <a name="deploy-kubernetes"></a>Implementación de Kubernetes

1. Abra el [portal de Azure Stack](https://portal.local.azurestack.external).

1. Seleccione **+ Crear un recurso** > **Proceso** > **Clúster de Kubernetes**. Haga clic en **Create**(Crear).

    ![Implementar plantilla de solución](media/azure-stack-solution-template-kubernetes-deploy/01_kub_market_item.png)

### <a name="1-basics"></a>1. Aspectos básicos

1. Seleccione **Aspectos básicos** en Crear un clúster de Kubernetes.

    ![Implementar plantilla de solución](media/azure-stack-solution-template-kubernetes-deploy/02_kub_config_basic.png)

1. Seleccione el identificador de **suscripción**.

1. Escriba el nombre del nuevo grupo de recursos o seleccione uno existente. El nombre del recurso debe ser alfanumérico y estar en minúsculas.

1. Seleccione la **ubicación** del grupo de recursos. Esta es la región que elige para la instalación de Azure Stack.

### <a name="2-kubernetes-cluster-settings"></a>2. Configuración de un clúster de Kubernetes

1. Seleccione **Kubernetes Cluster Settings** (Configuración de clúster de Kubernetes) en Crear un clúster de Kubernetes.

    ![Implementar plantilla de solución](media/azure-stack-solution-template-kubernetes-deploy/03_kub_config_settings-adfs.png)

1. Escriba el **nombre de usuario del administrador de la máquina virtual Linux**. Nombre de usuario de las máquinas virtuales de Linux que forman parte del clúster de Kubernetes y DVM.

1. Escriba la **clave pública SSH** utilizada para la autorización en todas las máquinas Linux creadas como parte del clúster de Kubernetes y DVM.

1. Escriba el **prefijo del DNS del perfil maestro** que es único para la región. Debe ser un nombre único para la región, como `k8s-12345`. Como procedimiento recomendado, intente elegirlo de modo que sea el mismo que el nombre del grupo de recursos.

    > [!Note]  
    > Para cada clúster, use un prefijo de DNS del perfil principal nuevo y único.

1. Seleccione la opción **Kubernetes Master Pool Profile Count** ( Recuento de perfiles del grupo maestro de Kubernetes). El recuento contiene el número de nodos en el grupo maestro. Puede haber entre 1 y 7. Este valor debe ser un número impar.

1. Seleccione **The VMSize of the Kubernetes master VMs** (VMSize de las máquinas virtuales maestras de Kubernetes).

1. Seleccione la opción **Kubernetes Node Pool Profile Count** ( Recuento de perfiles del grupo de nodos de Kubernetes). El recuento contiene el número de agentes en el clúster. 

1. Seleccione **The Storage Profile** (Perfil del almacenamiento). Puede elegir **Blob Disk** (Disco blob) o **Managed Disk** (Disco administrado). Así se especifica el tamaño de máquina virtual de las máquinas virtuales del nodo de Kubernetes. 

1. Seleccione **ADFS** como **sistema de identidad de Azure Stack** para la instalación de Azure Stack.

1. Escriba el **id. de cliente de la entidad de servicio**. El proveedor de nube de Azure Kubernetes usa este identificador. El id. de cliente identificado como identificador de la aplicación cuando el administrador de Azure Stack creó la entidad de servicio.

1. Escriba el **grupo de recursos del almacén de claves**. 

1. Escriba el **nombre del almacén de claves**.

1. Escriba el **secreto del almacén de claves**.

1. Escriba la **versión del proveedor de nube de Azure Kubernetes**. Esta es la versión para el proveedor de Kubernetes Azure. Azure Stack publica una compilación de Kubernetes personalizada para cada versión de Azure Stack.

### <a name="3-summary"></a>3. Resumen

1. Seleccione Summary (Resumen). La hoja muestra un mensaje de validación de la configuración del clúster de Kubernetes.

    ![Implementar plantilla de solución](media/azure-stack-solution-template-kubernetes-deploy/04_preview.png)

2. Revise la configuración.

3. Seleccione **Ok** (Aceptar) para implementar el clúster.

> [!TIP]  
>  Si tiene preguntas acerca de la implementación, puede publicarlas o ver si alguien ya ha respondido a las mismas preguntas en el [foro de Azure Stack](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack). 

## <a name="next-steps"></a>Pasos siguientes

[Conexión al clúster](azure-stack-solution-template-kubernetes-deploy.md#connect-to-your-cluster)