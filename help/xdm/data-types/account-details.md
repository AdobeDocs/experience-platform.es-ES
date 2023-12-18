---
title: Tipo de datos de detalles de cuenta
description: Obtenga información acerca del tipo de datos del modelo de datos de experiencia (XDM) de detalles de la cuenta.
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 5%

---

# [!UICONTROL Detalles de cuenta] tipo de datos

[!UICONTROL Detalles de cuenta] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe detalles relacionados con una organización empresarial.

![Estructura de tipo de datos](../images/data-types/account-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Moneda]](./currency.md) | El importe estimado de los ingresos anuales de la organización. |
| `DUNSNumber` | Cadena | Número D-U-N-S de Dun &amp; Bradstreet de la organización. Se trata de un número no indicativo de nueve dígitos asignado a cada ubicación empresarial en la base de datos de Dun &amp; Bradstreet que tiene una operación única, separada y distinta, y que mantiene únicamente Dun &amp; Bradstreet. |
| `NAICSCode` | Cadena | La clasificación de la organización dentro del Sistema de Clasificación Industrial de América del Norte. |
| `NAICSDescription` | Cadena | Una breve descripción de la línea de negocio de una organización, basada en su código NAICS. |
| `SICCode` | Cadena | El código de clasificación industrial estándar (SIC) de la organización. Se trata de un código de cuatro dígitos que categoriza el sector al que pertenecen las empresas en función de sus actividades comerciales. |
| `SICDescription` | Cadena | Una breve descripción de la línea de negocio de una organización, basada en su código SIC. |
| `companyProductAndServices` | Cadena | Los productos y servicios con los que la organización está negociando o haciendo negocios. |
| `facebookPageUrl` | Cadena | Un vínculo al sitio web de la cuenta de Facebook de la organización. |
| `industry` | Cadena | La industria de la que forma parte esta organización. Este es un campo de forma libre, y es aconsejable utilizar un valor estructurado para consultas o para utilizar la variable `xdm:classifier` propiedad. |
| `jigsaw` | Cadena | La clave Data.com de la organización. |
| `linkedinPageUrl` | Cadena | Un vínculo al sitio web de la cuenta de LinkedIn de la organización. |
| `logoUrl` | Cadena | Una ruta que se combinará con la URL de una instancia de Salesforce (por ejemplo, `https://yourInstance.salesforce.com/`) para generar una URL para solicitar la imagen de perfil de la red social asociada a la organización. La URL generada devuelve un redireccionamiento HTTP (código 302) a la imagen de perfil de la red social de la organización. |
| `marketSegment` | Cadena | La audiencia de mercado designada en la que participa la organización. Este es un campo de forma libre, y es aconsejable utilizar un valor estructurado para consultas o para utilizar la variable `xdm:identifier` propiedad. |
| `numberOfEmployees` | Número entero | El número de empleados de la organización. |
| `organizationType` | Cadena | Una etiqueta que describe el tipo de organización. |
| `primaryEmailDomain` | Cadena | El dominio de correo electrónico principal que utiliza la organización para su personal. |
| `rating` | Doble | La puntuación calculada o la clasificación por estrellas de esta organización. `1` indica la clasificación máxima posible, y `0` es la calificación mínima posible. |
| `tickerSymbol` | Cadena | El símbolo del mercado de valores de esta cuenta. Máximo de 20 caracteres. |
| `twitterHandleUrl` | Cadena | Un vínculo del sitio web al identificador de twitter de la organización. |
| `website` | Cadena | Dirección URL del sitio web de la organización. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
