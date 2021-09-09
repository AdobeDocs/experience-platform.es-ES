---
title: Extensiones
description: Conozca cómo funcionan las extensiones de etiquetas en Adobe Experience Platform.
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
source-git-commit: f7edfa05e25c17f9ace34287c8a2d8426d0f36d4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una extensión es un conjunto de código empaquetado que amplía las funcionalidades proporcionadas por las etiquetas o el reenvío de eventos.

Añadir una extensión añade nuevos elementos de datos y nuevas opciones de creación de reglas.

Las extensiones determinan los elementos disponibles al crear propiedades, reglas y elementos de datos. Proporcionan:

* Eventos, condiciones y excepciones
* Elementos de datos
* Código del lado del cliente

Utilice los enlaces de la parte superior de la lista Extensions para ver las extensiones instaladas, el catálogo de extensiones o las actualizaciones.

Seleccione una extensión y, a continuación, seleccione [!UICONTROL Configurar] para ver y modificar la configuración de la extensión. Para obtener más información, consulte la sección sobre [adición de una nueva extensión](#add-a-new-extension) para obtener información sobre las opciones de extensión.

>[!IMPORTANT]
>
>Los cambios no surtirán efecto hasta [que se publiquen](../../publishing/overview.md).

De forma predeterminada, Adobe proporciona extensiones compatibles con integraciones comunes. Las extensiones se pueden modificar mediante configuraciones personalizadas. Las configuraciones se proporcionan a través de las extensiones. Para crear una configuración, seleccione la tarjeta de extensión y, a continuación, seleccione **[!UICONTROL Añadir nueva configuración]**.

## Catálogo de extensiones

Utilice el catálogo de extensiones para examinar, configurar e implementar tecnología de marketing y publicidad creada y mantenida por proveedores de software independientes, así como extensiones para soluciones de Adobe.

La página Extensions proporciona tres vistas:

* Instalado

   Muestra todas las extensiones instaladas.

* Catálogo
* Muestra todas las extensiones disponibles.
* Actualizaciones

   Muestra las actualizaciones disponibles para las extensiones instaladas.

Seleccione **[!UICONTROL Extensiones]** para ver todas las extensiones instaladas. También puede utilizar el catálogo para ver una lista de todas las extensiones disponibles y qué extensiones tienen actualizaciones disponibles.

Consulte [Referencia de extensiones](../../../extensions/web/overview.md) para obtener detalles sobre las extensiones de Adobe.

## Añadir una nueva extensión de {#add-a-new-extension}

Las etiquetas son muy extensibles. Las extensiones añaden funciones principales a las etiquetas. Un uso habitual de las extensiones es la creación de integraciones con otras aplicaciones.

1. En la página de información general de una propiedad, abra la pestaña **[!UICONTROL Extensiones]**.
1. Seleccione una extensión.

   ![Extensión principal](../../../images/extensions.png)

   * Si la extensión existe, selecciónela en el catálogo de extensiones.
   * Pase el ratón sobre una extensión de la lista para configurarla o deshabilitarla.
   * Añada otras extensiones del catálogo si estas no están actualmente en la lista.

   La extensión principal es el punto de partida de la nueva extensión. La extensión predeterminada proporciona:

   * Eventos predeterminados
   * Condiciones y excepciones predeterminadas
   * Código predeterminado del lado del cliente

   Estos valores predeterminados constituyen la base de las reglas personalizadas que usted desarrolla para crear la extensión.

Al crear o editar elementos, puede guardar y desarrollar en su [biblioteca activa](../../publishing/libraries.md#active-library). Esto guarda inmediatamente el cambio en la biblioteca y ejecuta una compilación. Se muestra el estado de la compilación. También puede crear una nueva biblioteca desde la lista desplegable Active Library.

## Configuración de una extensión

Coloque el ratón sobre una extensión instalada y seleccione **[!UICONTROL Configurar]**.

>[!NOTE]
>
>Algunas extensiones no necesitan configuración y no ofrecen opciones de configuración.

Cada extensión configurable tiene opciones únicas. Consulte [Referencia de extensiones](../../../extensions/web/overview.md) para obtener información sobre las opciones disponibles para cada extensión de Adobe.
