---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;mapa de identidad;mapa de identidad;mapa de identidad;mapa de Esquema;mapa;mapa;unión esquema;unión
solution: Experience Platform
title: Mezcla de IdentityMap
topic: overview
description: Este documento proporciona información general sobre la clase de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


#  IdentityMapmixin

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento en [actualizaciones de nombres de mezcla](../name-updates.md) para obtener más información.

 IdentityMapis es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona un campo de mapa único, que contiene un conjunto de identidades de usuario con una clave de Área de nombres.

>[!WARNING]
>
>El sistema actualiza automáticamente el campo `IdentityMap` a medida que se ingieren datos de identidad. Para utilizar este campo correctamente para [Perfil del cliente en tiempo real](../../../profile/home.md), no intente actualizar manualmente el contenido del campo en sus operaciones de datos.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consulte la sección sobre mapas de identidad en [conceptos básicos de la composición de esquema](../../schema/composition.md#identityMap) para obtener más información sobre su caso de uso.