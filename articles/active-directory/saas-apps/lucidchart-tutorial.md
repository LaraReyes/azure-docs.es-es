---
title: 'Tutorial: Integración de Azure Active Directory con Lucidchart | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Lucidchart.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 1068d364-11f3-43b5-bd6d-26f00ecd5baa
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26b9fc0fa194b9e2be97eb3bb8471b61e7fb3b8f
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56202764"
---
# <a name="tutorial-azure-active-directory-integration-with-lucidchart"></a>Tutorial: Integración de Azure Active Directory con Lucidchart

En este tutorial, aprenderá a integrar Lucidchart con Azure Active Directory (Azure AD).

La integración de Lucidchart con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Lucidchart.
- Puede permitir que los usuarios inicien sesión automáticamente en Lucidchart (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Lucidchart, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en Lucidchart

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de Lucidchart desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-lucidchart-from-the-gallery"></a>Adición de Lucidchart desde la galería
Para configurar la integración de Lucidchart en Azure AD, es preciso agregar Lucidchart desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Lucidchart desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Lucidchart**.

    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/tutorial_lucidchart_search.png)

1. En el panel de resultados, seleccione **Lucidchart** y luego haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/tutorial_lucidchart_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Lucidchart con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Lucidchart para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Lucidchart.

Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de Azure AD como valor de **nombre de usuario** de Lucidchart.

Para configurar y probar el inicio de sesión único de Azure AD con Lucidchart, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Lucidchart](#creating-a-lucidchart-test-user)**: el objetivo es tener un homólogo de Britta Simon en Lucidchart que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y lo configurará en la aplicación Lucidchart.

**Para configurar el inicio de sesión único de Azure AD con Lucidchar, realice los pasos siguientes:**

1. En la página de integración de la aplicación **Lucidchart** de Azure Portal, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/lucidchart-tutorial/tutorial_lucidchart_samlbase.png)

1. En la sección **Dominio y direcciones URL de Lucidchart**, lleve a cabo los pasos siguientes:

    ![Configurar inicio de sesión único](./media/lucidchart-tutorial/tutorial_lucidchart_url.png)

    En el cuadro de texto **URL de inicio de sesión**, escriba una URL como: `https://chart2.office.lucidchart.com/saml/sso/azure`

1. En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.

    ![Configurar inicio de sesión único](./media/lucidchart-tutorial/tutorial_lucidchart_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/lucidchart-tutorial/tutorial_general_400.png)

1. En otra ventana del explorador web, inicie sesión como administrador en el sitio de la compañía de Lucidchart.

1. En el menú de la parte superior, haga clic en **Equipo**.
   
    ![Equipo](./media/lucidchart-tutorial/ic791190.png "Equipo")

1. Haga clic en **Applications \> (Aplicaciones) Manage SAML** (Administrar SAML).
   
    ![Administrar SAML](./media/lucidchart-tutorial/ic791191.png "Administrar SAML")

1. En la página de diálogo **Configuración de la autenticación SAML** , realice los pasos siguientes:
   
     a. Seleccione **Habilitar autenticación SAML** y, después, haga clic en **Opcional**.

    ![Configuración de la autenticación SAML](./media/lucidchart-tutorial/ic791192.png "Configuración de la autenticación SAML")
 
    b. En el cuadro de texto **Dominio**, escriba el dominio y, después, haga clic en **Cambiar certificado**.

    ![Cambiar certificado](./media/lucidchart-tutorial/ic791193.png "Cambiar certificado")
 
    c. Abra el archivo de metadatos descargado, copie el contenido y luego péguelo en el cuadro de texto **Cargar metadatos** .

    ![Cargar metadatos](./media/lucidchart-tutorial/ic791194.png "Cargar metadatos")
 
    d. Seleccione **Automatically Add new users to the team** (Agregar nuevo usuario al equipo automáticamente) y, después, haga clic en **Save changes** (Guardar los cambios).

    ![Guardar cambios](./media/lucidchart-tutorial/ic791195.png "Guardar cambios")

> [!TIP]
> Ahora puede leer una versión resumida de estas instrucciones dentro de [Azure Portal](https://portal.azure.com) mientras configura la aplicación.  Después de agregar esta aplicación desde la sección **Active Directory > Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y acceda a la documentación insertada a través de la sección **Configuración** de la parte inferior. Puede leer más aquí sobre la característica de documentación insertada: [Documentación insertada de Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/lucidchart-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-lucidchart-test-user"></a>Creación de un usuario de prueba de Lucidchart

No hay ningún elemento de acción para que configure el aprovisionamiento de usuarios para Lucidchart.  Cuando un usuario asignado intenta iniciar sesión en Lucidchart desde el Panel de acceso, Lucidchart comprueba si el usuario existe.  

Si no hay cuentas de usuario disponibles, Lucidchart crea una automáticamente.

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para que use el inicio de sesión único de Azure concediéndole acceso a Lucidchart.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Lucidchart, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Lucidchart**.

    ![Configurar inicio de sesión único](./media/lucidchart-tutorial/tutorial_lucidchart_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de Lucidchart en el Panel de acceso, debería iniciar sesión automáticamente en su aplicación Lucidchart.
Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lucidchart-tutorial/tutorial_general_01.png
[2]: ./media/lucidchart-tutorial/tutorial_general_02.png
[3]: ./media/lucidchart-tutorial/tutorial_general_03.png
[4]: ./media/lucidchart-tutorial/tutorial_general_04.png

[100]: ./media/lucidchart-tutorial/tutorial_general_100.png

[200]: ./media/lucidchart-tutorial/tutorial_general_200.png
[201]: ./media/lucidchart-tutorial/tutorial_general_201.png
[202]: ./media/lucidchart-tutorial/tutorial_general_202.png
[203]: ./media/lucidchart-tutorial/tutorial_general_203.png

