---
title: 'Tutorial: Integración de Azure Active Directory con HR2day by Merces | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y HR2day by Merces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: e932fd59fb888d73fb2ad9aee3f440b4aca3e662
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56180580"
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Tutorial: Integración de Azure Active Directory con HR2day by Merces

En este tutorial, obtendrá información sobre cómo integrar HR2day by Merces con Azure Active Directory (Azure AD).

La integración de HR2day by Merces con Azure AD proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a HR2day by Merces.
- Puede permitir que los usuarios inicien sesión automáticamente en HR2day by Merces con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: Azure Portal.

Para más información sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con HR2day by Merces, necesita los siguientes elementos:

- Una suscripción de Azure AD.
- Una suscripción habilitada para el inicio de sesión único en HR2day by Merces.

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Puede obtener [un versión de evaluación gratuita de un mes de Azure AD](https://azure.microsoft.com/pricing/free-trial/) si aún no la tiene.  

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. La escenario descrito aquí consta de dos bloques de creación principales:

1. Agregación de HR2day by Merces desde la galería.
1. Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-hr2day-by-merces-from-the-gallery"></a>Agregación de HR2day by Merces desde la galería
Para configurar la integración de HR2day by Merces en Azure AD, debe agregar HR2day by Merces desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar HR2day by Merces desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de [Azure Portal](https://portal.azure.com), seleccione el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, seleccione el botón **Nueva aplicación** en la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro Buscar, escriba **HR2day by Merces**.

    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/tutorial_hr2daybymerces_search.png)

1. En el panel de resultados, seleccione **HR2day by Merces** y haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, se configura y se prueba el inicio de sesión único de Azure AD con HR2day by Merces con un usuario de prueba llamado "Britta Simon."

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de HR2day by Merces para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de HR2day by Merces.

Para establecer la relación de vínculo, en HR2day by Merces, asigne el valor de **nombre de usuario** de Azure AD como valor de **Nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con HR2day by Merces, es preciso completar los siguientes bloques de creación:

1. Configuración del inicio de sesión único de Azure AD: Permita que los usuarios usen esta característica.
1. Creación de un usuario de prueba de Azure AD: Pruebe el inicio de sesión único de Azure AD con la usuaria Britta Simon.
1. Creación de un usuario de prueba de HR2day by Merces: Cree una homóloga de Britta Simon en HR2day by Merces que esté vinculada a la representación del usuario en Azure AD.
1. Asignación del usuario de prueba de Azure AD: Permita que Britta Simon use un inicio de sesión único de Azure AD.
1. Prueba de inicio de sesión único: Verifique que la configuración funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación HR2day by Merces.

**Para configurar el inicio de sesión único de Azure AD con HR2day by Merces, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **HR2day by Merces**, seleccione **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

1. En la sección **Dominio y direcciones URL de HR2day by Merces**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2daybymerces_url.png)

     a. En el cuadro de texto **Dirección URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<tenantname>.force.com/<instancename>`.

    b. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL de inicio de sesión y el identificador reales. Póngase en contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) para obtener estos valores. 
 


1. En la sección **Certificado de firma de SAML**, seleccione **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

1. Esta sección describe cómo se habilita la autenticación de usuarios en HR2day by Merces con sus cuentas de Azure AD. Se realiza utilizando la federación basada en el protocolo SAML.

    La aplicación HR2day by Merces espera las aserciones SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados al token SAML. La siguiente captura de pantalla le muestra un ejemplo de esto. 

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Antes de configurar la aserción SAML, debe ponerse en contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) y solicitar el valor del atributo de identificador único del inquilino. Necesita este valor para completar los pasos descritos en la sección siguiente. 

1. En el cuadro de diálogo **Inicio de sesión único**, en la sección **Atributos de usuario**, configure el atributo token SAML como muestra la imagen siguiente. A continuación, siga estos pasos.
    
      | Nombre del atributo    |   Valor de atributo |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | `join([mail],"102938475Z","@"` |
    
       a. Seleccione **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_attribute_05.png)

    b. En el cuadro de texto **Nombre**, escriba **ATTR_LOGINCLAIM**.

    c. En la lista **Valor**, seleccione **Join()**.

    d. En la lista **Cadena1**, seleccione **user.mail**.

    e. Para **Cadena2**, escriba el identificador único proporcionado por el equipo de HR2day.

    f. En el cuadro de texto **Separador**, escriba **\@**.
    
    g. Seleccione **Aceptar**.

1. Seleccione el botón **Guardar**.

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de HR2day by Merces**, seleccione **Configurar HR2day by Merces** para abrir la ventana **Configurar inicio de sesión**. Copie la **Dirección URL de cierre de sesión**, el **Identificador de entidad de SAML** y la **Dirección URL del servicio de inicio de sesión único de SAML** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

1. Para configurar el SSO para la aplicación, póngase en contacto con el [equipo de soporte técnico de HR2day by Merces](mailTo:servicedesk@merces.nl). Adjunte el archivo de **Certificado (Base64)** descargado a su correo electrónico. Además, proporcione la **dirección URL de cierre de sesión**, el **identificador de entidad de SAML** y la **dirección URL del servicio de inicio de sesión único de SAML** para que puedan configurar la integración del inicio de sesión único.

    > [!NOTE]
    >Indique al equipo de Merces que esta integración necesita que el id. de entidad se establezca con el patrón **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.  Después de agregar esta aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, seleccione la pestaña **Inicio de sesión único**. A continuación, consulte la documentación insertada en la sección **Configuración** en la parte inferior. Puede leer más sobre la característica de documentación insertada en el artículo sobre la [documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, seleccione el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, seleccione **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/create_aaduser_02.png) 

1. En la parte superior del cuadro de diálogo, seleccione **Agregar** para abrir el cuadro de diálogo **Usuario**.
 
    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/create_aaduser_03.png) 

1. En el cuadro de diálogo **Usuario**, realice los pasos siguientes:
 
    ![Creación de un usuario de prueba de Azure AD](./media/hr2day-tutorial/create_aaduser_04.png) 

     a. En el cuadro **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote la contraseña.

    d. Seleccione **Crear**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Creación de un usuario de prueba de HR2day by Merces

El objetivo de esta sección es crear una usuaria de prueba llamado Britta Simon en HR2day by Merces. Trabaje con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl) para agregar los usuarios en la cuenta de HR2day. 

> [!NOTE]
> Si necesita crear manualmente un usuario, es preciso que se ponga contacto con el [equipo de soporte técnico de HR2day by Merces](mailto:servicedesk@merces.nl).

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a HR2day by Merces.

![Asignar usuario][200] 

**Para asignar a Britta Simon a HR2day by Merces, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, vaya a la vista de directorio y vaya a **Aplicaciones empresariales**. A continuación, seleccione **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **HR2day by Merces**.

    ![Configurar inicio de sesión único](./media/hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

1. En el menú de la izquierda, seleccione **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Seleccione el botón **Agregar**. Después, en el cuadro de diálogo **Agregar asignación**, seleccione **Usuarios y grupos**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon**.

1. Haga clic en el botón **Seleccionar**.

1. En el cuadro de diálogo **Agregar asignación**, seleccione **Asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.  

Al seleccionar el icono de HR2day by Merces en el panel de acceso, iniciará sesión automáticamente en la aplicación HR2day by Merces.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre la integración de aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/hr2day-tutorial/tutorial_general_01.png
[2]: ./media/hr2day-tutorial/tutorial_general_02.png
[3]: ./media/hr2day-tutorial/tutorial_general_03.png
[4]: ./media/hr2day-tutorial/tutorial_general_04.png

[100]: ./media/hr2day-tutorial/tutorial_general_100.png

[200]: ./media/hr2day-tutorial/tutorial_general_200.png
[201]: ./media/hr2day-tutorial/tutorial_general_201.png
[202]: ./media/hr2day-tutorial/tutorial_general_202.png
[203]: ./media/hr2day-tutorial/tutorial_general_203.png

