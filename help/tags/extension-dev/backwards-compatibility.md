---
title: Estándar de compatibilidad con versiones anteriores
description: Obtenga información sobre el estándar de compatibilidad con versiones anteriores en Adobe Experience Platform que garantiza que las versiones actualizadas de las extensiones de etiquetas sean compatibles con versiones anteriores.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 97%

---

# Estándar de compatibilidad con versiones anteriores

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las actualizaciones de una extensión de etiqueta en Adobe Experience Platform deben ser compatibles con versiones anteriores de la extensión. Esto significa que:

* Cualquier modificación de los componentes principales de las extensiones debe ser compatible con las versiones anteriores. Esto incluye la configuración de las extensiones, tipos de evento, tipos de condición, tipos de acciones, tipos de elementos de datos y módulos compartidos.
* Los componentes que un usuario ha creado con la versión de extensión anterior deben poder aprobar la validación con los esquemas que ofrece la versión más reciente.
* Un usuario de Adobe Experience Platform debe poder instalar una versión actualizada de la extensión y hacer que todo lo que haya hecho siga funcionando tal cual hasta que realice cambios deliberados.

## Cambios permitidos

Se permiten los siguientes tipos de cambios en la extensión:

1. Puede añadir nuevos componentes (tipos de evento, tipos de condición, etc.).
1. Puede añadir nuevos campos opcionales a la configuración de la extensión.
1. Puede cambiar los campos obligatorios a campos opcionales.

## Cambios prohibidos

No se permiten los siguientes tipos de cambios en la extensión:

1. No se puede cambiar el nombre a ningún componente.
1. No se puede quitar ningún componente.
1. No se puede quitar ningún campo de un componente.
1. No puede cambiar los campos opcionales a campos obligatorios.
1. No se pueden añadir nuevos campos obligatorios.
1. No puede cambiar la API de módulos compartidos existentes.

Si realiza cualquiera de estos cambios, cualquier persona que haya instalado la extensión en su propiedad comenzará a tener problemas de inmediato, como estos:

* Las reglas ya no se representarán correctamente porque uno de los componentes de la regla busca un componente que no existe.
* Todas las compilaciones dan error porque la biblioteca incluye un recurso de subida que ya no existe en la extensión.
* Todas las compilaciones dan error porque la biblioteca incluye un recurso con una configuración que no supera la validación del nuevo esquema.

Particularmente en este segundo caso, los usuarios pueden quedar sin una solución y sin ninguna forma de arreglar su propiedad para poder publicar de nuevo.

## Eliminación de funcionalidades

Puede haber casos en los que hay una razón empresarial válida y cree que realmente necesita realizar un cambio prohibido (mencionado arriba). Todavía no se puede hacer, pero aquí tiene alternativas:

1. Deseo eliminar un componente => Cree un nuevo componente y elimine el anterior.
1. Deseo quitar un campo de un componente => Cree un nuevo componente sin ese campo y elimine el anterior.
1. Deseo cambiar un campo opcional para que sea obligatorio => Cree un nuevo componente que requiera el campo deseado y elimine el anterior.
1. Deseo cambiar la API de un módulo compartido => Cree un nuevo módulo compartido y elimine el antiguo.

Puede que elija un hilo común. Eso es bueno. Al dejar de utilizar un componente antiguo, deberá notificar a los usuarios de su extensión que ha quedado obsoleto y que necesitan cambiar a uno nuevo.  Algunas sugerencias para comunicarse con los usuarios:

* Actualice el nombre para mostrar del componente antiguo para incluir &quot;(obsoleto)&quot;.
* Actualice la vista del componente antiguo para que tenga un texto de advertencia de color rojo y en formato grande que indique que este componente está obsoleto y que el usuario debe cambiar al nuevo componente.
* Actualice el código del módulo para registrar los avisos de desaprobación en la consola. Tenga en cuenta que se mostrarán a los usuarios finales, por lo que debe quedar claro y ser algo genérico.
* Envíe mensajes de correo electrónico cordiales desde su sistema de CRM.

En los casos en los que la funcionalidad antigua no solo no se quiere, sino que ya no existe en la solución, hay un paso adicional que puede realizar, pero que solo debe llevar a cabo después de haber informado a los usuarios y de haberles dado tiempo para actualizarla.

* Actualice el contenido del módulo para que este no haga nada. Esto eliminará la funcionalidad de la biblioteca implementada por el usuario en la siguiente compilación, pero no romperá ninguna de sus reglas o compilaciones.

### Restauración de funciones eliminadas

Si ya ha eliminado la funcionalidad y escucha a los usuarios que las cosas están cambiando como resultado, debe publicar una nueva versión de la extensión que restaure los componentes que ha eliminado.

Restaurarlos en un estado obsoleto como se describe arriba está bien, pero deben existir.

Por ejemplo, supongamos que tiene una versión 1.0 con el componente XYZ que utilizan los usuarios. Por eso, publique una versión 1.1 sin el componente XYZ. Los usuarios le informan de que su extensión ha roto sus propiedades y que debe corregirla. Debe publicar una versión 1.2 que devuelva el componente XYZ (quizás en un estado obsoleto, que depende de usted) y hacer que los usuarios actualicen a la versión 1.2 para que las cosas vuelvan a funcionar.
