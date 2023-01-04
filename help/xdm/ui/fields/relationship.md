---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;relación;campo
solution: Experience Platform
title: Definir campos de relación en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de relación en la interfaz de usuario del Experience Platform.
topic-legacy: user guide
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definir campos de relación en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un [esquema de unión](../../schema/composition.md#union) es una vista unificada de todos los esquemas pertenecientes a la misma clase que también se han habilitado para [Perfil del cliente en tiempo real](../../../profile/home.md). Profile aprovecha el esquema de unión para construir una representación completa de un cliente a partir de datos de experiencia dispares.

En algunos casos, es posible que esté incorporando datos que no necesariamente formen parte de un perfil, pero que no estén relacionados con él. Un ejemplo de este tipo de datos sería un campo &quot;hotel favorito&quot; para un cliente. Dado que los atributos del hotel favorito de una persona no son atributos de la propia persona, un hotel se representa mejor mediante un esquema separado basado en una clase personalizada en lugar de [!DNL XDM Individual Profile].

Dado que los esquemas de unión solo se basan en esquemas que comparten la misma clase, simplemente habilitar el esquema &quot;Hoteles&quot; para su uso en Perfil no incluirá su esquema de unión de campos para [!DNL XDM Individual Profile]. En su lugar, debe definir una relación entre &quot;Hoteles&quot; y otro esquema perteneciente a la unión. Esto implica definir una **campo de relación** en un esquema de origen que hace referencia a la identidad principal de un esquema de destino.

Para ver los pasos detallados sobre la definición de una relación entre dos esquemas en la interfaz de usuario de Adobe Experience Platform, consulte la [tutorial de interfaz de usuario de relación](../../tutorials/relationship-ui.md).
