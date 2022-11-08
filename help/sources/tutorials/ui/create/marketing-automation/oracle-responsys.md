---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;oracle;
title: (Beta) Creación de una conexión de origen de Responsys de Oracle mediante la interfaz de usuario de Platform
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Responsys de Oracle mediante la interfaz de usuario de Platform.
source-git-commit: ff3cac5f18ea49b93b3d76e4cd8fb0d597d02be4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) Cree un [!DNL Oracle Responsys] conexión de origen mediante la interfaz de usuario de Platform

>[!NOTE]
>
>La variable [!DNL Oracle Responsys] el origen está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Este tutorial le proporciona los pasos para crear un [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) conexión de origen mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Si ya tiene una [!DNL Oracle Responsys] en Platform, puede omitir el resto de este documento y continuar con el tutorial en [creación de un flujo de datos para traer datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).

### Recopilar las credenciales necesarias

Para conectarse [!DNL Oracle Responsys] a Platform, debe proporcionar valores para las siguientes propiedades de autenticación:

| Credencial | Descripción |
| --- | --- |
| Punto final | La dirección URL de extremo de autenticación REST de su [!DNL Oracle Responsys] instancia. |
| ID del cliente | El ID de cliente de su [!DNL Oracle Responsys] instancia. |
| Secreto de cliente | El secreto de cliente de su [!DNL Oracle Responsys] instancia. |

Para obtener más información sobre las credenciales de autenticación para [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Oracle Responsys] a Platform.

## Conecte su [!DNL Oracle Responsys] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Automatización de marketing] categoría, seleccione **[!UICONTROL Responsys de oracle]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes de Adobe Experience Platform con la fuente de Oracle Responsys resaltada.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

La variable **[!UICONTROL Conectar cuenta de Responsys de Oracle]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Oracle Responsys] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![La pantalla de autenticación de cuenta existente para Responsys de Oracle.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nueva cuenta

Para crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Oracle Responsys] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![La nueva pantalla de autenticación de cuenta para Responsys de Oracle.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Pasos siguientes

Siguiendo este tutorial, se ha autenticado y creado una conexión de origen entre las [!DNL Oracle Responsys] cuenta y plataforma. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para traer datos de automatización de marketing a Platform](../../dataflow/marketing-automation.md).
