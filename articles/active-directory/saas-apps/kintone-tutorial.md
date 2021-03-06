---
title: 'Tutorial: Integración de Azure Active Directory con Kintone | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Kintone.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: c3c4c4bb924ed6faf1b194273a3cf8c17b16d741
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56209887"
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Tutorial: Integración de Azure Active Directory con Kintone

En este tutorial, aprenderá a integrar Kintone con Azure Active Directory (Azure AD).

La integración de Kintone con Azure AD le proporciona las siguientes ventajas:

- En Azure AD se puede controlar quién tiene acceso a Kintone
- Puede permitir que los usuarios inicien sesión automáticamente en Kintone (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Kintone, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Kintone

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de Kintone desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-kintone-from-the-gallery"></a>Adición de Kintone desde la galería
Para configurar la integración de Kintone en Azure AD, deberá agregar Kintone desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Kintone desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Kintone**.

    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/tutorial_kintone_search.png)

1. En el panel de resultados, seleccione **Kintone** y luego haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Kintone con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Kintone para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Kintone.

Para establecer la relación de vínculo, en Kintone, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario**.

Para configurar y probar el inicio de sesión único de Azure AD con Kintone, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Kintone](#creating-a-kintone-test-user)**: para tener un homólogo de Britta Simon en Kintone que esté vinculado a la representación de Azure AD de usuario.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en Kintone.

**Para configurar el inicio de sesión único de Azure AD con Kintone, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **Kintone**, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_kintone_samlbase.png)

1. En la sección **Dominio y direcciones URL de Kintone**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_kintone_url.png)

     a. En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<companyname>.kintone.com`.

    b. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión. Póngase en contacto con el [equipo de soporte de cliente de Kintone](https://www.kintone.com/contact/) para obtener estos valores. 
 
1. En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_kintone_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de Kintone**, haga clic en **Configurar Kintone** para abrir la ventana **Configurar inicio de sesión**. Copie los valores de **Dirección URL de cierre de sesión y SAML Single Sign-On Service URL (Dirección URL del servicio de inicio de sesión único de SAML)** de la **sección Referencia rápida**.

    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_kintone_configure.png) 

1. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de **Kintone** .

1. Haga clic en **Configuración**.
   
    ![Configuración](./media/kintone-tutorial/ic785879.png "Configuración")

1. Haga clic en **Users & System Administration** (Administración del sistema y usuarios).
   
    ![Administración de usuarios y del sistema](./media/kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")

1. En **Administración del sistema \> Seguridad**, haga clic en **Inicio de sesión**.
   
    ![Inicio de sesión](./media/kintone-tutorial/ic785881.png "inicio de sesión")

1. Haga clic en **Habilitar autenticación SAML**.
   
    ![Autenticación SAML](./media/kintone-tutorial/ic785882.png "Autenticación SAML")

1. En la sección SAML Authentication (Autenticación SAML), realice los pasos siguientes:
    
    ![Autenticación SAML](./media/kintone-tutorial/ic785883.png "Autenticación SAML")
    
     a. En el cuadro de texto **Dirección URL de inicio de sesión**, pegue el valor de la **dirección URL de inicio de sesión de SAML** que ha copiado de Azure Portal.
   
    b. En el cuadro de texto **Dirección URL de cierre de sesión**, pegue el valor de **Dirección URL de cierre de sesión** que copió de Azure Portal.
    
    c. Haga clic en **Browse** (Examinar) para cargar el certificado descargado.
    
    d. Haga clic en **Save**(Guardar).

> [!TIP]
> Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.  Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior. Puede leer más aquí sobre la característica de documentación insertada: [Documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/kintone-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-kintone-test-user"></a>Creación de un usuario de prueba de Kintone

Para permitir que los usuarios de Azure AD inicien sesión en Kintone, deben aprovisionarse en Kintone.  
En el caso de Kintone, el aprovisionamiento es una tarea manual.

### <a name="to-provision-a-user-account-perform-the-following-steps"></a>Para aprovisionar una cuenta de usuario, realice estos pasos:

1. Inicie sesión en el sitio de la compañía de **Kintone** como administrador.

1. Haga clic en **Configuración**.
   
    ![Configuración](./media/kintone-tutorial/ic785879.png "Configuración")

1. Haga clic en **Users & System Administration** (Administración del sistema y usuarios).
   
    ![Administración de usuarios y del sistema](./media/kintone-tutorial/ic785880.png "Administración de usuarios y del sistema")

1. En **Administración de usuarios** haga clic en **Departamentos y usuarios**.
   
    ![Departamentos y usuarios](./media/kintone-tutorial/ic785888.png "Departamentos y usuarios")

1. Haga clic en **Nuevo usuario**.
   
    ![Nuevos usuarios](./media/kintone-tutorial/ic785889.png "Nuevos usuarios")

1. En la sección **Nuevo usuario** , lleve a cabo estos pasos:
   
    ![Nuevos usuarios](./media/kintone-tutorial/ic785890.png "Nuevos usuarios")
   
     a. Escriba un **Nombre para mostrar**, **Nombre de inicio de sesión**, **Nueva contraseña**, **Confirmar contraseña**, **Dirección de correo electrónico** y otros detalles de una cuenta válida de AAD que quiera aprovisionar en los cuadros de texto relacionados.
 
    b. Haga clic en **Save**(Guardar).

> [!NOTE]
> Puede usar cualquier otra API o herramienta de creación de cuentas de usuario de Kintone ofrecida por Kintone para aprovisionar cuentas de usuario de AAD.

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Kintone.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Kintone, siga estos pasos:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Kintone**.

    ![Configurar inicio de sesión único](./media/kintone-tutorial/tutorial_kintone_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de Kintone en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Kintone.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/kintone-tutorial/tutorial_general_01.png
[2]: ./media/kintone-tutorial/tutorial_general_02.png
[3]: ./media/kintone-tutorial/tutorial_general_03.png
[4]: ./media/kintone-tutorial/tutorial_general_04.png

[100]: ./media/kintone-tutorial/tutorial_general_100.png

[200]: ./media/kintone-tutorial/tutorial_general_200.png
[201]: ./media/kintone-tutorial/tutorial_general_201.png
[202]: ./media/kintone-tutorial/tutorial_general_202.png
[203]: ./media/kintone-tutorial/tutorial_general_203.png

