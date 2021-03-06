---
title: Uso de la herramienta de validación de Azure Stack | Microsoft Docs
description: Recopilación de archivos de registro de diagnósticos en Azure Stack
services: azure-stack
author: jeffgilb
manager: femila
cloud: azure-stack
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 12/03/2018
ms.author: jeffgilb
ms.reviewer: adshar
ms.lastreviewed: 12/03/2018
ms.openlocfilehash: 82a691c0e0b6280a168605d56ee628d81f10823f
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/30/2019
ms.locfileid: "55245657"
---
# <a name="validate-azure-stack-system-state"></a>Validación del estado del sistema de Azure Stack

*Se aplica a: sistemas integrados de Azure Stack y Kit de desarrollo de Azure Stack*

Como operador de Azure Stack, es esencial tener la capacidad de saber a petición sobre el mantenimiento y el estado del sistema. La herramienta de validación de Azure Stack (**Test-AzureStack**) es un cmdlet de PowerShell que le permite ejecutar una serie de pruebas en el sistema para identificar errores, si los hubiera. Cuando se ponga en contacto con los Servicios de atención al cliente y soporte técnico de Microsoft (CSS) con un problema, normalmente se le pedirá que ejecute esta herramienta a través del [punto de conexión con privilegios (PEP)](azure-stack-privileged-endpoint.md). Con la información sobre el mantenimiento y el estado en todo el sistema, CSS puede recopilar y analizar registros detallados, centrarse en el área donde se produjo el error y trabajar conjuntamente con usted para resolver el problema.

## <a name="running-the-validation-tool-and-accessing-results"></a>Ejecución de la herramienta de validación y acceso a los resultados

Como se indicó anteriormente, la herramienta de validación se ejecuta a través del PEP. Cada prueba devuelve un estado **PASS/FAIL** (correcto/incorrecto) en la ventana de PowerShell. Además, se crea un informe HTML detallado al que se puede tener acceso más adelante durante la [recopilación de registros](azure-stack-diagnostics.md). Este es un esquema del proceso de prueba de validación de un extremo a otro: 

1. Acceda al punto de conexión con privilegios (PEP). Ejecute los comandos siguientes para establecer una sesión de PEP:

   ```powershell
   Enter-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
   ```

   > [!TIP]
   > Para acceder al PEP en un equipo host del Kit de desarrollo de Azure Stack, use AzS-ERCS01 para - ComputerName.

