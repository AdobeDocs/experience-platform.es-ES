---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Importación y uso de audiencias externas
description: Siga este tutorial para aprender a utilizar audiencias externas con Adobe Experience Platform.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# Importación y uso de audiencias externas

Adobe Experience Platform admite la posibilidad de importar audiencias externas, que posteriormente pueden utilizarse como componentes para una nueva definición de segmento. Este documento proporciona un tutorial para configurar un Experience Platform para importar y utilizar audiencias externas.

## Primeros pasos

- [Servicio](../home.md) de segmentación: Permite generar segmentos de audiencia a partir de datos del perfil del cliente en tiempo real.
- [Perfil](../../profile/home.md) del cliente en tiempo real: Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.
- [Conjuntos de datos](../../catalog/datasets/overview.md): La construcción de almacenamiento y administración para la persistencia de datos en el Experience Platform.
- [ingesta](../../ingestion/streaming-ingestion/overview.md) de transmisión: El modo en que el Experience Platform ingesta y almacena datos de dispositivos del lado del cliente y del servidor en tiempo real.

## Creación de un área de nombres de identidad para la audiencia externa

El primer paso para utilizar audiencias externas es crear un área de nombres de identidad. Las áreas de nombres de identidad permiten a Platform asociar desde dónde se origina un segmento.

Para crear un área de nombres de identidad, siga las instrucciones de la [guía del área de nombres de identidad](../../identity-service/namespaces.md#manage-namespaces). Al crear el área de nombres de identidad, agregue los detalles de origen al área de nombres de identidad y marque su [!UICONTROL Type] como **[!UICONTROL Non-people identifier]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Creación de un esquema para los metadatos del segmento

Después de crear un área de nombres de identidad, debe crear un nuevo esquema para el segmento que va a crear.

Para empezar a componer un esquema, seleccione primero **[!UICONTROL Schemas]** en la barra de navegación izquierda, seguido de **[!UICONTROL Create schema]** en la esquina superior derecha del espacio de trabajo Esquemas. Desde aquí, seleccione **[!UICONTROL Browse]** para ver una selección completa de los tipos de esquema disponibles.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Dado que está creando una definición de segmento, que es una clase predefinida, seleccione **[!UICONTROL Use existing class]**. Ahora, seleccione la clase **[!UICONTROL Segment definition]**, seguida de **[!UICONTROL Assign class]**.

![](../images/tutorials/external-audiences/assign-class.png)

Ahora que se ha creado el esquema, debe especificar qué campo contendrá el ID de segmento. Este campo debe marcarse como identidad principal y asignarse a los espacios de nombres creados anteriormente.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Después de marcar el campo `_id` como identidad principal, seleccione el título del esquema, seguido del botón denominado **[!UICONTROL Profile]**. Seleccione **[!UICONTROL Enable]** para habilitar el esquema para [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Ahora, este esquema está habilitado para Perfil, con la identificación principal asignada al espacio de nombres de identidad no personal que ha creado. Como resultado, esto significa que los metadatos de segmento importados a Platform mediante este esquema se incorporarán en Perfil sin combinarse con otros datos de Perfil relacionados con las personas.

## Creación de un conjunto de datos para el esquema

Después de configurar el esquema, deberá crear un conjunto de datos para los metadatos del segmento.

Para crear un conjunto de datos, siga las instrucciones de la [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#create). Debe seguir la opción **[!UICONTROL Create dataset from schema]** , utilizando el esquema creado anteriormente.

![](../images/tutorials/external-audiences/select-schema.png)

Después de crear el conjunto de datos, siga las instrucciones de la [guía del usuario del conjunto de datos](../../catalog/datasets/user-guide.md#enable-profile) para habilitar este conjunto de datos para el perfil del cliente en tiempo real.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Configuración e importación de datos de audiencia

Con el conjunto de datos habilitado, ahora se pueden enviar datos a Platform a través de la interfaz de usuario o mediante las API de Experience Platform. Para introducir estos datos en Platform, debe crear una conexión de flujo continuo.

Para crear una conexión de flujo continuo, puede seguir las instrucciones del [tutorial de API](../../sources/tutorials/api/create/streaming/http.md) o del [tutorial de interfaz de usuario](../../sources/tutorials/ui/create/streaming/http.md).

Una vez que haya creado la conexión de flujo continuo, tendrá acceso a su punto final de flujo único al que podrá enviar los datos. Para aprender a enviar datos a estos extremos, lea el [tutorial sobre transmisión de datos de registro](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Generación de segmentos con audiencias importadas

Una vez configuradas las audiencias importadas, se pueden utilizar como parte del proceso de segmentación. Para buscar audiencias externas, vaya al Generador de segmentos y seleccione la pestaña **[!UICONTROL Audiences]** en la sección **[!UICONTROL Fields]**.

![](../images/tutorials/external-audiences/external-audiences.png)

## Pasos siguientes

Ahora que puede utilizar audiencias externas en sus segmentos, puede utilizar el Generador de segmentos para crear segmentos. Para aprender a crear segmentos, lea el [tutorial sobre la creación de segmentos](./create-a-segment.md).
