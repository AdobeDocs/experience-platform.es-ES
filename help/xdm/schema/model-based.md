---
keywords: Experience Platform;inicio;temas populares;esquema basado en modelo;esquema relacional;esquemas relacionales;esquema;xdm;modelo de datos de experiencia;
solution: Experience Platform
title: Esquemas basados en modelos
description: Obtenga información acerca de los esquemas basados en modelos (también denominados esquemas relacionales) en Adobe Experience Platform, incluidas las funciones, los campos obligatorios, las relaciones y las limitaciones.
badge: Disponibilidad limitada
source-git-commit: 192e97c97ffcb2d695bcfa6269cc6920f5440832
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 0%

---

# Esquemas basados en modelos

>[!AVAILABILITY]
>
>Data Mirror y los esquemas basados en modelos están disponibles para los titulares de licencias de **campañas orquestadas** de Adobe Journey Optimizer. También están disponibles como una **versión limitada** para los usuarios de Customer Journey Analytics, según su licencia y la habilitación de características. Póngase en contacto con su representante de Adobe para obtener acceso.

Los esquemas basados en modelos proporcionan un patrón de modelado flexible y controlado para representar datos estructurados en el lago de datos de Adobe Experience Platform. Admiten claves principales forzadas, relaciones a nivel de esquema y un control preciso de los registros, todo sin depender de esquemas de unión ni de sistemas de base de datos relacionales completos.