2. Una vez que esté en el PEP, ejecute: 

   ```powershell
   Test-AzureStack
   ```

   Acuda a las secciones [Consideraciones sobre los parámetros](azure-stack-diagnostic-test.md#parameter-considerations) y [Ejemplos de caso de uso](azure-stack-diagnostic-test.md#use-case-examples) para más información.

3. Si cualquier informe de pruebas aparece como **FAIL**, ejecute:

   ```powershell
   Get-AzureStackLog -FilterByRole SeedRing -OutputSharePath "<path>" -OutputShareCredential $cred
   ```

   El cmdlet recopila registros generados por Test-AzureStack. Para más información sobre los registros de diagnóstico, consulte [Registros de diagnóstico de Azure Stack](azure-stack-diagnostics.md). Si las pruebas devuelven **WARN** (Advertir) no necesita recopilar registros ni ponerse en contacto con los Servicios de atención al cliente y soporte técnico de Microsoft (CSS).

4. Si el CSS le indicó que ejecutase la herramienta de validación, el representante del CSS le solicitará los registros que haya recopilado para continuar con la solución del problema.

## <a name="tests-available"></a>Pruebas disponibles

La herramienta de validación le permite ejecutar una serie de pruebas de nivel de sistema y escenarios de nube básicos que le proporcionan una recomendación sobre el estado actual y determinan los problemas en el sistema.

### <a name="cloud-infrastructure-tests"></a>Pruebas de infraestructura en la nube

Estas pruebas de bajo impacto trabajan a nivel de infraestructura y proporcionan información sobre los distintos componentes y funciones del sistema. Actualmente, las pruebas se agrupan en las siguientes categorías:

| Categoría de prueba                                        | Argumento de -Include and -Ignore |
| :--------------------------------------------------- | :-------------------------------- |
| Resumen de alertas de Azure Stack                            | AzsAlertSummary                   |
| Resumen de accesibilidad del recurso compartido de copia de seguridad de Azure Stack       | AzsBackupShareAccessibility       |
| Resumen de plano de Control de Azure Stack                    | AzsControlPlane                   |
| Resumen de Azure Stack Defender                         | AzsDefenderSummary                |
| Resumen del firmware de la infraestructura de hospedaje de Azure Stack  | AzsHostingInfraFWSummary          |
| Resumen de la infraestructura de hospedaje en la nube de Azure Stack     | AzsHostingInfraSummary            |
| Uso de la infraestructura de hospedaje en la nube de Azure Stack | AzsHostingInfraUtilization        |
| Capacidad de la infraestructura de Azure Stack                  | AzsInfraCapacity                  |
| Rendimiento de la infraestructura de Azure Stack               | AzsInfraPerformance               |
| Resumen de los roles de la infraestructura de Azure Stack              | AzsInfraRoleSummary               |
| Resumen de actualización de Azure Stack                           | AzsInfraUpdateSummary             |
| Resumen de API y del portal de Azure Stack                   | AzsPortalAPISummary               |
| Eventos de máquina virtual de la unidad de escalado de Azure Stack                     | AzsScaleUnitEvents                |
| Recursos de máquina virtual de la unidad de escalado de Azure Stack                  | AzsScaleUnitResources             |
| Resumen de validación de SDN de Azure Stack                   | AzsSDNValidation                  |
| Resumen de roles de Azure Stack Service Fabric              | AzsSFRoleSummary                  |
| Resumen del BMC de Azure Stack                              | AzsStampBMCSummary                |
| Resumen de los servicios de almacenamiento de Azure Stack                 | AzsStorageSvcsSummary             |
| Resumen del almacén de SQL de Azure Stack                        | AzsStoreSummary                   |
| Resumen de la selección de máquina virtual de Azure Stack                     | AzsVmPlacement                    |

### <a name="cloud-scenario-tests"></a>Pruebas de escenario de nube

Además de la infraestructura de pruebas anteriores, también tiene la capacidad de ejecutar pruebas de escenario de nube para comprobar la funcionalidad en todos los componentes de la infraestructura. Las credenciales de administrador de la nube son necesarias para ejecutar estas pruebas, ya que implican la implementación de recursos. 
    > [!NOTE]
    >
    > Currently you cannot run cloud scenario tests using Active Directory Federated Services (AD FS) credentials. 

Los siguientes escenarios de nube han sido probados por la herramienta de validación:
- Creación de grupos de recursos   
- Creación de planes              
- Creación de ofertas            
- Creación de cuentas de almacenamiento   
- Creación de máquinas virtuales 
- Operación de almacenamiento de blobs   
- Operación de almacenamiento en cola  
- Operación de almacenamiento en tabla  

## <a name="parameter-considerations"></a>Consideraciones sobre los parámetros

- El parámetro **List** puede usarse para mostrar todas las categorías de prueba disponibles.

- Los parámetros **Include** e **Ignore** pueden usarse para incluir o excluir las categorías de pruebas. Consulte la sección [Pruebas disponibles](azure-stack-diagnostic-test.md#tests-available) para más información sobre la forma abreviada para usar con estos argumentos.

  ```powershell
  Test-AzureStack -Include AzsSFRoleSummary, AzsInfraCapacity
  ```

  ```powershell
  Test-AzureStack -Ignore AzsInfraPerformance
  ```

- Se implementa una máquina virtual de inquilino como parte de una de las pruebas de escenario de nube. Puede usar **DoNotDeployTenantVm** para deshabilitar esta implementación. 

- Tendrá que agregar el parámetro **ServiceAdminCredential** para ejecutar las pruebas de escenario de nube, tal y como se describe en la sección [Ejemplos de caso de uso](azure-stack-diagnostic-test.md#use-case-examples).

- **BackupSharePath** y **BackupShareCredential** se utilizan cuando se prueba la configuración de copia de seguridad de la infraestructura, tal y como se muestra en la sección [Ejemplos de caso de uso](azure-stack-diagnostic-test.md#use-case-examples).

- La herramienta de validación también admite parámetros comunes de PowerShell: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable y OutVariable. Para más información, consulte [About Common Parameters](https://go.microsoft.com/fwlink/?LinkID=113216) (Acerca de parámetros habituales).  

## <a name="use-case-examples"></a>Ejemplos de caso de uso

### <a name="run-validation-without-cloud-scenarios"></a>Ejecución de la validación sin escenarios de nube

Ejecute la herramienta de validación sin el parámetro **ServiceAdminCredential** para omitir la ejecución de las pruebas de escenario de nube: 

```powershell
New-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred
Test-AzureStack
```

### <a name="run-validation-with-cloud-scenarios"></a>Ejecución de la validación con escenarios de nube

Al proporcionar la herramienta de validación con el parámetro **ServiceAdminCredentials** se ejecutan las pruebas de escenario de nube de forma predeterminada: 

```powershell
Enter-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
Test-AzureStack -ServiceAdminCredential "<Cloud administrator user name>" 
```

Si desea ejecutar SOLO escenarios de nube sin ejecutar el resto de las pruebas, puede usar el parámetro **Include** para hacerlo: 

```powershell
Enter-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
Test-AzureStack -ServiceAdminCredential "<Cloud administrator user name>" -Include AzsScenarios   
```

El nombre de usuario del administrador de la nube tiene que escribirse en formato UPN: serviceadmin@contoso.onmicrosoft.com (Azure AD). Cuando se le solicite, escriba la contraseña en la cuenta de administrador en la nube.

### <a name="run-validation-tool-to-test-system-readiness-before-installing-update-or-hotfix"></a>Ejecución de la herramienta de validación para probar la preparación del sistema antes de instalar una actualización o una revisión

Antes de iniciar la instalación de una actualización o una revisión, debe ejecutar la herramienta de validación para comprobar el estado de la instancia de Azure Stack:

```powershell
New-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
Test-AzureStack -Include AzsControlPlane, AzsDefenderSummary, AzsHostingInfraSummary, AzsHostingInfraUtilization, AzsInfraCapacity, AzsInfraRoleSummary, AzsPortalAPISummary, AzsSFRoleSummary, AzsStampBMCSummary
```

### <a name="run-validation-tool-to-test-infrastructure-backup-settings"></a>Ejecución de la herramienta de validación para probar la configuración de copia de seguridad de la infraestructura

*Antes* de configurar la copia de seguridad de la infraestructura, puede probar la ruta de acceso y las credenciales del recurso compartido de copia de seguridad mediante la prueba **AzsBackupShareAccessibility**: 

  ```powershell
  New-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
  Test-AzureStack -Include AzsBackupShareAccessibility -BackupSharePath "\\<fileserver>\<fileshare>" -BackupShareCredential <PSCredentials-for-backup-share>
  ```

*Después* de configurar la copia de seguridad, puede ejecutar **AzsBackupShareAccessibility** para asegurarse de que el recurso compartido sea accesible desde ERCS:

  ```powershell
  Enter-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
  Test-AzureStack -Include AzsBackupShareAccessibility
  ```

Para probar las nuevas credenciales con el recurso compartido de la copia de seguridad configurada, ejecute: 

  ```powershell
  Enter-PSSession -ComputerName "<ERCS VM-name/IP address>" -ConfigurationName PrivilegedEndpoint -Credential $localcred 
  Test-AzureStack -Include AzsBackupShareAccessibility -BackupShareCredential "<PSCredential for backup share>"
  ```



## <a name="next-steps"></a>Pasos siguientes

Para más información acerca de las herramientas de diagnóstico de Azure Stack y el registro de problemas, consulte [Herramientas de diagnóstico de Azure Stack](azure-stack-diagnostics.md).

Para más información acerca de la solución de problemas, consulte [Solución de problemas de Microsoft Azure Stack](azure-stack-troubleshooting.md).