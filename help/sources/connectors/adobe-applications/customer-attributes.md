---
keywords: Experience Platform;inicio;temas populares;Conector de atributos del cliente
solution: Experience Platform
title: Información general sobre el conector de origen Atributos del cliente
description: Obtenga información sobre cómo conectar los atributos del cliente a Adobe Experience Platform mediante API o la interfaz de usuario
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 139d6a6632532b392fdf8d69c5c59d1fd779a6d1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# Conector de Atributos del cliente

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) en Experience Cloud permite cargar los datos empresariales capturados desde una base de datos de administración de la relación con los clientes (CRM). Puede cargar los datos en una fuente de datos de atributos del cliente de Experience Cloud y, a continuación, utilizar los datos en Adobe Analytics y Adobe Target.

El Experience Platform proporciona asistencia para la ingesta [!DNL Customer Attributes] datos de perfil en Adobe Experience Platform.

## Conjuntos de datos y esquemas

El [!DNL Customer Attributes] source crea automáticamente el conjunto de datos en el que se almacenarán los datos. Este conjunto de datos creado automáticamente es fijo y no se puede seleccionar manualmente. El origen también crea automáticamente el esquema para el conjunto de datos en función del origen de datos de entrada. Este proceso también implica la creación automática de las asignaciones necesarias entre el esquema y los datos de origen.

## Identidades

La identidad principal de un conjunto de datos se encuentra en la primera columna del archivo CSV de los datos de origen. El [!DNL Customer Attributes] source supone que la identidad siempre está asignada a [`CORE` namespace](../../../identity-service/namespaces.md), un área de nombres generada por el sistema compatible con [[!DNL Identity Service]](../../../identity-service/home.md).

No se puede seleccionar un área de nombres existente para la identidad al utilizar [!DNL Customer Attributes] origen porque [!DNL Customer Attributes] supone que la identidad principal del esquema siempre está en el mapa de identidad. [!DNL Customer Attributes] a continuación, crea la asignación del ID de origen al UUID del mapa de identidad de forma automatizada.

Para [!DNL Customer Attributes] datos para vincularlos a otros [!DNL Profile] Los conjuntos de datos de, sus datos e identidades deben poder coincidir con un ID de Experience Cloud.

Puede establecer la variable `CORE` área de nombres estableciendo el ID de Experience Cloud del visitante que utiliza [SDK web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/), o el [API del servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es).

El [!DNL Customer Attributes] el archivo no rellena más ninguna otra relación de identidad. Por ejemplo, si [!DNL Customer Attributes] el conjunto de datos de origen contiene un **Correo electrónico** y una **ID de fidelización** , estos campos deben etiquetarse como campos de identidad en el esquema para procesarse en [!DNL Identity Service].

Consulte el tutorial sobre [creación de un [!DNL Customer Attributes] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obtener más información.
