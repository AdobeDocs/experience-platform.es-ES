---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;relación;campo;
solution: Experience Platform
title: Definición de un campo de relación en la interfaz de usuario
description: Obtenga información sobre cómo definir un campo de relación en la interfaz de usuario del Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Definición de un campo de relación en la interfaz de usuario

En el Modelo de datos de experiencia (XDM), un [esquema de unión](../../schema/composition.md#union) es una vista unificada de todos los esquemas pertenecientes a la misma clase que también se han habilitado para [Perfil del cliente en tiempo real](../../../profile/home.md). El Perfil aprovecha el esquema de unión para construir una representación completa de un cliente a partir de datos de experiencia dispares.

En algunos casos, puede estar ingiriendo datos que no necesariamente forman parte de un perfil, pero que, sin embargo, están relacionados con el perfil. Un ejemplo de este tipo de datos sería un campo de &quot;hotel favorito&quot; para un cliente. Dado que los atributos del hotel favorito de una persona no son atributos de la misma persona, un hotel se representa mejor con un esquema separado basado en una clase personalizada en lugar de [!DNL XDM Individual Profile].

Dado que los esquemas de unión se basan solamente en esquemas que comparten la misma clase, simplemente habilitar el esquema &quot;Hoteles&quot; para su uso en Perfil no incluirá su esquema de unión de campos para [!DNL XDM Individual Profile]. En su lugar, debe definir una relación entre &quot;Hoteles&quot; y otro esquema que pertenece a la unión. Esto implica definir un **campo de relación** en un esquema de origen que haga referencia a la identidad principal de un esquema de destino.

Para ver los pasos detallados sobre la definición de una relación entre dos esquemas en la interfaz de usuario de Adobe Experience Platform, consulte el [tutorial de interfaz de usuario de relación](../../tutorials/relationship-ui.md).