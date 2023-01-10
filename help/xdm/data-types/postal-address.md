---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dirección;xdm:dirección;tipo de datos;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección postal
description: Este documento proporciona información general sobre el tipo de datos XDM de la dirección postal.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Dirección postal] tipo de datos

[!UICONTROL Dirección postal] es un tipo de datos XDM estándar que describe los detalles de una dirección de correo.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `city` | El nombre de la ciudad. |
| `country` | Nombre del territorio administrado por el gobierno. Se trata de un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `countryCode` | Los dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alfa-2</a> para el país. |
| `createdByBatchID` | El ID del archivo por lotes introducido que creó el registro de direcciones. |
| `dmaID` | La investigación de medios de comunicación de Nielsen designó zona de mercado. |
| `label` | Un nombre de forma libre para la dirección. |
| `lastVerifiedDate` | La fecha en la que se verificó por última vez la dirección como asociada a la persona. |
| `modifiedByBatchID` | El ID del archivo por lotes introducido que modificó el registro por última vez. |
| `msaID` | El área estadística metropolitana en los Estados Unidos donde se produjo la observación. |
| `postOfficeBox` | La casilla de la oficina de correos de la dirección. |
| `postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles para todos los países. En algunos países, esto solo contiene parte del código postal. |
| `primary` | Un valor booleano que indica si esta es la dirección principal del individuo. Un perfil solo puede tener uno `primary` dirección en un momento determinado. |
| `region` | Región, condado o distrito de la dirección. |
| `repositoryCreatedBy` | ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |
| `stateProvince` | Estado o provincia de la observación. El formato sigue a la variable [ISO 3166-2 (país y subdivisión)](https://www.unece.org/cefact/locode/subdivisions.html) estándar. |
| `status` | Indica si la dirección se puede utilizar actualmente. |
| `statusReason` | Una descripción de la `status`. |
| `street1` - `street4` | Estos cuatro campos están pensados para contener información de nivel de calle principal, número de apartamento, número de calle y nombre de calle. `street2` a `street4` son opcionales. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos de dirección postal, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
