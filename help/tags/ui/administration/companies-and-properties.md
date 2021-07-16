---
title: Propiedades
description: Conozca cómo las extensiones, los entornos y las bibliotecas están organizados y agrupados para su organización en Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 70%

---

# Propiedades

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## Propiedades web

Una propiedad web es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Cada propiedad web tiene su propio conjunto de códigos incrustados y se puede implementar en cualquier número de sitios web diferentes (dominios diferentes).

## Propiedades móviles

Un tipo de propiedad móvil puede contener varias aplicaciones. Por ejemplo, en una propiedad móvil puede gestionar el mismo conjunto de reglas y extensiones en varias aplicaciones iOS y Android.

Para ver un videotutorial, consulte [Creación de su primera propiedad](../../quick-start/videos.md).

## Prácticas recomendadas para la planificación de propiedades {#best-practices-for-planning-properties}

Cada implementación de etiquetas en Adobe Experience Platform puede ser muy diferente. Tienen una amplia variedad de necesidades de recopilación de datos, uso de variables, extensiones, etiquetas de terceros, otros sistemas y tecnologías, personas, equipos y regiones geográficas, entre otros. Debe estructurar las propiedades de forma que coincidan con el flujo de trabajo y los procesos de la organización IMS.

Considerar lo siguiente a la hora de planificar las propiedades

* Estructura de código
* Datos
* Variables
* Extensiones, etiquetas y sistemas
* Personas

### Estructura de código

Los sitios se basan en HTML y aplicaciones móviles en código. Si las plantillas o los códigos HTML subyacentes son los mismos para varios sitios y aplicaciones, le recomendamos considerar el uso de una sola propiedad de etiqueta para administrar varios sitios o aplicaciones.

### Datos

Para todos los sitios web o aplicaciones, ¿los datos que va a recopilar son muy similares, son parecidos o son únicos?

Si los datos que necesita recopilar son similares en distintos sitios, puede que sea recomendable agrupar los sitios o aplicaciones en una propiedad web para evitar la duplicación de reglas o la necesidad de copiar las reglas de una propiedad a otra.

Si la recopilación de datos debe ser única para cada sitio o aplicación, puede que sea recomendable separarlos de sus propias propiedades. Este método permite controlar las recopilaciones de datos de una forma más específica, sin necesidad de utilizar una gran cantidad de lógica condicional en los scripts personalizados.

### Variables

De forma similar a los datos, ¿las variables que va a establecer en [!DNL Analytics] y en otras herramientas son muy similares, son parecidas o son únicas?

Por ejemplo, si se utiliza eVar27 para el mismo valor de fuente en todos los sitios o aplicaciones, puede que sea recomendable agrupar estos sitios o aplicaciones de forma que pueda establecer las variables comunes de sus sitios en una única propiedad web.

### Extensiones, etiquetas y sistemas

¿Las extensiones, etiquetas y sistemas que va a implementar son muy similares, son parecidos o son únicos?

Si las extensiones, etiquetas y sistemas que va a implementar son muy similares en sus sitios o aplicaciones, es posible que desee incluirlos en la misma propiedad.

Si va a implementar [!DNL Adobe Analytics] solo en un sitio o aplicación, y las demás extensiones y etiquetas son también únicas, puede que desee crear propiedades independientes para tener más control.

Por ejemplo, si está implementando [!DNL Adobe Analytics], [!DNL Target] y las mismas extensiones de terceros en todos sus sitios o aplicaciones, tiene sentido realizar agrupaciones.

### Personas

Para las personas, los equipos y las organizaciones que trabajan en Adobe Experience Platform, ¿necesitarán acceso a todos sus sitios web y aplicaciones, a algunos o solo a uno?

Las funciones de administración de usuarios le permiten asignar diferentes funciones a distintas personas para todas las propiedades, o en función de cada propiedad. Si alguien tiene derechos suficientes, esa persona puede realizar acciones administrativas en todas las propiedades de esa organización IMS de Platform. El resto de las funciones se podrán asignar en función de cada propiedad. Incluso puede ocultar una propiedad para determinados usuarios (que no sean administradores). Para ello, no debe otorgarles ninguna función en dicha propiedad.

## Página de Properties

