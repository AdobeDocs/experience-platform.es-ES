---
title: Permisos de usuario para etiquetas
description: Obtenga información sobre los distintos tipos de permisos disponibles para etiquetas y algunas estrategias de implementación básicas para diferentes casos de uso empresarial.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 22%

---

# Permisos de usuario para etiquetas

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Los permisos de usuario para etiquetas en Adobe Experience Platform se asignan a usuarios a través de Adobe Admin Console. En lugar de asignarse a usuarios individuales, los distintos conjuntos de permisos se configuran por separado como perfiles de producto. A continuación, se asignan los usuarios a estos perfiles de producto para que se les concedan los permisos para los que se han configurado.

Esta guía proporciona información general sobre los diferentes tipos de permisos disponibles para etiquetas, las funcionalidades a las que conceden acceso y algunas estrategias de implementación básicas para diferentes casos de uso empresarial.

>[!NOTE]
>
>Para ver los pasos sobre cómo configurar los permisos para los usuarios que utilizan Admin Console, consulte el tutorial en [administración de permisos para la recopilación de datos](../../../collection/permissions.md).

## Tipos de permiso

Dentro de un perfil de producto, los permisos para etiquetas se dividen en cuatro categorías:

1. Plataformas
1. Propiedades
1. Derechos de propiedad
1. Derechos de compañía

### Plataformas

Cada propiedad de etiqueta tiene una plataforma. Actualmente hay dos plataformas que puede utilizar para etiquetas: web y móvil. Puede utilizar este tipo de permiso para restringir o conceder acceso a un tipo concreto de propiedad. Esto puede resultar útil cuando el equipo que administra las aplicaciones móviles es diferente del que administra los sitios web.

### Propiedades

De forma predeterminada, los perfiles de producto otorgan acceso a todas las propiedades que existen dentro de su empresa, tanto actualmente como en el futuro. Con este tipo de permiso, puede restringir o conceder acceso a propiedades existentes específicas por nombre.

### Derechos de propiedad {#property-rights}

Cualquier propiedad de etiqueta que cree en la interfaz de usuario estará disponible en Admin Console, lo que le permitirá agrupar la propiedad con derechos de propiedad específicos en el mismo perfil de producto.

Por ejemplo, si un perfil de producto determinado no tiene acceso a la Propiedad A1, los usuarios que pertenezcan a ese perfil no podrán ver ni modificar ninguna configuración de la Propiedad A1.

Si un usuario pertenece a un perfil que sí tiene acceso a la Propiedad A1, las acciones que puede realizar dentro de la Propiedad A1 están determinadas por los derechos otorgados desde este perfil. Si un usuario tiene permisos para la Propiedad A1 pero no tiene derechos asignados, tendrá acceso de solo lectura para esa propiedad.

La siguiente tabla describe los derechos de propiedad disponibles y las funcionalidades a las que conceden acceso:

| Propiedad | Descripción |
| --- | --- |
| **Desarrollo** | Esto le permite realizar las siguientes acciones:<ul><li>Creación de reglas y elementos de datos</li><li>Cree bibliotecas y créelas en entornos de desarrollo existentes</li><li>Enviar una biblioteca para su aprobación</li></ul>La mayoría de las tareas diarias de la interfaz de usuario requieren este derecho. |
| **Aprobar** | Esto le permite tomar una biblioteca enviada y crearla en el entorno de ensayo. También puede aprobar una biblioteca para publicarla una vez completada la prueba. |
| **Publicar** | Esto le permite publicar bibliotecas aprobadas en el entorno de producción. |
| **Administrar extensiones** | Esto le permite realizar las siguientes acciones: <ul><li>Instalar nuevas extensiones en una propiedad</li><li>Modificación de la configuración de una extensión ya instalada</li><li>Eliminación de una extensión</li></ul>Consulte la documentación de descripción general de las extensiones para obtener [más información sobre las extensiones](../managing-resources/extensions/overview.md). Esta función suele pertenecer a TI o Marketing, según su organización. |
| **Administrar entornos** | Esto le permite crear y modificar entornos. Consulte la [documentación de entornos](../publishing/environments.md) para obtener más información. Esta función pertenece normalmente al grupo de TI. |

{style=&quot;table-layout:auto&quot;}

### Derechos de compañía

Los derechos de compañía se aplican a permisos que abarcan varias propiedades. Estos se describen en el cuadro siguiente:

| Derecho de compañía | Descripción |
| --- | --- |
| **Administrar propiedades** | Esto le permite realizar las siguientes acciones:<ul><li>Crear nuevas propiedades</li><li>Modificar metadatos y configuraciones en el nivel de propiedad</li><li>Eliminar propiedades</li></ul>Normalmente esta función recae sobre los administradores. Consulte la [documentación de propiedades](companies-and-properties.md) para obtener más información. |
| **Desarrollo de extensiones** | Concede la capacidad de crear y modificar paquetes de extensión que son propiedad de la empresa, incluidas versiones privadas y solicitudes de lanzamiento público. |
| **Administrar configuraciones de aplicación** | Solo está disponible para si dispone de una licencia para Adobe Journey Optimizer u otra solución que conceda acceso a la mensajería push y en la aplicación móvil.  Esto permite administrar las aplicaciones que Experience Cloud conoce, así como las credenciales push necesarias para comunicarse con el servicio Firebase Cloud Messaging y el servicio de notificaciones push de Apple. |

{style=&quot;table-layout:auto&quot;}

## Permisos totales de usuario

El total de permisos de un usuario individual se determina por su pertenencia total a diferentes perfiles de producto. Si un usuario pertenece a varios perfiles de producto, los permisos de cada perfil se suman en lugar de multiplicarse.

Por ejemplo, el Perfil de producto A le otorga el derecho de desarrollo para la Propiedad 1. El Perfil de producto B le otorga el derecho de publicación para la Propiedad 2. En este caso, puede desarrollar en la propiedad 1 y publicar en la propiedad 2, pero no puede publicar en la propiedad 1 ni desarrollar en la propiedad 2 porque no se le han concedido derechos explícitos para hacerlo.

## Situaciones de derechos

Las distintas empresas tienen diferentes necesidades al crear nuevos perfiles de producto. Estas necesidades varían según el tamaño de la empresa, la estructura de la organización, el número de sitios, el número de personas involucradas en la administración de etiquetas, etc.

A continuación se presentan algunos escenarios comunes y un punto de partida recomendado para crear perfiles de producto y añadirlos a los usuarios.

### Encargado individual

Si dirige una compañía pequeña que tiene una persona a cargo de todo, conceda a este usuario permisos para todas las propiedades y asígneles todos los derechos enumerados arriba.

### Separación de tareas

Considere una situación en la que muchas personas de su organización participan en el etiquetado. Tiene un conjunto de personas (como un consultor externo) que crea reglas y elementos de datos, pero no desea que tengan acceso al entorno de producción. En este caso, debe asegurarse de que nadie se implemente en Producción excepto el equipo de TI.

Para lograr esto:

1. Cree una cuenta para sus consultores y asígneles únicamente el derecho de desarrollo.
1. El consultor desarrolla y prueba dentro de los límites establecidos.
1. Si el consultor desea una nueva extensión o está listo para ejecutarse, un representante de su organización (con los derechos adecuados) realiza esas acciones.

### Para compañías

Una compañía puede tener varias instalaciones divididas geográficamente, con equipos diferentes responsables de cada ubicación geográfica. Dentro de esos equipos, distintas personas se encargan de desarrollar y publicar.

Es similar a la “Separación de tareas” anterior, pero se organiza por áreas geográficas. Por ejemplo, puede crear un perfil &quot;Desarrollo&quot; y un perfil &quot;Publicación&quot; para Norteamérica y crear grupos &quot;Desarrollo&quot; y &quot;Publicación&quot; independientes para Europa.

## Funciones de ejemplo

La siguiente tabla proporciona algunos ejemplos de los tipos de funciones que podría tener en su organización y de los permisos que debe asignarles:

| Función | Descripción | Propiedades | Derechos de propiedad | Derechos de compañía |
| --- | --- | --- | --- | --- |
| Administrador | Quiere ver lo que está pasando en el sistema, pero no debería poder realizar ningún cambio. | Inclusión automática | (Ninguna) | (Ninguna) |
| Experto en marketing | Puede instalar extensiones y configurar nuevas etiquetas para propiedades existentes, pero no puede publicar en los entornos de ensayo o producción. | Inclusión automática | <ul><li>Desarrollo</li><li>Administrar extensiones</li></ul> | <ul><li>Administrar propiedades</li></ul> |
| Desarrollador de aplicaciones móviles | Es responsable de implementar soluciones de Adobe y de terceros dentro de una aplicación móvil nativa. | Inclusión automática | <ul><li>Desarrollo</li><li>Administrar extensiones</li></ul> | <li>Administrar propiedades</li><li>Administrar configuraciones de aplicación</li> |
| Equipo de TI | En realidad no modifica ninguna etiqueta, pero tiene control total sobre los entornos de ensayo y producción y qué incluye. | Inclusión automática | (Ninguna) | <ul><li>Aprobar</li><li>Publicar</li><li>Administrar entornos</li></ul> |
| Desarrollador de extensiones | Desarrolla extensiones y puede enviarlas para su aprobación, pero no puede publicarlas o agregarlas a propiedades existentes. | Inclusión automática | <ul><li>Desarrollo</li></ul> | <ul><li>Administrar propiedades</li><li>Desarrollo de extensiones</li></ul> |
| El superusuario | Lo hace todo. | Inclusión automática | <ul><li>Desarrollo</li><li>Aprobar</li><li>Publicar</li><li>Administrar extensiones</li><li>Administrar entornos</li></ul> | <ul><li>Administrar propiedades</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Este documento proporciona una descripción general de los permisos disponibles para las etiquetas en Experience Platform. Para ver los pasos sobre cómo configurar perfiles de producto para etiquetas en Adobe Admin Console, consulte la guía de [administración de permisos de usuario para la recopilación de datos](../../../collection/permissions.md).
