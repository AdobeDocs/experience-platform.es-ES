---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;compatibilidad;modo de compatibilidad;modo de compatibilidad;tipo de campo;tipos de campo;
solution: Experience Platform
title: Apéndice de la Guía de API de Registro de esquemas
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de Registro de esquemas.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# Apéndice de la guía de API de Registro de esquemas

Este documento proporciona información complementaria relacionada con el trabajo con [!DNL Schema Registry] API.

## Uso de parámetros de consulta {#query}

El [!DNL Schema Registry] admite el uso de parámetros de consulta para paginar y filtrar los resultados al enumerar recursos.

>[!NOTE]
>
>Al combinar varios parámetros de consulta, deben separarse con el símbolo et (`&`).

### Paginación {#paging}

Los parámetros de consulta más comunes para la paginación incluyen:

| Parámetro | Descripción |
| --- | --- |
| `orderby` | Ordene los resultados por una propiedad específica. Ejemplo: `orderby=title` ordenará los resultados por título en orden ascendente (A-Z). Adición de un `-` antes del valor del parámetro (`orderby=-title`) ordenará los elementos por título en orden descendente (Z-A). |
| `limit` | Cuando se usa junto con un `orderby` parámetro, `limit` restringe el número máximo de elementos que deben devolverse para una solicitud determinada. Este parámetro no se puede utilizar sin un `orderby` parámetro presente.<br><br>El `limit` parámetro especifica un entero positivo (entre `0` y `500`) as a *indicio* en cuanto al número máximo de elementos que deben devolverse. Por ejemplo, `limit=5` devuelve solo cinco recursos de la lista. Sin embargo, este valor no se respeta estrictamente. El tamaño de respuesta real puede ser menor o mayor, ya que está limitado por la necesidad de proporcionar un funcionamiento fiable del `start` parámetro, si se proporciona uno. |
| `start` | Cuando se usa junto con un `orderby` parámetro, `start` especifica dónde debe comenzar la lista de elementos subconfigurada. Este parámetro no se puede utilizar sin un `orderby` parámetro presente. Este valor se puede obtener del `_page.next` de una respuesta de lista y se utiliza para acceder a la siguiente página de resultados. Si la variable `_page.next` el valor es nulo, por lo que no hay ninguna página adicional disponible.<br><br>Normalmente, este parámetro se omite para obtener la primera página de resultados. Después de eso, `start` debe establecerse en el valor máximo de la propiedad de ordenación principal de la variable `orderby` campo recibido en la página anterior. A continuación, la respuesta de la API devuelve entradas que comienzan por las que tienen una propiedad de ordenación principal de `orderby` estrictamente mayor que (para ascendente) o estrictamente menor que (para descendente) el valor especificado.<br><br>Por ejemplo, si la variable `orderby` El parámetro se ha establecido en `orderby=name,firstname`, el `start` contendría un valor para el parámetro `name` propiedad. En este caso, si desea mostrar las 20 entradas siguientes de un recurso inmediatamente después del nombre &quot;Miller&quot;, debe utilizar: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filtro {#filtering}

Puede filtrar los resultados utilizando la variable `property` , que se utiliza para aplicar un operador específico a una propiedad JSON determinada dentro de los recursos recuperados. Los operadores admitidos son:

| Operador | Descripción | Ejemplo |
| --- | --- | --- |
| `==` | Filtra por si la propiedad es igual al valor proporcionado. | `property=title==test` |
| `!=` | Filtra por si la propiedad no es igual al valor proporcionado. | `property=title!=test` |
| `<` | Filtra por si la propiedad es menor que el valor proporcionado. | `property=version<5` |
| `>` | Filtra por si la propiedad es mayor que el valor proporcionado. | `property=version>5` |
| `<=` | Filtra por si la propiedad es menor o igual que el valor proporcionado. | `property=version<=5` |
| `>=` | Filtra por si la propiedad es mayor o igual que el valor proporcionado. | `property=version>=5` |
| (Ninguna) | Si se indica solo el nombre de la propiedad, solo se devuelven entradas donde exista la propiedad. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>Puede usar el complemento `property` para filtrar grupos de campos de esquema por su clase compatible. Por ejemplo, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` devuelve solo los grupos de campos compatibles con [!DNL XDM Individual Profile] clase.

## Modo de compatibilidad {#compatibility}

[!DNL Experience Data Model] (XDM) es una especificación documentada públicamente, impulsada por el Adobe de mejorar la interoperabilidad, la expresividad y la potencia de las experiencias digitales. El Adobe mantiene el código fuente y las definiciones XDM formales en una [proyecto de código abierto en GitHub](https://github.com/adobe/xdm/). Estas definiciones se escriben en notación estándar XDM, utilizando JSON-LD (notación de objetos JavaScript para datos vinculados) y esquema JSON como gramática para definir esquemas XDM.

Al consultar las definiciones de XDM formales en el repositorio público, puede ver que el XDM estándar difiere de lo que se ve en Adobe Experience Platform. Lo que está viendo en [!DNL Experience Platform] se denomina Modo de compatibilidad y proporciona una asignación sencilla entre XDM estándar y la forma en que se utiliza dentro de [!DNL Platform].

### Funcionamiento del modo de compatibilidad

El modo de compatibilidad permite que el modelo XDM JSON-LD funcione con una infraestructura de datos existente alterando los valores dentro del XDM estándar y manteniendo la semántica igual. Utiliza una estructura JSON anidada, que muestra los esquemas en un formato de árbol.

La principal diferencia entre el XDM estándar y el modo de compatibilidad es la eliminación del prefijo &quot;xdm:&quot; para los nombres de campo.

A continuación se muestra una comparación en paralelo que muestra campos relacionados con el cumpleaños (con atributos de &quot;descripción&quot; eliminados) tanto en el XDM estándar como en el modo de compatibilidad. Observe que los campos Modo de compatibilidad incluyen una referencia al campo XDM y su tipo de datos en los atributos &quot;meta:xdmField&quot; y &quot;meta:xdmType&quot;.

<table style="table-layout:auto">
  <th>XDM estándar</th>
  <th>Modo de compatibilidad</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate": { "title": "Fecha de nacimiento", "type": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:birthYear": { "title": "Birth year", "type": "integer", "minimum": 1, "maximum": 32767 } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate": { "title": "Fecha de nacimiento", "type": "string", "format": "date", "meta:xdmField": "xdm:birthDate", "meta:xdmType": "date" }, "birthDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9]", "meta:xdmField": "xdm m:birthDayAndMonth", "meta:xdmType": "string" }, "birthYear": { "title": "Birth year", "type": "integer", "minimum": 1, "maximum": 32767, "meta:xdmField": "xdm:birthYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### ¿Por qué es necesario el modo de compatibilidad?

Adobe Experience Platform está diseñado para trabajar con varias soluciones y servicios, cada uno con sus propios desafíos y limitaciones técnicas (por ejemplo, cómo gestionan ciertas tecnologías los caracteres especiales). Para superar estas limitaciones, se desarrolló el Modo de compatibilidad.

Más [!DNL Experience Platform] servicios que incluyen [!DNL Catalog], [!DNL Data Lake], y [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] en lugar del XDM estándar. El [!DNL Schema Registry] La API también utiliza [!DNL Compatibility Mode]y los ejemplos de este documento se muestran utilizando [!DNL Compatibility Mode].

Vale la pena saber que se produce una asignación entre el XDM estándar y la forma en que se opera en [!DNL Experience Platform], pero no debería afectar a su uso de [!DNL Platform] servicios.

El proyecto de código abierto está disponible, pero cuando se trata de interactuar con recursos a través de [!DNL Schema Registry]Sin embargo, los ejemplos de API de este documento proporcionan las prácticas recomendadas que debe conocer y seguir.