Una propiedad es una colección de reglas, elementos de datos, extensiones configuradas, entornos y bibliotecas. Para la web, solo hay un código incrustado de publicación por propiedad. Para móviles, hay un ID de aplicación de configuración por propiedad.

Una propiedad puede ser cualquier conjunto de uno o varios dominios y subdominios. Puede administrar y rastrear estos recursos de manera similar. Por ejemplo, supongamos que tiene varios sitios web basados en una plantilla y quiere rastrear los mismos recursos en todos. Puede aplicar una propiedad a varios dominios.

La parte izquierda de la pantalla muestra las compañías de su organización. Esto es especialmente útil si administra varias cuentas. Seleccione una compañía para ver las propiedades y los registros de auditoría de esa compañía.

Cada propiedad se muestra en la lista Properties.

En la lista Properties se muestra la siguiente información:

* Nombre de la propiedad
* Plataforma
* Estado

Seleccione una propiedad para ver una descripción general de dicha propiedad. La descripción general muestra toda actividad realizada sobre la propiedad. También muestra las métricas y extensiones de la propiedad.

## Creación o configuración de una propiedad

En esta sección se explica cómo crear o configurar una propiedad de etiqueta en Adobe Experience Platform.

>[!NOTE]
>
>Solo los usuarios con derechos suficientes pueden crear una propiedad. Consulte [Administración de usuarios](user-permissions.md).

Antes de comenzar, consulte [Prácticas recomendadas para la planificación de propiedades](companies-and-properties.md#best-practices-for-planning-properties) para obtener propiedades.

Vaya a la página de su empresa y, a continuación, seleccione **[!UICONTROL Añadir propiedad]**, o bien escoja una propiedad existente de la lista y seleccione **[!UICONTROL Configurar]**.

![](../../images/property-settings.png)

### Para la web

Siga las instrucciones para crear una propiedad web.

1. Rellene los campos:

   **Nombre:** el nombre de su propiedad.

   **Dominios:** la dirección URL base de los sitios en los que planee implementar esta propiedad.

1. (Avanzado) **[!UICONTROL Ejecutar componentes de regla en secuencia]**: Seleccione esta casilla de verificación para que las condiciones y las acciones esperen a que se complete la anterior antes de ejecutarse.
1. (Avanzado) **[!UICONTROL Devolver una cadena vacía para los elementos de datos que faltan:]** Si hace referencia a un elemento de datos que no existe dentro de una biblioteca, normalmente devolverá `undefined`. Seleccione esta casilla de verificación si desea que ese escenario devuelva una cadena vacía en su lugar.
1. (Avanzado) **[!UICONTROL Configurar para desarrollo de extensiones:]** Seleccione esta casilla de verificación si planea instalar extensiones de desarrollo que su compañía esté desarrollando activamente.
1. Seleccione **[!UICONTROL Guardar]**.

### Para dispositivos móviles

Siga las instrucciones para crear una propiedad móvil.

1. Rellene los campos:

   * **Nombre:** el nombre de su propiedad.
   * **Privacy:** de forma predeterminada, la configuración de privacidad se configura en “Opted in”, lo que significa que desea que el SDK recopile y envíe datos a las soluciones. Si selecciona “Opted out”, el SDK de forma predeterminada NO envía datos a las soluciones. Si elige Desconocido como configuración, el SDK requerirá que la aplicación solicite primero al usuario que permita la recopilación y el uso compartido de datos.

      >[!NOTE]
      >
      >Estos ajustes se pueden controlar aún más mediante API en la aplicación móvil.

   * **Use HTTPS:** seleccione si todas las comunicaciones de datos deben enviarse por HTTP o HTTPS.

1. Seleccione **[!UICONTROL Guardar]**.

Una vez creada la propiedad, Platform agrega automáticamente un host predeterminado, un conjunto de entornos (Desarrollo, Ensayo y Producción) y las extensiones predeterminadas.

## Eliminar una propiedad

Siga los pasos a continuación para eliminar una propiedad de etiqueta.

>[!NOTE]
>
>No se puede deshacer la eliminación de una propiedad. El solicitante debe ser un usuario de nivel de administrador. Esta solicitud no se puede deshacer.

1. En la lista Propiedades, seleccione la propiedad que desee eliminar.

   Puede seleccionar varias propiedades que desee eliminar.

1. Seleccione **[!UICONTROL Eliminar]** y confirme la eliminación de la propiedad.
