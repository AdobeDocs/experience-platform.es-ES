---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Mezcla de IdentityMap
topic: overview
description: Este documento proporciona información general sobre la clase de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# [!UICONTROL Mezcla de IdentityMap]

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../name-updates.md) mezcla para obtener más información.

[!UICONTROL IdentityMap] es una combinación estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona un campo de mapa único, que contiene un conjunto de identidades de usuario con una clave de Área de nombres.

>[!WARNING]
>
>El sistema actualiza automáticamente el `IdentityMap` campo a medida que se ingestan datos de identidad. Para utilizar este campo correctamente para el Perfil [del cliente en tiempo](../../../profile/home.md)real, no intente actualizar manualmente el contenido del campo en sus operaciones de datos.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consulte la sección sobre mapas de identidad en los [conceptos básicos de la composición](../../schema/composition.md#identityMap) de esquemas para obtener más información sobre su caso de uso.