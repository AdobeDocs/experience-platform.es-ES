---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;oracle;elocuencia de oracle;eloqua
solution: Experience Platform
title: Creación de una conexión de origen Eloqua de Oracle mediante la interfaz de usuario de Platform
topic-legacy: tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Eloqua mediante la interfaz de usuario de Platform.
source-git-commit: a40a1b8fae41c495afd9cdfc3c8d68148e90f2cd
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Cree un [!DNL Oracle Eloqua] conexión de origen mediante la interfaz de usuario de Platform

Este tutorial proporciona los pasos para crear un [!DNL Oracle Eloqua] conector de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Si ya tiene una [!DNL Oracle Eloqua] en Platform, puede omitir el resto de este documento y continuar con el tutorial en [creación de un flujo de datos para traer datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL Oracle Eloqua] a Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Punto final | El punto final de su [!DNL Oracle Eloqua]. |
| Nombre de usuario | El nombre de usuario de su [!DNL Oracle Eloqua] cuenta. El nombre de usuario debe tener el formato `siteName + \\ + username`, donde `siteName` es el nombre de empresa que utilizó para iniciar sesión en [!DNL Oracle Eloqua] y `username` es su nombre de usuario. Por ejemplo, el nombre de usuario de inicio de sesión puede ser: `adobe\\emily`. |
| Contraseña | La contraseña correspondiente a su [!DNL Oracle Eloqua] nombre de usuario. |

Para obtener más información sobre las credenciales de autenticación para [!DNL Oracle Eloqua], consulte la [[!DNL Oracle Eloqua] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Oracle Eloqua] a Platform.

## Conecte su [!DNL Oracle Eloqua] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Automatización de marketing] categoría, seleccione **[!UICONTROL Oracle Eloqua]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

La variable **[!UICONTROL Conectar cuenta de Eloqua de Oracle]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Oracle Eloqua] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Oracle Eloqua] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Siguiendo este tutorial, se ha autenticado y creado una conexión de origen entre las [!DNL Oracle Eloqua] cuenta y plataforma. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para traer datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

