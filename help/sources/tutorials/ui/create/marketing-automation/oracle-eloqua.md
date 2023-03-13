---
title: Crear una conexión de origen de Oracle Eloqua mediante la IU de Platform
description: Aprenda a conectar Adobe Experience Platform a Oracle Eloqua mediante la interfaz de usuario de Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 1%

---

# Crear un [!DNL Oracle Eloqua] conexión de origen mediante la IU de Platform

Este tutorial proporciona los pasos para crear una [!DNL Oracle Eloqua] conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Si ya tiene un [!DNL Oracle Eloqua] cuenta en Platform, puede omitir el resto de este documento y continuar con el tutorial sobre [creación de un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias

Para poder conectarse [!DNL Oracle Eloqua] En Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Extremo | El punto final de su [!DNL Oracle Eloqua] servidor. [!DNL Oracle Eloqua] admite varios centros de datos. Para encontrar el punto final, inicie sesión en [[!DNL Oracle Eloqua] interfaz](https://login.eloqua.com) con sus credenciales de y copie la parte de la dirección URL base de la dirección URL de redireccionamiento. El formato del patrón de URL es el siguiente `xxx.xx.eloqua.com` y deben introducirse sin `http` o `https`. |
| Nombre de usuario | El nombre de usuario de su [!DNL Oracle Eloqua] servidor. El nombre de usuario debe tener el formato `siteName + \\ + username`, donde `siteName` es el nombre de empresa que utilizó para iniciar sesión en [!DNL Oracle Eloqua] y `username` es su nombre de usuario. Por ejemplo, el nombre de usuario para iniciar sesión puede ser: `Eloqua\Andy`. **Nota**: debe utilizar una sola barra invertida (`\`)al utilizar la interfaz de usuario de porque la interfaz de usuario de Experience Platform agrega automáticamente una barra invertida adicional (`\`) al introducir un nombre de usuario. |
| Una contraseña | La contraseña correspondiente a su [!DNL Oracle Eloqua] nombre de usuario. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Eloqua], consulte la [[!DNL Oracle Eloqua] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Oracle Eloqua] a Platform.

## Conecte su [!DNL Oracle Eloqua] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Automatización de marketing] categoría, seleccionar **[!UICONTROL Oracle Eloqua]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

El **[!UICONTROL Conectar la cuenta de Oracle Eloqua]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Oracle Eloqua] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Oracle Eloqua] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Al seguir este tutorial, ha autenticado y creado una conexión de origen entre sus [!DNL Oracle Eloqua] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para llevar los datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
