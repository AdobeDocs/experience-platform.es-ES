---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos;ui;espacio de trabajo;relación;campo;
solution: Experience Platform
title: Definición de campos de relación en la IU
description: Obtenga información sobre cómo definir un campo de relación en la interfaz de usuario del Experience Platform.
exl-id: 8a6be545-0edb-4b9c-b164-e44a7a5f54f5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Definición de campos de relación en la IU

En Experience Data Model (XDM), un [esquema de unión](../../schema/composition.md#union) es una vista unificada de todos los esquemas que pertenecen a la misma clase y que también se han habilitado para [Perfil del cliente en tiempo real](../../../profile/home.md). El esquema de unión lo aprovecha el perfil para construir una representación completa de un cliente a partir de datos de experiencias dispares.

En algunos casos, es posible que esté introduciendo datos que no necesariamente forman parte de un perfil, pero que, sin embargo, están relacionados con el perfil. Un ejemplo de este tipo de datos sería un campo &quot;hotel favorito&quot; para un cliente. Dado que los atributos del hotel favorito de una persona no son atributos de la propia persona, un hotel se representa mejor mediante un esquema independiente basado en una clase personalizada que [!DNL XDM Individual Profile].

Dado que los esquemas de unión solo se basan en esquemas que comparten la misma clase, al habilitar el esquema &quot;Hotels&quot; para utilizarlo en el perfil, no se incluirá su esquema de unión de campos para [!DNL XDM Individual Profile]. En su lugar, debe definir una relación entre &quot;Hotels&quot; y otro esquema que pertenezca a la unión. Esto implica definir un **campo de relación** en un esquema de origen que hace referencia a la identidad principal de un esquema de referencia.

Para ver los pasos detallados sobre cómo definir una relación entre dos esquemas en la interfaz de usuario de Adobe Experience Platform, consulte el [tutorial de la interfaz de usuario de la relación](../../tutorials/relationship-ui.md).
