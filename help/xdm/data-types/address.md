---
title: Tipo de datos de dirección postal
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de la dirección postal.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 9%

---

# [!UICONTROL Dirección postal] tipo de datos

[!UICONTROL Dirección postal] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona detalles de dirección.

![Un diagrama de la [!UICONTROL Dirección postal] tipo de datos.](../images/data-types/postal-address.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principal] | `primary` | Booleano | Indicador de dirección principal. Un perfil solo puede tener uno `primary` dirección en un momento determinado. |
| [!UICONTROL Etiqueta] | `label` | string | Nombre en formato libre de la dirección. |
| [!UICONTROL Calle 1] | `street1` | string | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| [!UICONTROL Calle 2] | `street2` | string | Segunda línea para información de dirección (opcional) |
| [!UICONTROL Calle 3] | `street3` | string | Tercera línea para información de dirección (opcional). |
| [!UICONTROL Calle 4] | `street4` | string | Cuarta línea para información de dirección (opcional). |
| [!UICONTROL Región] | `region` | string | La región, condado o distrito de la dirección. |
| [!UICONTROL Apartado de correos] | `postOfficeBox` | string | Apartado de correos de la dirección. |
| [!UICONTROL País] | `country` | string | El nombre del territorio administrado por el gobierno. Distinto a ``countryCode``Sin embargo, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| [!UICONTROL Estado] | `state` | string | El nombre del estado. Este es un campo de forma libre. |
| [!UICONTROL Estado] | `status` | string | Una indicación de la capacidad de uso de la dirección. |
| [!UICONTROL Razón del estado] | `statusReason` | string | Una descripción del estado actual. |
| [!UICONTROL Última fecha de verificación] | `lastVerifiedDate` | string | La fecha en la que se verificó por última vez que la dirección aún estaba asociada a la persona. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte la [esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) en el repositorio XDM público:
