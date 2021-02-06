---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;dirección;xdm:dirección;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección postal
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de Dirección postal.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# [!UICONTROL Tipo ] de datos de dirección postal

[!UICONTROL La ] dirección postal es un tipo de datos XDM estándar que describe los detalles de una dirección de correo.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `city` | El nombre de la ciudad. |
| `country` | El nombre del territorio administrado por el gobierno. Se trata de un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `countryCode` | Código de dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> para el país. |
| `createdByBatchID` | ID del archivo de lote ingestado que creó el registro de direcciones. |
| `dmaID` | La investigación de medios Nielsen designó área de mercado. |
| `label` | Un nombre de forma libre para la dirección. |
| `lastVerifiedDate` | Fecha en la que se verificó por última vez la dirección como asociada a la persona. |
| `modifiedByBatchID` | El ID del archivo por lotes ingerido que modificó el registro por última vez. |
| `msaID` | Área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postOfficeBox` | La casilla de correo de la dirección. |
| `postalCode` | Código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contendrá parte del código postal. |
| `primary` | Un valor booleano que indica si esta es la dirección principal del individuo. Un perfil sólo puede tener una dirección `primary` en un momento dado. |
| `region` | La región, condado o distrito de la dirección. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | ID del usuario que modificó el registro por última vez. |
| `stateProvince` | El estado o la parte provincial de la observación. El formato sigue el estándar [ISO 3166-2 (país y subdivisión)](http://www.unece.org/cefact/locode/subdivisions.html). |
| `status` | Indica si la dirección se puede usar actualmente. |
| `statusReason` | Una descripción del `status` actual. |
| `street1` - `street4` | Estos cuatro campos están diseñados para contener información de nivel de calle principal, número de apartamento, número de calle y nombre de calle. `street2` a  `street4` son opcionales. |

Para obtener más información sobre el tipo de datos de dirección postal, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)