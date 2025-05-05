---
keywords: Experience Platform;inicio;temas populares;Conector de atributos del cliente
solution: Experience Platform
title: Información general sobre el conector Source de Atributos del cliente
description: Obtenga información sobre cómo conectar los atributos del cliente a Adobe Experience Platform mediante API o la interfaz de usuario
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 7%

---

# Conector de Atributos del cliente

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=es) en Experience Cloud le permite cargar los datos empresariales capturados desde una base de datos de administración de la relación con los clientes (CRM). Puede cargar los datos en una fuente de datos de atributos del cliente de Experience Cloud y, a continuación, utilizar los datos en Adobe Analytics y Adobe Target.

Experience Platform proporciona soporte para la ingesta de datos de perfil [!DNL Customer Attributes] en Adobe Experience Platform.

## Conjuntos de datos y esquemas

El origen [!DNL Customer Attributes] crea automáticamente el conjunto de datos en el que se almacenarán los datos. Este conjunto de datos creado automáticamente es fijo y no se puede seleccionar manualmente. El origen también crea automáticamente el esquema para el conjunto de datos en función del origen de datos de entrada. Este proceso también implica la creación automática de las asignaciones necesarias entre el esquema y los datos de origen.

## Identidades

La identidad principal de un conjunto de datos se encuentra en la primera columna del archivo CSV de los datos de origen. El origen [!DNL Customer Attributes] supone que la identidad siempre está asignada al espacio de nombres [`CORE`](../../../identity-service/features/namespaces.md), un espacio de nombres generado por el sistema que es compatible con [[!DNL Identity Service]](../../../identity-service/home.md).

No puede seleccionar un área de nombres existente para la identidad al usar el origen [!DNL Customer Attributes] porque [!DNL Customer Attributes] supone que la identidad principal del esquema siempre está en el mapa de identidad. [!DNL Customer Attributes] crea a continuación la asignación del ID de origen al UUID del mapa de identidad de forma automatizada.

Para que los datos de [!DNL Customer Attributes] se vinculen a otros conjuntos de datos de [!DNL Profile], sus datos e identidades deben poder coincidir con un Experience Cloud ID.

Puede establecer el área de nombres `CORE` estableciendo el Experience Cloud ID para el visitante mediante [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) o la [API del servicio de Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es).

El archivo [!DNL Customer Attributes] no rellena más ninguna otra relación de identidad. Por ejemplo, si un conjunto de datos de origen de [!DNL Customer Attributes] contiene un campo de **Correo electrónico** y **ID de fidelidad**, esos campos deben etiquetarse como campos de identidad en el esquema para que se procesen en [!DNL Identity Service].

Consulte el tutorial sobre [creación de una conexión de origen [!DNL Customer Attributes] en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obtener más información.
