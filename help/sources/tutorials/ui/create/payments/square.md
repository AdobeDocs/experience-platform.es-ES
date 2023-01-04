---
keywords: Experience Platform;inicio;temas populares;cuadrado;cuadrado
title: Crear una conexión de origen cuadrado en la interfaz de usuario
description: Aprenda a crear una conexión de origen cuadrada mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Cree un [!DNL Square] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear un [!DNL Square] conector de origen mediante la interfaz de usuario de Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

### Recopilar las credenciales necesarias

Para acceder a su [!DNL Square] plataforma de cuenta, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| --- | --- |
| Host | La dirección URL del [!DNL Square] instancia. |
| ID del cliente | El ID de cliente asociado con su [!DNL Square] cuenta. |
| Secreto de cliente | El secreto de cliente asociado con su [!DNL Square] cuenta. |
| Token de acceso | El token de acceso se utiliza para autenticar su [!DNL Square] cuenta con autenticación OAuth 2.0. El token de acceso se puede obtener de [!DNL Square]. |
| Actualizar token | El token de actualización se utiliza para generar nuevos tokens de acceso una vez que caduca el token de acceso actual. El token de actualización se puede obtener de [!DNL Square]. |

Para obtener más información sobre estas credenciales y cómo obtenerlas, consulte la [[!DNL Square] documentación sobre OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL Square] a Platform.

## Conecte su [!DNL Square] account

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Fuentes]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Fuentes] espacio de trabajo. La variable [!UICONTROL Catálogo] muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el [!UICONTROL Pagos] categoría, seleccione **[!UICONTROL Cuadrado]** y, a continuación, seleccione **[!UICONTROL Añadir datos]**.

![catálogo](../../../../images/tutorials/create/square/catalog.png)

La variable **[!UICONTROL Conectar a cuadrado]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para usar una cuenta existente, seleccione la opción [!DNL Square] cuenta con la que desee crear un nuevo flujo de datos y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/square/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre, una descripción opcional y los valores adecuados para su [!DNL Square] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar a origen]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![new](../../../../images/tutorials/create/square/new.png)

## Pasos siguientes

Siguiendo este tutorial, se ha autenticado y creado una conexión de origen entre las [!DNL Square] cuenta y plataforma. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para introducir los datos de pagos en Platform](../../dataflow/payments.md).
