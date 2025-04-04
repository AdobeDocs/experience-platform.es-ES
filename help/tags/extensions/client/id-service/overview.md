---
title: Información general sobre la extensión del servicio de identidad de Adobe Experience Cloud
description: Obtenga información acerca de la extensión de etiquetas del servicio de identidad de Adobe Experience Cloud en Adobe Experience Platform.
exl-id: 9bfcb666-a3f1-46ad-8678-2c63738da2b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 95%

---

# Información general sobre la extensión del servicio de identidad de Adobe Experience Cloud

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Utilice esta referencia para obtener información acerca de cómo configurar la extensión del Adobe Experience Cloud ID y las opciones disponibles al utilizar esta extensión para generar una regla.

Utilice esta extensión para integrar el servicio de identidad de Experience Cloud con su propiedad. Con el servicio de identidad de Experience Cloud, puede crear y almacenar ID únicos y persistentes para los visitantes del sitio.

## Configurar la extensión Experience Cloud ID

Esta sección proporciona una referencia para las opciones disponibles al configurar la extensión Experience Cloud ID.

Si la extensión Experience Cloud ID aún no está instalada, abra su propiedad, haga clic en **[!UICONTROL Extensiones > Catálogo]**, sitúe el cursor sobre la extensión Experience Cloud ID y, a continuación, haga clic en **[!UICONTROL Instalar]**.

Para configurar la extensión, abra la pestaña Extensiones, pase el puntero sobre la extensión y, a continuación, seleccione **[!UICONTROL Configurar]**.

![](../../../images/optin.jpg)

Las opciones de configuración disponibles son las siguientes:

### Experience Cloud Organization ID

El ID de su organización de Experience Cloud.

Este ID es una cadena alfanumérica de 24 caracteres seguida de `@AdobeOrg`. Si no conoce este ID, póngase en contacto con el Servicio de atención al cliente.

### Excluir rutas específicas

El Experience Cloud ID no se carga si la dirección URL coincide con cualquiera de las rutas especificadas.

(Opcional) Habilite Regex si es una expresión regular.

Seleccione **[!UICONTROL Añadir]** para excluir otra ruta.

### Opt-in

Utilice las opciones de inclusión Opt-in para determinar si se requiere que los visitantes acepten los servicios de Adobe en su sitio, incluido si se crean cookies que realizan un seguimiento de la actividad del visitante.

La opción Opt-in es el punto de referencia centralizado de todas las bibliotecas de soluciones del lado del cliente de Experience Platform para determinar si las cookies se pueden crear en un dispositivo o explorador del usuario al visitar el sitio. La opción Opt In no proporciona asistencia para recopilar o almacenar las preferencias de consentimiento de usuario.

**¿Desea habilitar la opción Opt In?**

La opción seleccionada determina si el sitio web espera el consentimiento para rastrear las actividades de un visitante en el sitio web.

Tiene tres opciones:

* **No:** No espera el consentimiento para rastrear al visitante. Este es el comportamiento predeterminado si no selecciona otra opción.
* **Sí:** Espera al consentimiento para rastrear al visitante.
* **Se determina durante la ejecución mediante la función:** Se determina mediante programación si el valor es &quot;true&quot; o &quot;false&quot; durante la ejecución. Si selecciona esta opción, aparecerá el campo Select Data Element. Seleccione un elemento de datos que pueda determinar si desea esperar el consentimiento. Este elemento de datos responde a un valor booleano. Por ejemplo, puede seleccionar un elemento de datos que proporcione consentimiento y que esté determinado por la posible ubicación dentro de la UE del visitante.

**¿Está habilitada la opción de Opt In del almacenamiento?**

Si está habilitado, el consentimiento se almacena en una cookie individual de su dominio. Si no está habilitada, la configuración de consentimiento se conserva en la CMP o en una cookie que administra.

**¿Cuál es el dominio de la opción Opt In?**

Utilice esta configuración opcional para especificar el dominio donde la cookie de Opt In se almacena, en el caso de que el almacenamiento esté habilitado. Puede introducir un dominio o seleccionar un elemento de datos que contenga el dominio.

**¿Cuál es la caducidad del almacenamiento de la opción Opt In?**

Especifique cuando la cookie Opt In caduca si el almacenamiento está habilitado, en segundos.

Indique un número y, a continuación, seleccione una unidad de tiempo en la lista desplegable. Por ejemplo, introduzca 2 y seleccione **[!UICONTROL Semanas]**. El valor predeterminado es de 13 meses.

**¿Permisos?**

Pase el consentimiento previo a la biblioteca de Opt In. Seleccione un elemento de datos que contenga el consentimiento. El tipo de elemento debe ser un objeto o una cadena JSON. Anulaciones de aprobaciones previas a la opción Opt In.

Ejemplo:

`"{"aa":true,"aam":true,"ecid":true}"`

**¿Hay aprobaciones previas de la opción Opt In?**

Se definen qué categorías se aprueban o deniegan cuando el visitante no haya establecido ninguna preferencia. Se asume el consentimiento de las soluciones seleccionadas desde el momento en que se carga la página. El tipo de elemento debe ser un objeto o una cadena JSON (por ejemplo: `{aam: true}`).

### Variables

Establezca pares de nombre-valor como propiedades de instancias de Experience Cloud ID. Utilice la lista desplegable para seleccionar una variable, luego escriba o seleccione un valor. Para obtener información acerca de cada variable, consulte la documentación de [Servicio de identidad de Experience Cloud](https://experiencecloud.adobe.com/resources/help/es_ES/mcvid/mcvid-overview.html).

## Tipos de acción de extensión de Experience Cloud ID

Esta sección describe los tipos de acción disponibles en la extensión de Experience Cloud ID.

### Tipos de acción

#### Establecimiento de ID de cliente

Establezca uno o más ID de cliente.

1. Introduzca el código de integración.

   El código de integración debe contener el valor definido como fuente de datos en Audience Manager o Customer Attributes.

1. Seleccione un valor.

   El valor debe ser un ID de usuario. Los elementos de datos son contenedores adecuados para valores dinámicos, como los ID de un sistema interno específico del cliente.

1. Seleccione un estado de autenticación.

   Entre las opciones disponibles se encuentran:

   * Unknown
   * Authenticated
   * Logged out

1. (Opcional) Seleccione **[!UICONTROL Añadir]** para configurar más ID de cliente.
1. Seleccione **[!UICONTROL Conservar cambios]**.
