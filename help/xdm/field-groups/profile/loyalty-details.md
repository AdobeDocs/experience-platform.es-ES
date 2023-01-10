---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;detalles de lealtad;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Detalles de fidelidad Grupo de campos de esquema
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de lealtad .
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 3%

---

# [!UICONTROL Detalles de fidelidad] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de fidelidad] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de tipo objeto, `loyalty`, que captura información relacionada con la pertenencia de una persona a un programa de fidelidad de cliente.

![](../../images/field-groups/loyalty-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `pointsExpiration` | Matriz de objetos | Enumera cualquier punto de lealtad (o grupo de puntos de lealtad) que caducará y las fechas en las que caducará. Cada elemento de matriz debe ser un objeto que contenga las dos propiedades siguientes: <ul><li>`pointsExpirationDate`: Una fecha y hora ISO 8601 del momento en que caducarán los puntos.</li><li>`pointsExpiring`: El saldo de punto que caduca a partir de la fecha de caducidad asociada.</li></ul> |
| `joinDate` | DateTime | Una fecha y hora ISO 8601 del momento en que la persona se unió al programa de fidelidad. |
| `loyaltyID` | Matriz de cadenas | Representa los ID de programa de fidelidad asociados al miembro del programa de fidelidad. |
| `points` | Doble | El balance actual de puntos de lealtad o premios para el miembro socio. |
| `pointsRedeemed` | Doble | Cantidad de puntos que el miembro socio ha aplicado a una compra o que ha redimido de otra manera. |
| `program` | Cadena | Nombre del programa de fidelidad en el que está inscrita la persona. |
| `status` | Cadena | El estado actual de la pertenencia de fidelidad de la persona, como `active`, `disabled`o `suspended`. |
| `tier` | Cadena | Captura el nivel de programa de fidelidad en el que está inscrita la persona. |
| `upgradeDate` | Cadena | La fecha en la que el miembro socio se actualizó a su nivel de nivel más reciente. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
