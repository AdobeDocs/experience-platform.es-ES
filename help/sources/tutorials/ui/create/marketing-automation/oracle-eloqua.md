---
title: Crear una conexión de origen de Oracle Eloqua mediante la IU de Platform
description: Aprenda a conectar Adobe Experience Platform a Oracle Eloqua mediante la interfaz de usuario de Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Oracle Eloqua] mediante la interfaz de usuario de Platform

>[!WARNING]
>
>El origen [!DNL Oracle Eloqua] quedará obsoleto a finales de junio de 2025.

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL Oracle Eloqua] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene una cuenta de [!DNL Oracle Eloqua] autenticada en Platform, puede omitir el resto de este documento y continuar con el tutorial sobre [creación de un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para conectar [!DNL Oracle Eloqua] a Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Punto de conexión | Extremo del servidor [!DNL Oracle Eloqua]. [!DNL Oracle Eloqua] admite varios centros de datos. Para encontrar su punto de conexión, inicie sesión en la [[!DNL Oracle Eloqua] interfaz](https://login.eloqua.com) con sus credenciales y copie la parte de la dirección URL base de la dirección URL de redireccionamiento. El formato del patrón de la dirección URL es `xxx.xx.eloqua.com` y se debe especificar sin `http` o `https`. |
| Nombre de usuario | El nombre de usuario de su servidor [!DNL Oracle Eloqua]. El nombre de usuario debe tener el formato `siteName + \\ + username`, donde `siteName` es el nombre de empresa que usó para iniciar sesión en [!DNL Oracle Eloqua] y `username` es su nombre de usuario. Por ejemplo, su nombre de usuario de inicio de sesión puede ser: `Eloqua\Andy`. **Nota**: debe usar una sola barra invertida (`\`) al usar la interfaz de usuario porque la interfaz de usuario del Experience Platform agrega automáticamente una barra invertida adicional (`\`) al escribir un nombre de usuario. |
| Contraseña | La contraseña correspondiente a su nombre de usuario [!DNL Oracle Eloqua]. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Eloqua], consulte la [[!DNL Oracle Eloqua] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Oracle Eloqua] a Platform.

## Conectar su cuenta de [!DNL Oracle Eloqua]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Automatización de marketing], seleccione **[!UICONTROL Oracle Eloqua]** y, a continuación, seleccione **[!UICONTROL Agregar datos]**.

![catálogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

Aparecerá la página **[!UICONTROL Conectar cuenta Eloqua de Oracle]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la cuenta de [!DNL Oracle Eloqua] con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nueva cuenta

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores apropiados para las credenciales de [!DNL Oracle Eloqua]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Al seguir este tutorial, se ha autenticado y creado una conexión de origen entre su cuenta de [!DNL Oracle Eloqua] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing a la plataforma](../../dataflow/marketing-automation.md).
