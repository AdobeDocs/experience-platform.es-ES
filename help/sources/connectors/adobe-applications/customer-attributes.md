---
keywords: Experience Platform;inicio;temas populares;conector de Atributos del cliente
solution: Experience Platform
title: Información general sobre el conector de origen de Atributos del cliente
description: Obtenga información sobre cómo conectar los Atributos del cliente a Adobe Experience Platform mediante API o la interfaz de usuario
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# Conector de atributos del cliente

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) en Experience Cloud permite cargar los datos empresariales capturados desde una base de datos de administración de la relación con los clientes (CRM). Puede cargar los datos en una fuente de datos de atributos del cliente de Experience Cloud y, a continuación, utilizar los datos en Adobe Analytics y Adobe Target.

El Experience Platform es compatible con la ingesta [!DNL Customer Attributes] datos de perfil en Adobe Experience Platform.

## Conjuntos de datos y esquemas

La variable [!DNL Customer Attributes] source crea automáticamente el conjunto de datos en el que los datos se dirigen. Este conjunto de datos creado automáticamente es fijo y no se puede seleccionar manualmente. El origen también crea automáticamente el esquema para el conjunto de datos en función del origen de datos de entrada. Este proceso también implica la creación automática de las asignaciones necesarias entre el esquema y los datos de origen.

## Identidades

La identidad principal de un conjunto de datos se encuentra en la primera columna del archivo CSV de los datos de origen. La variable [!DNL Customer Attributes] el origen supone que la identidad siempre está asignada al [`CORE` namespace](../../../identity-service/namespaces.md), un espacio de nombres generado por el sistema que admite [[!DNL Identity Service]](../../../identity-service/home.md).

No se puede seleccionar un área de nombres existente para la identidad al utilizar [!DNL Customer Attributes] source porque [!DNL Customer Attributes] supone que la identidad principal del esquema siempre está en el mapa de identidad. [!DNL Customer Attributes] a continuación, crea la asignación del ID de origen al UUID de mapa de identidad de forma automatizada.

Para [!DNL Customer Attributes] datos para enlazar a otros [!DNL Profile] Los conjuntos de datos de , sus datos e identidades deben poder coincidir con un ID de Experience Cloud.

Puede establecer la variable `CORE` espacio de nombres estableciendo el ID de Experience Cloud del visitante que utiliza [SDK web](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [SDK móvil](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)o [API del servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=es).

La variable [!DNL Customer Attributes] no rellena ninguna otra relación de identidad. Por ejemplo, si una [!DNL Customer Attributes] el conjunto de datos de origen contiene un **Correo electrónico** y **ID de fidelidad** , esos campos deben etiquetarse como campos de identidad en el esquema para que se puedan procesar en [!DNL Identity Service].

Consulte el tutorial en [crear un [!DNL Customer Attributes] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/adobe-applications/customer-attributes.md) para obtener más información.
