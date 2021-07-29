---
keywords: Experience Platform;inicio;temas populares;conector de Atributos del cliente
solution: Experience Platform
title: Información general sobre el conector de origen de Atributos del cliente
topic-legacy: overview
description: Obtenga información sobre cómo conectar los Atributos del cliente a Adobe Experience Platform mediante API o la interfaz de usuario
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Conector de atributos del cliente

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) en Experience Cloud permite cargar los datos empresariales capturados desde una base de datos de administración de la relación con los clientes (CRM). Puede cargar los datos en un origen de datos de Atributos del cliente en el Experience Cloud y, a continuación, utilizar los datos en Adobe Analytics y Adobe Target.

Experience Platform proporciona asistencia para la ingesta de [!DNL Customer Attributes] datos de perfil en Adobe Experience Platform.

## Conjuntos de datos y esquemas

El origen [!DNL Customer Attributes] crea automáticamente el conjunto de datos para que los datos lleguen a su destino. Este conjunto de datos creado automáticamente es fijo y no se puede seleccionar manualmente. El origen también crea automáticamente el esquema para el conjunto de datos en función del origen de datos de entrada. Este proceso también implica la creación automática de las asignaciones necesarias entre el esquema y los datos de origen.

## Identidades

La identidad principal de un conjunto de datos se encuentra en la primera columna del archivo CSV de los datos de origen. El origen [!DNL Customer Attributes] supone que la identidad siempre se asigna al espacio de nombres [`CORE`](../../../identity-service/namespaces.md), un espacio de nombres generado por el sistema compatible con [[!DNL Identity Service]](../../../identity-service/home.md).

No se puede seleccionar un área de nombres existente para la identidad al utilizar el origen [!DNL Customer Attributes] porque [!DNL Customer Attributes] supone que la identidad principal del esquema siempre está en el mapa de identidad. [!DNL Customer Attributes] a continuación, crea la asignación del ID de origen al UUID de mapa de identidad de forma automatizada.

Para que los datos [!DNL Customer Attributes] se vinculen a otros [!DNL Profile] conjuntos de datos, sus datos e identidades deben poder coincidir con un ID de Experience Cloud.

Puede establecer el espacio de nombres `CORE` estableciendo el ID de Experience Cloud del visitante mediante [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity) o la [API del servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=en).

El archivo [!DNL Customer Attributes] no rellena ninguna otra relación de identidad. Por ejemplo, si un conjunto de datos de origen [!DNL Customer Attributes] contiene un campo **Email** y un campo **Loyalty ID**, esos campos deben etiquetarse como campos de identidad en el esquema para procesarse en [!DNL Identity Service].

Consulte el tutorial sobre la [creación de una conexión de origen [!DNL Customer Attributes] en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obtener más información.
