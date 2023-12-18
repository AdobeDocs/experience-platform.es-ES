---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;dirección;xdm:address;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección postal
description: Obtenga información sobre el tipo de datos XDM de la dirección postal.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# [!UICONTROL Dirección postal] tipo de datos

[!UICONTROL Dirección postal] es un tipo de datos XDM estándar que describe los detalles de una dirección de correo.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `city` | El nombre de la ciudad. |
| `country` | El nombre del territorio administrado por el gobierno. Este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `countryCode` | Los dos caracteres <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> código del país. |
| `createdByBatchID` | El ID del archivo por lotes ingerido que creó el registro de dirección. |
| `dmaID` | El área de mercado designada por Nielsen Media Research. |
| `label` | Un nombre en formato libre para la dirección. |
| `lastVerifiedDate` | La fecha en la que se verificó por última vez que la dirección aún estaba asociada a la persona. |
| `modifiedByBatchID` | ID del archivo por lotes ingerido que modificó el registro por última vez. |
| `msaID` | El área estadística metropolitana de los Estados Unidos donde ocurrió la observación. |
| `postOfficeBox` | El apartado de correos de la dirección. |
| `postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `primary` | Un valor booleano que indica si esta es la dirección principal del individuo. Un perfil solo puede tener uno `primary` dirección en un momento determinado. |
| `region` | La región, condado o distrito de la dirección. |
| `repositoryCreatedBy` | El ID del usuario que creó el registro. |
| `repositoryLastModifiedBy` | El ID del usuario que modificó el registro por última vez. |
| `stateProvince` | Estado o parte de provincia de la observación. El formato sigue el [ISO 3166-2 (país y subdivisión)](https://www.unece.org/cefact/locode/subdivisions.html) estándar. |
| `status` | Indica si la dirección se puede utilizar actualmente. |
| `statusReason` | Una descripción del actual `status`. |
| `street1` - `street4` | Estos cuatro campos están pensados para contener información principal de la dirección postal, número de piso, número de calle y nombre de la calle. `street2` hasta `street4` son opcionales. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos de la dirección postal, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
