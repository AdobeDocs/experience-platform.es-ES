---
keywords: Experience Platform;inicio;temas populares;Cuadrado;cuadrado
title: Creación de una conexión de origen cuadrada en la interfaz de usuario
description: Aprenda a crear una conexión de origen cuadrado mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Crear un [!DNL Square] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL Square] conector de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

### Recopilar credenciales necesarias

Para acceder a su [!DNL Square] En la plataforma de cuenta de, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| --- | --- |
| Host | La dirección URL del [!DNL Square] ejemplo. |
| ID del cliente | El ID de cliente asociado con su [!DNL Square] cuenta. |
| Secreto de cliente | El secreto de cliente asociado con su [!DNL Square] cuenta. |
| Token de acceso | El token de acceso se utiliza para autenticar su [!DNL Square] cuenta con autenticación OAuth 2.0. El token de acceso se puede obtener de [!DNL Square]. |
| Actualizar token | El token de actualización se utiliza para generar nuevos tokens de acceso una vez que caduca el token de acceso actual. El token de actualización se puede obtener de [!DNL Square]. |

Para obtener más información sobre estas credenciales y cómo obtenerlas, consulte la [[!DNL Square] documentación de OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Square] a Platform.

## Conecte su [!DNL Square] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Pagos] categoría, seleccionar **[!UICONTROL Cuadrado]**, y luego seleccione **[!UICONTROL Añadir datos]**.

![catalogar](../../../../images/tutorials/create/square/catalog.png)

El **[!UICONTROL Conectar con Square]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para utilizar una cuenta existente, seleccione la [!DNL Square] cuenta con la que desea crear un nuevo flujo de datos y seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/square/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Square] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![nuevo](../../../../images/tutorials/create/square/new.png)

## Pasos siguientes

Al seguir este tutorial, ha autenticado y creado una conexión de origen entre sus [!DNL Square] y Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para introducir datos de pagos en Platform](../../dataflow/payments.md).
