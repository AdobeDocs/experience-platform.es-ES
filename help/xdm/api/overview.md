---
keywords: Experience Platform;inicio;temas populares;api;API;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;Registro de esquemas;
solution: Experience Platform
title: Guía de API de Registro de esquemas
description: La API de Registro de esquemas permite a los desarrolladores administrar mediante programación todos los esquemas y los recursos del Modelo de datos de experiencia (XDM) relacionados dentro de Adobe Experience Platform. Siga esta guía para aprender a realizar operaciones clave con la API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 3dffa9687f3429b970e8fceebd6864a5b61ead21
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 5%

---

# Guía de la API de [!DNL Schema Registry]

El [!DNL Schema Registry] se utiliza para acceder a la biblioteca de esquemas en Adobe Experience Platform, proporcionando una interfaz de usuario y una API RESTful desde la cual se puede acceder a todos los recursos de biblioteca disponibles.

La API de Registro de esquemas proporciona varios extremos que le permiten administrar mediante programación todos los esquemas y los recursos del Modelo de datos de experiencia (XDM) relacionados disponibles en Platform. Esto incluye los definidos por el Adobe, [!DNL Experience Platform] socios y proveedores cuyas aplicaciones utilice.

Estos extremos se describen a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

>[!IMPORTANT]
>
>XDM utiliza el formato de esquema JSON para describir y validar la estructura de los datos de experiencia del cliente introducidos. Antes de trabajar con la API de Registro de esquemas, se recomienda encarecidamente que revise la [Documentación oficial del esquema JSON](https://json-schema.org/) para comprender mejor esta tecnología subyacente.

Para ver todos los extremos disponibles y las operaciones de CRUD, visite la [Referencia de API del Registro de esquemas](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Esquemas

Los esquemas XDM representan y validan la estructura y el formato de los datos introducidos en Platform. Un esquema está compuesto por una clase y cero o más grupos de campos de esquema. Puede crear, ver, editar y eliminar esquemas utilizando `/schemas` punto final. Para obtener información sobre cómo utilizar este extremo, consulte la [guía de extremo de esquemas](./schemas.md).

Para obtener una guía paso a paso sobre cómo crear manualmente un esquema completo en la API de Registro de esquemas, incluida la creación y adición de grupos de campos y tipos de datos, consulte la [Tutorial de creación de esquemas de API](../tutorials/create-schema-api.md).

Si está introduciendo datos CSV, consulte la sección sobre [Conversión de CSV a esquema](#csv-to-schema).

## Comportamientos

Los comportamientos definen la naturaleza de los datos que describe un esquema. Cada clase XDM debe hacer referencia a un comportamiento específico, que heredarán todos los esquemas que emplean esa clase. Consulte la [guía de extremo de comportamientos](./behaviors.md) para obtener información sobre cómo ver los comportamientos disponibles en la API.

## Clases

Una clase define la estructura base de propiedades comunes que deben contener todos los esquemas basados en esa clase y determina qué grupos de campos pueden utilizarse en esos esquemas. Cada clase debe asociarse con un comportamiento existente. Consulte la [guía de extremo de clases](./classes.md) para obtener más información sobre cómo trabajar con clases en la API.

## Grupos de campo

Los grupos de campos son componentes reutilizables que definen uno o varios campos que representan un concepto determinado, como una persona individual, una dirección de correo o un entorno de explorador web. Los grupos de campos están pensados para incluirse como parte de un esquema que implementa una clase compatible, según el comportamiento de los datos que representan (registro o serie temporal). Consulte la [guía de extremo de grupos de campos](./field-groups.md) para aprender a trabajar con grupos de campos en la API.

## Tipos de datos

Los tipos de datos se utilizan como campos de tipo de referencia en clases o grupos de campos de la misma manera que los campos literales básicos, con la diferencia clave de que los tipos de datos pueden definir varios subcampos. Aunque son similares a los grupos de campos en el sentido de que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque se pueden incluir en cualquier parte de la estructura del esquema, mientras que los grupos de campos solo se pueden añadir en el nivel raíz. Consulte la [guía de extremo de tipos de datos](./data-types.md) para obtener más información sobre cómo trabajar con tipos de datos en la API.

## Descriptores

Los descriptores son conjuntos de metadatos que se asignan a campos específicos dentro de un esquema, lo que proporciona varios detalles contextuales, incluido cómo esos campos (y el propio esquema) están relacionados con otros esquemas. Cada esquema puede tener una o más entidades de descriptor aplicadas y hay varios tipos de descriptor diferentes para servir diferentes propósitos. Consulte la [guía de extremo de descriptores](./descriptors.md) para obtener más información sobre cómo trabajar con descriptores en la API y una visión general de los diferentes tipos de descriptor y sus casos de uso.

## Uniones

Aunque Platform le permite componer esquemas para casos de uso específicos, también le permite componer una &quot;unión&quot; de esquemas pertenecientes a una clase específica. Un esquema de unión agrega los campos de todos los esquemas que comparten la misma clase en una sola representación. Al habilitar un esquema para su uso con [Perfil del cliente en tiempo real](../../profile/home.md), ese esquema se incluye en la unión para su clase particular. Como tal, los esquemas de unión no se pueden editar directamente y solo se pueden ver afectados por la inclusión o exclusión de esquemas para su uso en el perfil.

Para obtener información sobre cómo ver uniones en la API de Registro de esquemas, consulte la [guía de extremo de union](./unions.md).

## Conversión de CSV a esquema {#csv-to-schema}

Puede generar automáticamente un esquema XDM utilizando un archivo CSV como plantilla, lo que le permite crear plantillas para importar campos de esquema por lotes y reducir el trabajo manual de la API o la IU.

Consulte la [Guía de extremo de conversión de CSV a esquema](./export.md) para obtener más información.

>[!NOTE]
>
>También puede utilizar la interfaz de usuario para lo siguiente: [asignar un CSV a un esquema mediante recomendaciones generadas por IA](../../ingestion/tutorials/map-csv/recommendations.md) (actualmente en fase beta).

## Exportar {#export}

La API de Registro de esquemas permite transferir y compartir recursos XDM entre entornos limitados y organizaciones IMS. Para cualquier esquema, grupo de campos o tipo de datos, se puede generar una carga útil de exportación que contenga la estructura del recurso y cualquier recurso dependiente. Esta carga útil se puede utilizar para importar el recurso en una zona protegida de destino y una organización de IMS.

Consulte la [guía de extremo de exportación](./export.md) para obtener más información sobre cómo crear una carga útil de exportación para un recurso XDM existente.

## Importar

Si usa el [exportar](#export) o [Conversión de CSV a esquema](./import.md) extremos Para crear una carga útil de exportación, puede enviar esa carga útil a una organización de destino y a una zona protegida para importar los recursos especificados.

Consulte la [guía de importar extremo](./export.md) para obtener más información sobre cómo generar recursos XDM a partir de cargas útiles de exportación.

## Datos de muestra

Puede generar datos de ejemplo para cualquier esquema especificado en la Biblioteca de esquemas. El objeto de respuesta devuelto se puede utilizar como fuente de ingesta de datos.

Consulte la [guía de extremo de datos de ejemplo](./sample-data.md) para obtener más información sobre el uso de este extremo.

## Registro de auditoría

El Registro de esquemas mantiene un registro de todos los cambios que se han producido en un recurso (clase, grupo de campos, tipo de datos o esquema) entre diferentes actualizaciones. Puede recuperar el registro de un recurso concreto proporcionando su `$id` o `meta:altId` en la ruta de una solicitud de GET a este extremo.

Consulte la [guía de extremo de registro de auditoría](./audit-log.md) para obtener más información sobre el uso de este extremo.

## Pasos siguientes

Para empezar a realizar llamadas mediante la API de Registro de esquemas, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de extremos para aprender a utilizar extremos específicos.
