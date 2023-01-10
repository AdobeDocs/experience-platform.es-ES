---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;compatibilidad;modo de compatibilidad;modo de compatibilidad;tipo de campo;tipos de campo
solution: Experience Platform
title: Apéndice de la API del Registro de Esquemas
description: Este documento proporciona información complementaria relacionada con el trabajo con la API del Registro de esquemas.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# Apéndice de la guía de API del Registro de Esquemas

Este documento proporciona información complementaria relacionada con el trabajo con la variable [!DNL Schema Registry] API.

## Uso de parámetros de consulta {#query}

La variable [!DNL Schema Registry] admite el uso de parámetros de consulta en los resultados de filtro y página al enumerar recursos.

>[!NOTE]
>
>Cuando se combinan varios parámetros de consulta, deben separarse con el símbolo &amp; (`&`).

### Paginación {#paging}

Los parámetros de consulta más comunes para la paginación incluyen:

| Parámetro | Descripción |
| --- | --- |
| `orderby` | Ordene los resultados por una propiedad específica. Ejemplo: `orderby=title` ordenará los resultados por título en orden ascendente (A-Z). Adición de un `-` antes del valor del parámetro (`orderby=-title`) ordenará los elementos por título en orden descendente (Z-A). |
| `limit` | Cuando se usa junto con un `orderby` parámetro, `limit` restringe el número máximo de elementos que deben devolverse para una solicitud determinada. Este parámetro no se puede usar sin un `orderby` presente.<br><br>La variable `limit` especifica un entero positivo (entre `0` y `500`) como un *sugerencia* en cuanto al número máximo de elementos que deben devolverse. Por ejemplo, `limit=5` devuelve solo cinco recursos en la lista. Sin embargo, este valor no se respeta estrictamente. El tamaño real de la respuesta puede ser menor o mayor, ya que está limitado por la necesidad de proporcionar el funcionamiento fiable de la variable `start` , si se proporciona uno. |
| `start` | Cuando se usa junto con un `orderby` parámetro, `start` especifica dónde debe comenzar la lista de elementos de la subconfiguración. Este parámetro no se puede usar sin un `orderby` presente. Este valor se puede obtener de la variable `_page.next` de una respuesta de lista y se utiliza para acceder a la siguiente página de resultados. Si la variable `_page.next` es nulo y no hay ninguna página adicional disponible.<br><br>Normalmente, este parámetro se omite para obtener la primera página de resultados. Después de eso, `start` debe establecerse en el valor máximo de la propiedad de ordenación principal de la variable `orderby` campo recibido en la página anterior. A continuación, la respuesta de API devuelve entradas que comienzan con las que tienen una propiedad de ordenación principal de `orderby` estrictamente bueno (para ascendente) o estrictamente menor que (para descendente) el valor especificado.<br><br>Por ejemplo, si la variable `orderby` se establece en `orderby=name,firstname`, el `start` contendría un valor para `name` propiedad. En este caso, si desea mostrar las 20 entradas siguientes de un recurso inmediatamente después del nombre &quot;Miller&quot;, debe utilizar: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtro {#filtering}

Puede filtrar los resultados utilizando la variable `property` , que se utiliza para aplicar un operador específico a una propiedad JSON determinada dentro de los recursos recuperados. Los operadores admitidos son:

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
>Puede usar la variable `property` para filtrar grupos de campos de esquema por su clase compatible. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` solo devuelve grupos de campos compatibles con la variable [!DNL XDM Individual Profile] Clase .

## Modo de compatibilidad {#compatibility}

[!DNL Experience Data Model] (XDM) es una especificación públicamente documentada, impulsada por el Adobe para mejorar la interoperabilidad, la expresividad y el poder de las experiencias digitales. Adobe mantiene el código fuente y las definiciones XDM formales en un [proyecto de código abierto en GitHub](https://github.com/adobe/xdm/). Estas definiciones se escriben en la Notación estándar XDM, utilizando JSON-LD (Notación de objetos JavaScript para datos vinculados) y Esquema JSON como gramática para definir esquemas XDM.

Al consultar las definiciones formales de XDM en el repositorio público, puede ver que el XDM estándar difiere de lo que ve en Adobe Experience Platform. Qué está viendo en [!DNL Experience Platform] se denomina Modo de compatibilidad y proporciona una asignación sencilla entre el XDM estándar y la forma en que se utiliza en [!DNL Platform].

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
{ "xdm:birthDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "cadena", "patrón": "[0-1][0-9]-[0-9][0-9]" }, "xdm:birthYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767 } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate": { "title": "Fecha de nacimiento", "tipo": "string", "format": "date", "meta:xdmField": "xdm:birthDate", "meta:xdmType": "date" }, "birthDayAndMonth": { "title": "Fecha de nacimiento", "tipo": "cadena", "patrón": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:birthDayAndMonth", "meta:xdmType": "string" }, "birthYear": { "title": "Año de nacimiento", "tipo": "integer", "Minimum": 1, "máximo": 32767, "meta:xdmField": "xdm:birthYear", "meta:xdmType": "short" } }
      </pre>
  </td>
  </tr>
</table>

### ¿Por qué es necesario el modo de compatibilidad?

Adobe Experience Platform está diseñado para trabajar con múltiples soluciones y servicios, cada uno con sus propios desafíos y limitaciones técnicos (por ejemplo, cómo ciertas tecnologías manejan caracteres especiales). Para superar estas limitaciones, se desarrolló el Modo de compatibilidad.

Más [!DNL Experience Platform] servicios incluidos [!DNL Catalog], [!DNL Data Lake]y [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] en lugar del XDM estándar. La variable [!DNL Schema Registry] La API también utiliza [!DNL Compatibility Mode], y los ejemplos de este documento se muestran utilizando [!DNL Compatibility Mode].

Vale la pena saber que se realiza una asignación entre el XDM estándar y la forma en que se opera en [!DNL Experience Platform], pero no debe afectar a su uso de [!DNL Platform] servicios.

El proyecto de código abierto está disponible para usted, pero cuando se trata de interactuar con los recursos a través del [!DNL Schema Registry], los ejemplos de API de este documento proporcionan las prácticas recomendadas que debe conocer y seguir.
