---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;esquemas;detalles de lealtad;Diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de fidelización
description: Obtenga información acerca del grupo de campos de esquema Detalles de fidelización.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL Detalles de fidelización] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de fidelización] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de tipo de objeto, `loyalty`, que captura información relacionada con la pertenencia de una persona a un programa de fidelidad de clientes.

![](../../images/field-groups/loyalty-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `pointsExpiration` | Matriz de objetos | Enumera los puntos de fidelidad (o grupos de puntos de fidelidad) que van a caducar y las fechas en las que caducarán. Cada elemento de matriz debe ser un objeto que contenga las dos propiedades siguientes: <ul><li>`pointsExpirationDate`: fecha y hora ISO 8601 de caducidad de los puntos.</li><li>`pointsExpiring`: el saldo de puntos vence en la fecha de vencimiento asociada.</li></ul> |
| `joinDate` | Fecha/Hora | Fecha y hora ISO 8601 en que la persona se unió al programa de fidelidad. |
| `loyaltyID` | Matriz de cadenas | Representa los ID del programa de fidelización asociados con el miembro del programa de fidelización. |
| `points` | Duplicada | El saldo actual de puntos de fidelidad o premios para el miembro socio. |
| `pointsRedeemed` | Duplicada | Cantidad de puntos que el miembro socio ha aplicado a una compra o ha canjeado de otro modo. |
| `program` | Cadena | El nombre del programa de fidelización en el que está inscrita la persona. |
| `status` | Cadena | El estado actual de la pertenencia de fidelidad de la persona, como `active`, `disabled` o `suspended`. |
| `tier` | Cadena | Registra el nivel del programa de fidelización en el que está inscrita la persona. |
| `upgradeDate` | Cadena | La fecha en la que el miembro socio se actualizó a su nivel más reciente. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
