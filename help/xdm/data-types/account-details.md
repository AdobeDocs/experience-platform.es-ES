---
title: Tipo de datos de detalles de la cuenta
description: Este documento proporciona información general sobre el tipo de datos del Modelo de datos de experiencia (XDM) de detalles de la cuenta.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL Detalles de la cuenta] tipo de datos

[!UICONTROL Detalles de la cuenta] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles relacionados con una organización empresarial.

![Estructura del tipo de datos](../images/data-types/account-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Moneda]](./currency.md) | El importe estimado de los ingresos anuales de la organización. |
| `DUNSNumber` | Cadena | El número D-U-N-S de Dun &amp; Bradstreet de la organización. Se trata de un número no indicativo de nueve dígitos asignado a cada ubicación comercial en la base de datos de Dun &amp; Bradstreet que tiene una operación única, independiente y diferenciada, y es mantenido exclusivamente por Dun &amp; Bradstreet. |
| `NAICSCode` | Cadena | Clasificación de la organización dentro del Sistema de Clasificación de la Industria de América del Norte. |
| `NAICSDescription` | Cadena | Breve descripción de la línea de negocio de una organización, basada en su código NAICS. |
| `SICCode` | Cadena | El código de clasificación industrial estándar (SIC) de la organización. Este es un código de cuatro dígitos que categoriza el sector al que pertenecen las empresas en función de sus actividades comerciales. |
| `SICDescription` | Cadena | Breve descripción de la línea de negocio de una organización, basada en su código SIC. |
| `companyProductAndServices` | Cadena | Los productos y servicios en los que la organización está negociando o haciendo negocios. |
| `facebookPageUrl` | Cadena | Un vínculo a la cuenta de Facebook de la organización. |
| `industry` | Cadena | El sector del que forma parte esta organización. Se trata de un campo de forma libre y se recomienda utilizar un valor estructurado para las consultas o para usar la variable `xdm:classifier` propiedad. |
| `jigsaw` | Cadena | La clave Data.com para la organización. |
| `linkedinPageUrl` | Cadena | Un vínculo a la cuenta de LinkedIn de la organización. |
| `logoUrl` | Cadena | Una ruta que se combinará con la URL de una instancia de Salesforce (por ejemplo, `https://yourInstance.salesforce.com/`) para generar una dirección URL que solicite la imagen de perfil de red social asociada a la organización. La URL generada devuelve un redireccionamiento HTTP (código 302) a la imagen de perfil de red social de la organización. |
| `marketSegment` | Cadena | El segmento de mercado designado en el que participa la organización. Se trata de un campo de forma libre y se recomienda utilizar un valor estructurado para las consultas o para usar la variable `xdm:identifier` propiedad. |
| `numberOfEmployees` | Número entero | Número de empleados de la organización. |
| `organizationType` | Cadena | Etiqueta que describe el tipo de organización. |
| `primaryEmailDomain` | Cadena | El dominio de correo electrónico principal que utiliza la organización para su personal. |
| `rating` | Duplicada | Puntuación calculada o clasificación por estrellas para esta organización. `1` indica la clasificación máxima posible, y `0` es la clasificación mínima posible. |
| `tickerSymbol` | Cadena | Símbolo del mercado de valores para esta cuenta. Máximo de 20 caracteres. |
| `twitterHandleUrl` | Cadena | Un vínculo del sitio web al identificador de twitter de la organización. |
| `website` | Cadena | Dirección URL del sitio web de la organización. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