>[!IMPORTANT]
>
>Las consideraciones de eliminación de datos se aplican a todas las implementaciones de esquema basadas en modelos. Las aplicaciones que utilizan estos esquemas deben comprender cómo las eliminaciones afectan a los conjuntos de datos relacionados, los requisitos de cumplimiento y los procesos descendentes. Planifique escenarios de eliminación y revise las [directrices de higiene de los datos](../../hygiene/ui/record-delete.md#model-based-record-delete) antes de la implementación.

>[!NOTE]
>
>Las aplicaciones pueden hacer referencia a los esquemas basados en modelos como &quot;esquemas relacionales&quot; al solicitar la creación de esquemas para casos de uso de modelado de datos relacionales.

Utilice esquemas basados en modelos para lo siguiente:

* Garantice la integridad de los datos con claves principales compuestas o de un solo campo obligatorio.
* Habilite un seguimiento de cambios preciso mediante el control de versiones para inserciones, actualizaciones y eliminaciones.
* Defina relaciones de nivel de esquema reutilizables para modelar conexiones de entidad del mundo real.
* Evite duplicar estructuras de esquema entre aplicaciones al admitir varios modelos de datos.
* Omitir restricciones de esquema de unión para optimizar la incorporación, reducir la sobrecarga de esquema y evitar cambios de esquema no deseados.

## Cómo difieren los esquemas basados en modelos de los esquemas XDM estándar

Los esquemas XDM estándar en Experience Platform siguen uno de los tres comportamientos de datos: registro, serie temporal o ad hoc. Para ver definiciones y detalles, consulte [comportamientos de datos XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

En el modelo tradicional, los esquemas de registros y series temporales participan en [esquemas de unión](../api/unions.md) (consulte también la [guía de la interfaz de usuario del esquema de unión](../../profile/ui/union-schema.md)). Estos esquemas evolucionan automáticamente a medida que se actualizan [grupos de campos](./composition.md#field-group) compartidos y los campos personalizados deben anidarse en un área de nombres de inquilino. Aunque es potente, este modelo puede ralentizar la incorporación, producir esquemas demasiado complejos con campos no utilizados y requerir una asignación o transformación de datos adicional. Estos factores aumentan la curva de aprendizaje y el esfuerzo de mantenimiento continuo.

Los esquemas basados en modelos eliminan las dependencias de esquema de unión, lo que elimina las actualizaciones automáticas de los grupos de campos compartidos y permite definiciones de campo directas sin restricciones de área de nombres de inquilino. Puede obtener un control explícito sobre las claves principales, las relaciones y el diseño inicial del esquema, lo que facilita la creación de modelos de datos que se ajusten a sus necesidades en el momento de la creación.

## Características de los esquemas basados en modelos

Utilice las siguientes capacidades para modelar datos estructurados en el lago de datos a la vez que mantiene la gobernanza, la integridad y la interoperabilidad.

* **Compatibilidad con el comportamiento de esquema**: Configure con:
   * **Registrar comportamiento**: Registra el estado actual de una entidad, como un cliente, una cuenta o una campaña.
   * **Comportamiento de series de tiempo**: captura eventos y la hora en que ocurren, lo cual resulta útil para rastrear secuencias o cambios a lo largo del tiempo.
* **Aplicación de clave principal**: defina una clave principal para identificar de forma exclusiva cada registro y evitar duplicados durante la ingesta.
* **Control de versiones**: use un **identificador de versión** (un descriptor) para asegurarse de que las actualizaciones se aplican en el orden correcto, incluso si los registros llegan fuera de secuencia.
* **Asignación de relaciones**: cree relaciones uno a uno o varios a uno entre esquemas basados en modelos o entre esquemas basados en modelos y esquemas estándar. Las definiciones de relaciones se almacenan como descriptores para permitir uniones eficientes.
* **Evolución simplificada**: los esquemas basados en modelos no participan en vistas de unión y no se actualizan cuando cambian los grupos de campos compartidos, lo que evita cambios descendentes inesperados.
* **Definición de campo flexible**: agregue campos directamente sin espaciado de nombres de id de inquilino. Los esquemas basados en modelos no admiten grupos de campos XDM.
* **Sin dependencia en esquemas de unión**: mejora el rendimiento de la consulta y reduce la sobrecarga operativa de la administración de vistas de esquema globales.
* **Ordenación del tiempo del evento**: Para los esquemas de series temporales, use un **identificador de marca de tiempo** para ordenar los eventos por hora de ocurrencia en lugar del tiempo de ingesta.

## Campos requeridos

Los esquemas basados en modelos requieren ciertos descriptores: metadatos en la definición del esquema que controla comportamientos y restricciones clave. Agregue los siguientes descriptores como parte de su definición de esquema.

### Descriptor de clave principal

Utilice un descriptor de clave principal para asegurarse de que cada registro se pueda identificar de forma exclusiva. Las configuraciones admitidas son:

* **Clave principal de un solo campo**: Utilice un campo con un valor único para cada registro.
* **Clave principal compuesta**: utilice varios campos para formar un identificador único. Para los esquemas de series temporales, la clave compuesta debe incluir el campo de marca de tiempo identificado por el descriptor de marca de tiempo.

>[!NOTE]
>
>En el Editor de esquemas de interfaz de usuario, el descriptor de versión y los descriptores de marca de tiempo aparecen como &quot;[ !UICOTRNOL Identificador de versión]&quot; y &quot;[ !UICOTRNOL Identificador de marca de tiempo]&quot; respectivamente.

**Ejemplo (un solo campo):**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Ejemplo (compuesto para series temporales)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Descriptor de la versión (identificador)

Defina un descriptor de versión (identificador) para mantener el estado de registro correcto y garantizar que se aplique la actualización más reciente. Cuando varios registros comparten la misma clave principal, el registro con el valor de versión más alto se considera el más reciente.

**Ejemplo:**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Descriptor de marca de tiempo (identificador)

Para los esquemas de series temporales, defina un descriptor de marca de tiempo (identificador) para establecer la hora del evento para la ordenación.

**Ejemplo:**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Los descriptores forman parte de los metadatos de la definición del esquema y no se almacenan en filas de datos.

Para obtener instrucciones sobre cómo crear descriptores en el Editor de esquemas, vea [Crear descriptores en el Editor de esquemas](../tutorials/relationship-ui.md). Para la creación basada en API, consulte [Crear descriptores mediante la API](../tutorials/relationship-api.md).

## Compatibilidad con relaciones {#relationship-support}

El modelado de datos relacionales es un uso principal de los esquemas basados en modelos. Los casos de uso de la aplicación incluso pueden hacer referencia a estos esquemas como &quot;esquemas relacionales&quot;. Los descriptores de relación habilitan estas conexiones vinculando conjuntos de datos entre esquemas sin incrustar claves externas en filas de datos. Mejoran la integridad referencial, habilitan patrones de modelado reutilizables y admiten consultas conectadas entre aplicaciones.

Cree descriptores de relación en el nivel de esquema para la resolución dinámica en el momento de la consulta. Los valores de cardinalidad (1:1, varios a uno) proporcionan orientación, pero no aplican restricciones durante la ingesta, lo que admite el modelado de datos flexible en conjuntos de datos conectados.

Antes de agregar descriptores de relación, determine el tipo y el destino adecuados:

* **Uno a uno**: cada registro del esquema de origen corresponde a un registro como máximo del esquema de destino.
* **Varios a uno**: varios registros en el esquema de origen pueden hacer referencia al mismo registro en el esquema de destino.

>[!NOTE]
>
>Puede definir relaciones entre dos esquemas basados en modelos o entre un esquema basado en modelos y un esquema estándar. No se admiten relaciones con esquemas ad hoc.

<!-- Q) 
Madeline commented: "model-based schema to standard might only be offered for b2b customers; that's how it will be on the UI" - is that still accurate? -->

**Ejemplo: relación uno a uno**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

<!-- Q) 
Should these be `@type: "xdm:descriptorRelationship",` This could be a copy-pasting error? -->

**Ejemplo: relación de varios a uno**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Para obtener una lista de tipos de descriptor de relación y sintaxis, consulte la [referencia de API de descriptores](../api/descriptors.md). Para aprender a aplicar estos conceptos en la práctica, siga los tutoriales para [definir una relación en la API](../tutorials/relationship-api.md) o [crear una relación en la interfaz de usuario](../tutorials/relationship-ui.md).

>[!NOTE]
>
>A medida que las relaciones se definen en el nivel de esquema, asegúrese de unir explícitamente los conjuntos de datos relacionados en las consultas. Utilice una herramienta como Data Distiller para resolver estas relaciones durante la consulta.

>[!IMPORTANT]
>
>La cardinalidad de la relación es informativa y no se aplica durante la ingesta. Solo se aplica cuando se resuelven relaciones durante una consulta o análisis. No confíe en la configuración de cardinalidad para validar los datos durante la ingesta. Compruebe y limpie los datos usted mismo, y asegúrese de que las reglas de relación definidas coinciden con la forma en que desea consultar o analizar los datos.

>[!NOTE]
>
> Los esquemas basados en modelos pueden vincularse a esquemas estándar, pero no a esquemas ad hoc.

## Consideraciones de higiene y eliminación de datos {#data-hygiene-support}

Los esquemas basados en modelos permiten eliminaciones precisas a nivel de registro que tienen implicaciones universales para todas las aplicaciones y casos de uso. Los descriptores de clave principal, versión y marca de tiempo proporcionan la base para una identificación precisa de los registros durante las operaciones de eliminación.

### Impactos de eliminación universales

Todas las aplicaciones que utilizan esquemas basados en modelos deben tener en cuenta:

* **Integridad referencial**: las eliminaciones pueden afectar los registros relacionados entre conjuntos de datos conectados
* **Requisitos de cumplimiento**: algunos sectores requieren comportamientos de eliminación y pistas de auditoría específicos
* **Comportamiento de la aplicación**: Es posible que los sistemas descendentes tengan que gestionar correctamente los eventos de eliminación
* **Coherencia de datos**: los conjuntos de datos relacionados deben mantener la coherencia durante las operaciones de eliminación
* **Planificación de eliminación**: tenga en cuenta los impactos descendentes en todos los conjuntos de datos y aplicaciones conectados durante la fase de diseño

Para obtener instrucciones de implementación, consulte [Eliminación de registros de conjuntos de datos basados en modelos](../../hygiene/ui/record-delete.md#model-based-record-delete).

## Limitaciones y consideraciones {#limitations}

Revise las siguientes limitaciones antes de utilizar esquemas basados en modelos:

* Los esquemas basados en modelos no participan en esquemas de unión.
* La evolución del esquema es manual; no se actualizan automáticamente cuando cambian los grupos de campos.

>[!IMPORTANT]
>
>La evolución del esquema se restringe después de que se inicialice un conjunto de datos con el esquema. Planifique los nombres y tipos de los campos con cuidado de antemano, ya que una vez introducidos los datos, los campos no se pueden eliminar ni modificar.

* Las relaciones se limitan a uno a uno y a varios a uno.
* La disponibilidad depende de la licencia o de la habilitación de funciones.
* Las claves principales compuestas son necesarias para los esquemas de series temporales.

