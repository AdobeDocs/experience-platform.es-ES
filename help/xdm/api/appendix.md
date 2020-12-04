---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: Apéndice para desarrolladores de esquema Registry
description: Este documento proporciona información adicional relacionada con el trabajo con la API del Registro de Esquemas.
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---


# Apéndice

Este documento proporciona información adicional relacionada con el trabajo con la [!DNL Schema Registry] API.

## Uso de parámetros de consulta {#query}

La opción [!DNL Schema Registry] admite el uso de parámetros de consulta para filtrar los resultados de la página al enumerar los recursos.

>[!NOTE]
>
>Cuando se combinan varios parámetros de consulta, deben separarse con signos ampersands (`&`).

### Paginación {#paging}

Los parámetros de consulta más comunes para la paginación incluyen:

| Parámetro | Descripción |
| --- | --- |
| `start` | Especifique dónde deben comenzar los resultados enumerados. Este valor puede obtenerse del `_page.next` atributo de una respuesta de lista y utilizarse para acceder a la siguiente página de resultados. Si el `_page.next` valor es nulo, no hay ninguna página adicional disponible. |
| `limit` | Limite el número de recursos devueltos. Ejemplo: `limit=5` devolverá una lista de cinco recursos. |
| `orderby` | Ordene los resultados por una propiedad específica. Ejemplo: `orderby=title` clasificará los resultados por título en orden ascendente (A-Z). Añadir un `-` antes del valor del parámetro (`orderby=-title`) ordenará los elementos por título en orden descendente (Z-A). |

### Filtro {#filtering}

Puede filtrar los resultados utilizando el `property` parámetro, que se utiliza para aplicar un operador específico a una propiedad JSON determinada dentro de los recursos recuperados. Los operadores admitidos son:

| Operador | Descripción | Ejemplo |
| --- | --- | --- |
| `==` | Filtros si la propiedad es igual al valor proporcionado. | `property=title==test` |
| `!=` | Filtros por si la propiedad no es igual al valor proporcionado. | `property=title!=test` |
| `<` | Filtros si la propiedad es menor que el valor proporcionado. | `property=version<5` |
| `>` | Filtros según si la propiedad es buena que el valor proporcionado. | `property=version>5` |
| `<=` | Filtros por si la propiedad es menor o igual que el valor proporcionado. | `property=version<=5` |
| `>=` | Filtros por si la propiedad es buena o igual al valor proporcionado. | `property=version>=5` |
| `~` | Filtros según si la propiedad coincide con una expresión regular proporcionada. | `property=title~test$` |
| (Ninguna) | Si se establece únicamente el nombre de la propiedad, solo se devuelven las entradas donde existe la propiedad. | `property=title` |

>[!TIP]
>
>Puede utilizar el `property` parámetro para filtrar mezclas según su clase compatible. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` devuelve solo las mezclas compatibles con la [!DNL XDM Individual Profile] clase.

## Modo de compatibilidad

[!DNL Experience Data Model] (XDM) es una especificación públicamente documentada, impulsada por el Adobe de mejorar la interoperabilidad, la expresividad y el poder de las experiencias digitales. Adobe mantiene el código fuente y las definiciones XDM formales en un proyecto de código [abierto en GitHub](https://github.com/adobe/xdm/). Estas definiciones se escriben en notación estándar XDM, utilizando JSON-LD (JavaScript Object Notation for Linked Data) y Esquema JSON como gramática para definir esquemas XDM.

Al consultar las definiciones XDM formales en el repositorio público, puede ver que el XDM estándar difiere de lo que ve en Adobe Experience Platform. Lo que se ve en [!DNL Experience Platform] se llama Modo de compatibilidad y proporciona una sencilla asignación entre el XDM estándar y la forma en que se utiliza en [!DNL Platform].

### Funcionamiento del modo de compatibilidad

El modo de compatibilidad permite que el modelo JSON-LD de XDM funcione con la infraestructura de datos existente alterando los valores dentro del XDM estándar manteniendo la semántica igual. Utiliza una estructura JSON anidada, que muestra esquemas en un formato de árbol.

La principal diferencia que notará entre el modo XDM estándar y el modo de compatibilidad es la eliminación del prefijo &quot;xdm:&quot; para los nombres de campo.

A continuación se muestra una comparación paralela que muestra los campos relacionados con el cumpleaños (con los atributos &quot;description&quot; eliminados) tanto en el modo XDM estándar como en el modo de compatibilidad. Observe que los campos Modo de compatibilidad incluyen una referencia al campo XDM y su tipo de datos en los atributos &quot;meta:xdmField&quot; y &quot;meta:xdmType&quot;.

<table>
  <th>XDM estándar</th>
  <th>Modo de compatibilidad</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:bornDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date", }, "xdm:bornDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", }, "xdm:bornYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "bornDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date", "meta:xdmField": "xdm:bornDate", "meta:xdmType": "date" }, "bornDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:bornDayAndMonth", "meta:xdmType": "string" }, "bornYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767, "meta:xdmField": "xdm:bornYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### ¿Por qué es necesario el modo de compatibilidad?

Adobe Experience Platform está diseñado para trabajar con múltiples soluciones y servicios, cada uno con sus propios desafíos y limitaciones técnicos (por ejemplo, cómo ciertas tecnologías manejan caracteres especiales). Para superar estas limitaciones, se desarrolló el Modo de compatibilidad.

La mayoría de [!DNL Experience Platform] los servicios, incluidos [!DNL Catalog], [!DNL Data Lake]y [!DNL Real-time Customer Profile] utilizados [!DNL Compatibility Mode] en lugar de XDM estándar. La [!DNL Schema Registry] API también utiliza [!DNL Compatibility Mode], y todos los ejemplos de este documento se muestran usando [!DNL Compatibility Mode].

Vale la pena saber que se produce una asignación entre el XDM estándar y la forma en que se realiza su operación en [!DNL Experience Platform], pero no debería afectar al uso de [!DNL Platform] los servicios.

El proyecto de código abierto está disponible para usted, pero cuando se trata de interactuar con los recursos a través del [!DNL Schema Registry], los ejemplos de API de este documento proporcionan las prácticas recomendadas que debe conocer y seguir.