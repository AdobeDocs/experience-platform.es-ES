---
title: Filtrado de respuestas en la API de Reactor
description: Obtenga información sobre cómo filtrar los resultados al enumerar recursos en la API de Reactor.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 100%

---

# Filtrado de respuestas en la API de Reactor

Al utilizar puntos finales de lista (GET) en la API de Reactor, es posible que necesite limitar los resultados devueltos a un subconjunto de registros. Para ello, muchos de los puntos finales de lista de la API admiten la capacidad de filtrar por atributos específicos. Si desea realizar consultas estructuradas a la API en su lugar, consulte la guía sobre [búsqueda](./search.md).

## Filtrado de sintaxis

En el siguiente ejemplo se explica cómo implementar filtros para las solicitudes de GET.

**Formato de API**

Para filtrar la respuesta de un extremo de lista determinado, debe proporcionar un parámetro de consulta `filter` en la ruta de solicitud.

>[!NOTE]
>
>La plantilla siguiente utiliza corchetes (`[]`) y caracteres de espacio para facilitar la lectura. En la práctica, estos caracteres deben contar con cifrado de URI, tal como se describe en [RFC 3986](https://tools.ietf.org/html/rfc3986). Más adelante en esta guía se muestra un ejemplo de una ruta de solicitud cifrada correctamente.
>
>Tenga en cuenta que si la estructura de los filtros es incorrecta, no se aplican filtros y se devuelve el conjunto de resultados completo.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Propiedad | Descripción |
| --- | --- |
| `{ENDPOINT}` | Punto final de lista en la API de Reactor que admite parámetros de filtro. |
| `{ATTRIBUTE_NAME}` | Nombre de un atributo específico por el que filtrar los resultados. Tenga en cuenta que los distintos extremos admiten atributos diferentes para el filtrado. Consulte la guía de referencia del extremo que está usando para obtener una lista de atributos de filtrado disponibles. |
| `{OPERATOR}` | El operador que determina cómo se evalúan los resultados frente al `{VALUE}` proporcionado. Los operadores admitidos se enumeran en la sección [apéndice](#supported-operators). |
| `{VALUE}` | Valor con el que comparar los resultados devueltos. Cuando se compara para la igualdad utilizando el operador `EQ`, el valor debe ser una coincidencia exacta que distinga entre mayúsculas y minúsculas para que se incluya en la respuesta. |

{style="table-layout:auto"}

**Solicitud**

La solicitud de ejemplo siguiente recupera una lista de bibliotecas publicadas aplicando un filtro que requiere que el atributo `state` de la biblioteca sea igual a `published`.

Antes del cifrado de URI, la sintaxis de este filtro en la ruta de solicitud sería similar a la siguiente:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Una vez que la ruta y los parámetros de consulta han sido cifrados con URI, pueden utilizarse en solicitudes de API como la que se muestra a continuación:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## Filtrado en varios valores {#multiple-values}

Para filtrar por varios valores para un único atributo, proporcione los valores como una lista separada por comas.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Uso de varios filtros

Para aplicar filtros para varios atributos, proporcione un parámetro `filter` para cada atributo. Los parámetros deben separarse con caracteres ampersand (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Si especifica el mismo atributo en varios filtros en la misma solicitud, solo se aplicará el último filtro proporcionado para ese atributo.

## Apéndice

La siguiente sección contiene información adicional para trabajar con filtros en la API de Reactor.

### Operadores de filtro admitidos {#operators}

En la tabla siguiente se enumeran los valores de operador admitidos como parámetros de filtro. Tenga en cuenta que, según el atributo por el que filtre, no todos los operadores de filtro disponibles serán aplicables, como el uso de operadores “menor que” o “mayor que” para atributos de cadena.

| Operador | Descripción |
| --- | --- |
| `EQ` | El atributo debe ser igual al valor proporcionado. |
| `NOT` | El atributo no debe ser igual al valor proporcionado. |
| `LT` | El atributo debe ser menor que el valor proporcionado. |
| `GT` | El atributo debe ser mayor que el valor proporcionado. |
| `BETWEEN` | El atributo debe encontrarse dentro de un rango de valores especificado. Al utilizar este operador, se deben proporcionar [dos valores](#multiple-values) para indicar los valores mínimo y máximo del rango deseado. |
| `CONTAINS` | El atributo debe contener el valor proporcionado, como un conjunto de caracteres dentro de un atributo de cadena. |
