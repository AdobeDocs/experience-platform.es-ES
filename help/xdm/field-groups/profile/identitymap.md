---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;esquemas;identityMap;mapa de identidad;mapa de identidad;diseño de esquema;mapa;esquema;esquema de unión;;esquema;esquema de unión
title: Grupo de campos de esquema IdentityMap
description: Obtenga información acerca de la clase de perfil individual de XDM.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# [!UICONTROL IdentityMap] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL IdentityMap] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de asignación, que contiene un conjunto de identidades de usuario marcadas por el área de nombres.

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
