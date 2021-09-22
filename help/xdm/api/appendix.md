---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;compatibilidad;modo de compatibilidad;modo de compatibilidad;tipo de campo;tipos de campo
solution: Experience Platform
title: Apéndice de la API del Registro de Esquemas
description: Este documento proporciona información complementaria relacionada con el trabajo con la API del Registro de esquemas.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 403dcb75e43b5c7aa462495086e5a9e403ef6f5b
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Apéndice de la guía de API del Registro de Esquemas

Este documento proporciona información complementaria relacionada con el trabajo con la API [!DNL Schema Registry].

## Uso de parámetros de consulta {#query}

El [!DNL Schema Registry] admite el uso de parámetros de consulta en la página y filtrar los resultados al enumerar recursos.

>[!NOTE]
>
>Cuando se combinan varios parámetros de consulta, deben separarse con ampersands (`&`).

### Paginación {#paging}

Los parámetros de consulta más comunes para la paginación incluyen:

| Parámetro | Descripción |
| --- | --- |
| `orderby` | Ordene los resultados por una propiedad específica. Ejemplo: `orderby=title` ordenará los resultados por título en orden ascendente (A-Z). Si se añade un `-` antes del valor del parámetro (`orderby=-title`), los elementos se ordenarán por título en orden descendente (Z-A). |
| `limit` | Cuando se utiliza junto con un parámetro `orderby` , `limit` restringe el número máximo de elementos que deben devolverse para una solicitud determinada. Este parámetro no se puede usar sin un parámetro `orderby` presente.<br><br>El  `limit` parámetro especifica un número entero positivo (entre  `0` y  `500`) como un  ** número hintas al número máximo de elementos que deben devolverse. Por ejemplo, `limit=5` devuelve solo cinco recursos en la lista. Sin embargo, este valor no se respeta estrictamente. El tamaño real de la respuesta puede ser menor o mayor, ya que está limitado por la necesidad de proporcionar el funcionamiento fiable del parámetro `start`, si se proporciona uno. |
| `start` | Cuando se utiliza junto con un parámetro `orderby` , `start` especifica dónde debe comenzar la lista de elementos de la subconfiguración. Este parámetro no se puede usar sin un parámetro `orderby` presente. Este valor se puede obtener del atributo `_page.next` de una respuesta de lista y se puede utilizar para acceder a la siguiente página de resultados. Si el valor `_page.next` es nulo, no hay ninguna página adicional disponible.<br><br>Normalmente, este parámetro se omite para obtener la primera página de resultados. Después, `start` debe configurarse con el valor máximo de la propiedad de ordenación principal del campo `orderby` recibido en la página anterior. A continuación, la respuesta de API devuelve entradas que comienzan con las que tienen una propiedad de ordenación principal de `orderby` estrictamente buena (para ascendente) o estrictamente inferiores (para descendente) al valor especificado.<br><br>Por ejemplo, si el  `orderby` parámetro se establece en  `orderby=name,firstname`, el  `start` parámetro contendrá un valor para la  `name` propiedad. En este caso, si desea mostrar las 20 entradas siguientes de un recurso inmediatamente después del nombre &quot;Miller&quot;, debe utilizar: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtro {#filtering}

Puede filtrar los resultados utilizando el parámetro `property` , que se utiliza para aplicar un operador específico a una propiedad JSON determinada dentro de los recursos recuperados. Los operadores admitidos son:

| Operador | Descripción | Ejemplo |
| --- | --- | --- |
| `==` | Filtra si la propiedad es igual al valor proporcionado. | `property=title==test` |
| `!=` | Filtra si la propiedad no es igual al valor proporcionado. | `property=title!=test` |
| `<` | Filtra si la propiedad es menor que el valor proporcionado. | `property=version<5` |
| `>` | Filtra si la propiedad es buena que el valor proporcionado. | `property=version>5` |
| `<=` | Filtra si la propiedad es menor o igual que el valor proporcionado. | `property=version<=5` |
| `>=` | Filtra por si la propiedad es buena o igual al valor proporcionado. | `property=version>=5` |
| `~` | Filtra si la propiedad coincide con una expresión regular proporcionada. | `property=title~test$` |
| (Ninguna) | Al indicar solo el nombre de propiedad, solo se devuelven las entradas en las que existe la propiedad. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Puede utilizar el parámetro `property` para filtrar grupos de campos de esquema por su clase compatible. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` solo devuelve grupos de campos compatibles con la clase [!DNL XDM Individual Profile].

## Modo de compatibilidad {#compatibility}

[!DNL Experience Data Model] (XDM) es una especificación públicamente documentada, impulsada por el Adobe para mejorar la interoperabilidad, la expresividad y el poder de las experiencias digitales. Adobe mantiene el código fuente y las definiciones XDM formales en un [proyecto de código abierto en GitHub](https://github.com/adobe/xdm/). Estas definiciones se escriben en la Notación estándar XDM, utilizando JSON-LD (Notación de objetos JavaScript para datos vinculados) y Esquema JSON como gramática para definir esquemas XDM.

Al consultar las definiciones formales de XDM en el repositorio público, puede ver que el XDM estándar difiere de lo que ve en Adobe Experience Platform. Lo que está viendo en [!DNL Experience Platform] se llama Modo de compatibilidad y proporciona una asignación simple entre el XDM estándar y la forma en que se utiliza dentro de [!DNL Platform].

### Funcionamiento del modo de compatibilidad

El modo de compatibilidad permite que el modelo JSON-LD de XDM funcione con la infraestructura de datos existente al modificar los valores dentro del XDM estándar y mantener la semántica igual. Utiliza una estructura JSON anidada, que muestra los esquemas en un formato de árbol.

La principal diferencia que notará entre el XDM estándar y el Modo de compatibilidad es la eliminación del prefijo &quot;xdm:&quot; para los nombres de campo.

A continuación se muestra una comparación en paralelo que muestra los campos relacionados con el cumpleaños (con los atributos de &quot;descripción&quot; eliminados) tanto en el XDM estándar como en el modo de compatibilidad. Observe que los campos Modo de compatibilidad incluyen una referencia al campo XDM y su tipo de datos en los atributos &quot;meta:xdmField&quot; y &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM estándar</th>
  <th>Modo de compatibilidad</th>
  <tr>
  <td>
  <pre class=" language-json">
        {
          "xdm:birthDate": {
              "title": "Fecha de nacimiento",
              "type": "string",
              "formato": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Fecha de nacimiento",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Año de nacimiento",
              "type": "integer",
              "mínimo": 1,
              "máximo": 32767
        }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
        {
          "birthDate": {
              "title": "Fecha de nacimiento",
              "type": "string",
              "formato": "date",
              "meta:xdmField": "xdm:birthDate",
              "meta:xdmType": "date"
          },
          "birthDayAndMonth": {
              "title": "Fecha de nacimiento",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField": "xdm:birthDayAndMonth",
              "meta:xdmType": "string"
          },
          "birthYear": {
              "title": "Año de nacimiento",
              "type": "integer",
              "mínimo": 1,
              "máximo": 32767,
              "meta:xdmField": "xdm:birthYear",
              "meta:xdmType": "short"
        }
      </pre>
  </td>
  </tr>
</table>

### ¿Por qué es necesario el modo de compatibilidad?

Adobe Experience Platform está diseñado para trabajar con múltiples soluciones y servicios, cada uno con sus propios desafíos y limitaciones técnicos (por ejemplo, cómo ciertas tecnologías manejan caracteres especiales). Para superar estas limitaciones, se desarrolló el Modo de compatibilidad.

La mayoría de los [!DNL Experience Platform] servicios, incluidos [!DNL Catalog], [!DNL Data Lake] y [!DNL Real-time Customer Profile], utilizan [!DNL Compatibility Mode] en lugar del XDM estándar. La API [!DNL Schema Registry] también utiliza [!DNL Compatibility Mode] y los ejemplos de este documento se muestran utilizando [!DNL Compatibility Mode].

Vale la pena saber que se realiza una asignación entre el XDM estándar y la forma en que se realiza en [!DNL Experience Platform], pero no debería afectar al uso de los servicios [!DNL Platform].

El proyecto de código abierto está disponible para usted, pero cuando se trata de interactuar con los recursos a través de [!DNL Schema Registry], los ejemplos de API de este documento proporcionan las prácticas recomendadas que debe conocer y seguir.
