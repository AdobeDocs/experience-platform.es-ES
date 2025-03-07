---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;perfil individual;campos;esquemas;identityMap;mapa de identidad;mapa de identidad;diseño de esquema;mapa de identidad;esquema;esquema;esquema de unión;unión
title: Grupo de campos de esquema IdentityMap
description: Obtenga información acerca de la clase de perfil individual de XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL IdentityMap] es un grupo de campos de esquema estándar para la clase [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) y un grupo de campos compatible para la clase [[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de asignación, que contiene un conjunto de identidades de usuario marcadas por el área de nombres.

![Un diagrama del grupo de campos de esquema [!UICONTROL IdentityMap]](../../images/field-groups/identitymap.png)

Consulte la sección sobre mapas de identidad en los [conceptos básicos de la composición de esquemas](../../schema/composition.md#identityMap) para obtener más información sobre su caso de uso, incluidos sus beneficios y desventajas.

**ejemplo**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Para obtener más información sobre el grupo de campos, consulte el [esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) en el repositorio XDM público.
