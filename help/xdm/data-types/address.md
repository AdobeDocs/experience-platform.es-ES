---
title: Tipo de datos de dirección postal
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de la dirección postal.
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 42%

---

# [!UICONTROL Tipo de datos de la dirección postal]

[!UICONTROL La dirección postal] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que proporciona detalles de dirección.

![Un diagrama del tipo de datos [!UICONTROL Dirección postal].](../images/data-types/postal-address.png)

| Nombre para mostrar | Propiedad | Tipo de datos | Descripción |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principal] | `primary` | Booleano | Indicador de dirección principal. Un perfil solo puede tener una dirección `primary` en un momento determinado. |
| [!UICONTROL Etiqueta] | `label` | cadena | Nombre en formato aleatorio de la dirección. |
| [!UICONTROL Calle 1] | `street1` | cadena | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| [!UICONTROL Calle 2] | `street2` | cadena | Segunda línea para información de dirección (opcional). |
| [!UICONTROL Calle 3] | `street3` | cadena | Tercera línea para información de dirección (opcional). |
| [!UICONTROL Calle 4] | `street4` | cadena | Cuarta línea para información de dirección (opcional). |
| [!UICONTROL Región] | `region` | cadena | La parte de región, condado o distrito de la dirección. |
| [!UICONTROL apartado de oficinas de Post] | `postOfficeBox` | cadena | Apartado de correos de la dirección. |
| [!UICONTROL País] | `country` | cadena | El nombre del territorio administrado por el gobierno. Aparte de ``countryCode``, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| [!UICONTROL Estado] | `state` | cadena | Nombre del estado. Este es un campo improvisado. |
| [!UICONTROL Estado] | `status` | cadena | Una indicación de la capacidad de uso de la dirección. |
| [!UICONTROL Razón del estado] | `statusReason` | cadena | Una descripción del estado actual. |
| [!UICONTROL Última fecha de verificación] | `lastVerifiedDate` | cadena | La fecha en la que se verificó por última vez que la dirección aún estaba asociada a la persona. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el [esquema completo](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) en el repositorio XDM público:
