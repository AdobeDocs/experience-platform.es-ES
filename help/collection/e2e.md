---
title: Información general de extremo a extremo de la recopilación de datos
description: Información general de alto nivel sobre cómo enviar datos de evento a soluciones de Adobe Experience Cloud mediante las funciones de recopilación de datos de Adobe Experience Platform.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 0%

---

# Resumen de la recopilación de datos integral

Adobe Experience Platform recopila y transfiere sus datos a otros productos de Adobe y destinos de terceros. Para enviar datos de evento desde la aplicación a la red perimetral del Experience Platform, es importante comprender estas tecnologías principales y cómo configurarlas para que entreguen los datos a los destinos que necesite, cuando sea necesario.

Esta guía proporciona un tutorial de alto nivel sobre cómo enviar un evento a través de la red perimetral mediante las funciones de recopilación de datos de Platform. En concreto, el tutorial explica los pasos de instalación y configuración de la extensión de etiqueta del SDK web de Adobe Experience Platform en la interfaz de usuario de recopilación de datos (anteriormente Adobe Experience Platform Launch).

>[!NOTE]
>
>También puede optar por instalar y configurar el SDK manualmente si no desea utilizar etiquetas, pero los pasos que lo rodean deben completarse como se describe a continuación.
>
>Todos los pasos que implican la interfaz de usuario de la recopilación de datos también se pueden realizar en la interfaz de usuario del Experience Platform.

## Requisitos previos

Este tutorial utiliza la interfaz de usuario de recopilación de datos para crear un esquema, configurar un conjunto de datos e instalar el SDK web. Para realizar estas acciones en la interfaz de usuario, se debe otorgar acceso a al menos una propiedad web junto con lo siguiente [derechos de propiedad](../tags/ui/administration/user-permissions.md#property-rights):

* Desarrollo
* Administrar extensiones

Consulte la guía de [administración de permisos para la recopilación de datos](./permissions.md) para aprender a conceder acceso a las propiedades y los derechos de propiedad.

Para utilizar los distintos productos de recopilación de datos mencionados en esta guía, también debe tener acceso a los conjuntos de datos y a la capacidad de crear y administrar esquemas. Si necesita acceder a cualquiera de estas funciones, póngase en contacto con su CSM para ayudarle a obtener el acceso necesario. Tenga en cuenta que si no ha comprado Adobe Experience Platform, el Adobe le proporcionará el acceso necesario para utilizar el SDK sin coste adicional.

Si ya tiene acceso a Platform, debe asegurarse de que dispone de todas las [permissions](../access-control/home.md#permissions) en las siguientes categorías habilitadas:

* Modelado de datos
* Identidades

Consulte la [información general sobre la interfaz de usuario de control de acceso](../access-control/ui/overview.md) para aprender a conceder permisos para las funcionalidades de Platform a los usuarios.

## Resumen del proceso

El proceso de configuración de la recopilación de datos para el sitio web se puede resumir de la siguiente manera:

1. [Crear un esquema](#schema) para determinar cómo se estructurarán los datos al enviarlos a la red perimetral.
1. [Crear un conjunto de datos](#datastream) para configurar a qué destinos desea enviar los datos.
1. [Instalación y configuración del SDK web](#sdk) para enviar datos al conjunto de datos cuando se producen determinados eventos en el sitio web.

Una vez que pueda enviar datos a la red perimetral, también puede, opcionalmente, [configurar el reenvío de eventos](#event-forwarding) si su organización tiene una licencia para ello.

## Creación de un esquema {#schema}

[Modelo de datos de experiencia (XDM)](../xdm/home.md) es una especificación de código abierto que proporciona estructuras y definiciones comunes para los datos en forma de esquemas. En otras palabras, XDM es una forma de estructurar y dar formato a los datos de una manera que se puede procesar mediante la red perimetral y otras aplicaciones de Adobe Experience Cloud.

El primer paso para configurar las operaciones de recopilación de datos es crear un esquema XDM que represente los datos. En un paso posterior de este tutorial, asignará los datos que desee enviar a la estructura de este esquema.

>[!NOTE]
>
>Los esquemas XDM son muy personalizables. En lugar de ser demasiado prescriptivos, los pasos descritos a continuación se centran específicamente en los requisitos de esquema para el SDK web. Fuera de estos parámetros, puede definir la estructura restante de sus datos como desee.

En la interfaz de usuario, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo. Desde aquí puede ver una lista de esquemas creados anteriormente que pertenecen a su organización. Para continuar, seleccione **[!UICONTROL Crear esquema]** y, a continuación, seleccione **[!UICONTROL XDM ExperienceEvent]** en el menú desplegable.

![Espacio de trabajo de Esquemas](./images/e2e/schemas.png)

Aparece un cuadro de diálogo que le solicita que empiece a agregar grupos de campos al esquema. Para enviar eventos mediante el SDK web, debe añadir el grupo de campos **[!UICONTROL Mezcla de ExperienceEvent del SDK web de AEP]**. Este grupo de campos contiene definiciones de atributos de datos que la biblioteca del SDK web recopila automáticamente.

Utilice la barra de búsqueda para reducir la lista y encontrar más fácilmente este grupo de campos. Una vez encontrada, selecciónela en la lista antes de seleccionar **[!UICONTROL Agregar grupos de campos]**.

![Espacio de trabajo de Esquemas](./images/e2e/add-field-group.png)

Aparece el lienzo del esquema, que muestra una estructura de árbol del esquema XDM, incluidos los campos proporcionados por el grupo de campos SDK web.

![Estructura del esquema](./images/e2e/schema-structure.png)

Seleccione el campo raíz del árbol para abrir **[!UICONTROL Propiedades del esquema]** en el carril derecho, donde puede proporcionar un nombre y una descripción opcional para el esquema.

![Asigne un nombre al esquema](./images/e2e/name-schema.png)

Si desea añadir más campos al esquema, puede hacerlo seleccionando **[!UICONTROL Agregar]** en el **[!UICONTROL Grupos de campo]** en el carril izquierdo.

![Agregar grupos de campos](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>Consulte la guía de [adición de grupos de campos](../xdm/ui/resources/schemas.md#add-field-groups) en la documentación de XDM para ver los pasos detallados sobre cómo buscar diferentes grupos de campos para adaptarlos a sus casos de uso.
>
>Una práctica recomendada es añadir solo campos para los datos que planea enviar a través de la red perimetral. Una vez añadidos los campos a un esquema y guardados, solo se pueden realizar cambios adicionales en el esquema a partir de entonces. Consulte la sección sobre [reglas de evolución de esquema](../xdm/schema/composition.md#evolution) para obtener más información.

Una vez añadidos los campos que necesite, seleccione **[!UICONTROL Guardar]** para guardar el esquema.

![Guardar el esquema](./images/e2e/save-schema.png)

## Crear un flujo de datos {#datastream}

Un conjunto de datos es una configuración que indica a la red perimetral dónde desea que se envíen los datos. En concreto, un conjunto de datos especifica a qué productos de Experience Cloud desea enviar los datos y a cómo desea que se gestionen y almacenen los datos en cada producto.

>[!NOTE]
>
>Si desea utilizar [reenvío de eventos](../tags/ui/event-forwarding/overview.md) (suponiendo que su organización tenga licencia para la funcionalidad), debe habilitarla para un conjunto de datos de la misma manera que habilita los productos de Adobe. Los detalles de este proceso se tratan en una [sección posterior](#event-forwarding).

Select **[!UICONTROL Datastreams]** en el panel de navegación izquierdo. Desde aquí puede seleccionar un conjunto de datos existente de la lista para editarlo o puede crear una nueva configuración seleccionando **[!UICONTROL Nuevo conjunto de datos]**.

![Corrientes de datos](./images/e2e/datastreams.png)

Los requisitos de configuración de un conjunto de datos dependen de los productos y capacidades a los que envía los datos. Para obtener información detallada sobre las opciones de configuración de cada producto, consulte la [información general sobre datastreams](../edge/datastreams/overview.md).

## Instalación y configuración del SDK web {#install}

Una vez que haya creado un esquema y un conjunto de datos, el siguiente paso es instalar y configurar el SDK web de Platform para que empiece a enviar datos a la red perimetral.

>[!NOTE]
>
>Esta sección utiliza la interfaz de usuario de recopilación de datos para configurar la extensión de etiqueta del SDK web, pero también puede instalarla y configurarla con código sin procesar. Consulte las siguientes guías para obtener más información:
>
>* [Instalación del SDK](../edge/fundamentals/installing-the-sdk.md)
>* [Configuración del SDK](../edge/fundamentals/configuring-the-sdk.md)
>
>Tenga en cuenta también que, aunque solo desee utilizar el reenvío de eventos, aún debe instalar y configurar el SDK tal como se describe antes de configurar el reenvío de eventos en una [paso posterior](#event-forwarding).

El proceso puede resumirse de la siguiente manera:

1. [Instalación del SDK web de Adobe Experience Platform en una propiedad de etiqueta](#install-sdk) para obtener acceso a sus capacidades.
1. [Creación de un elemento de datos de objeto XDM](#data-element) para asignar variables en el sitio web a la estructura del esquema XDM creado anteriormente.
1. [Crear una regla](#rule) para indicar al SDK cuándo debe enviar datos a la red perimetral.
1. [Creación e instalación de una biblioteca](#library) para implementar la regla en el sitio web.

### Instalación del SDK en una propiedad de etiqueta {#install-sdk}

Select **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo para mostrar una lista de propiedades de etiquetas. Puede elegir una propiedad existente para editarla si lo desea, o puede seleccionar **[!UICONTROL Nueva propiedad]** en su lugar.

![Propiedades](./images/e2e/properties.png)

Si crea una nueva propiedad, proporcione un nombre descriptivo y establezca la variable [!UICONTROL Plataforma] a **[!UICONTROL Web]**. Proporcione el dominio completo para la propiedad web y, a continuación, seleccione **[!UICONTROL Guardar]**.

![Crear propiedad](./images/e2e/create-property.png)

Aparecerá la página de información general de la propiedad. Desde aquí, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Catálogo]**. Busque el listado del SDK web de Platform (opcionalmente, utilizando la barra de búsqueda para reducir los resultados) y seleccione **[!UICONTROL Instalar]**.

![Instalación del SDK web](./images/e2e/install-sdk.png)

Aparece la página de configuración del SDK. La mayoría de los valores requeridos se rellenan automáticamente con valores predeterminados que puede elegir cambiar si lo desea.

![Configuración del SDK web](./images/e2e/configure-sdk.png)

Sin embargo, antes de instalar el SDK, debe seleccionar un conjunto de datos para que sepa a dónde enviar los datos. En **[!UICONTROL Datastreams]**, utilice el menú desplegable para seleccionar el conjunto de datos que configuró en un [paso anterior](#datastream). Una vez configurado el conjunto de datos, seleccione **[!UICONTROL Guardar]** para finalizar la instalación del SDK en la propiedad .

![Establecer el conjunto de datos y guardar](./images/e2e/set-datastream.png)

### Creación de un elemento de datos XDM {#data-element}

Para que el SDK envíe datos a la red perimetral, estos datos deben asignarse al esquema XDM que haya creado en un [paso anterior](#schema). Esta asignación se realiza mediante el uso de un elemento de datos.

En la interfaz de usuario, seleccione **[!UICONTROL Elementos de datos]** y, a continuación, seleccione **[!UICONTROL Crear nuevo elemento de datos]**.

![Crear nuevo elemento de datos](./images/e2e/data-elements.png)

En la siguiente pantalla, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]** en el [!UICONTROL Extensión] lista desplegable y, a continuación, seleccione **[!UICONTROL Objeto XDM]** para el tipo de elemento de datos.

![Tipo de objeto XDM](./images/e2e/xdm-object.png)

Aparece el cuadro de diálogo de configuración para el tipo de objeto XDM. El cuadro de diálogo selecciona automáticamente el simulador de pruebas de Platform y, desde aquí, puede ver todos los esquemas creados en dicho simulador de pruebas. Seleccione el esquema XDM que creó anteriormente en la lista.

![Tipo de objeto XDM](./images/e2e/select-schema.png)

Aparece la estructura del esquema . Todos los campos con un asterisco (**\***) indican campos que se rellenarán automáticamente cuando se activen eventos. Para los demás campos, se puede explorar la estructura del esquema y rellenar el resto de los datos.

![Asignación de datos a campos XDM](./images/e2e/map-schema.png)

>[!NOTE]
>
>La captura de pantalla anterior muestra cómo asignar una variable accesible globalmente desde el lado del cliente del sitio web (`cartAbandonsTotal`) a un campo XDM haciendo referencia a su nombre en el [!UICONTROL Valor] campo, rodeado por signos de porcentaje (`%`).
>
>También puede utilizar otros elementos de datos creados anteriormente para rellenar estos campos. Consulte la referencia sobre [elementos de datos](../tags/ui/managing-resources/data-elements.md) en la documentación de etiquetas para obtener más información.

Una vez que haya terminado de asignar los datos al esquema, proporcione un nombre para el elemento de datos antes de seleccionar **[!UICONTROL Guardar]**.

![Asigne un nombre al elemento de datos y guárdelo](./images/e2e/name-and-save.png)

### Crear una regla

Después de guardar el elemento de datos, el siguiente paso es crear una regla que lo envíe a la red perimetral siempre que se produzca un evento determinado en el sitio web (como cuando un cliente añada un producto a un carro de compras).

Puede configurar reglas para prácticamente cualquier evento que se pueda producir en el sitio web. Por ejemplo, esta sección muestra cómo crear una regla que se déclencheur cuando un cliente envía un formulario. El siguiente HTML representa una página web simple con un formulario &quot;Añadir al carro&quot;, que será el asunto de la regla:

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

En la interfaz de usuario de la recopilación de datos, seleccione **[!UICONTROL Reglas]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Crear nueva regla]**.

![Reglas](./images/e2e/rules.png)

En la siguiente pantalla, proporcione un nombre para la regla. A partir de aquí, el siguiente paso es determinar el evento para la regla (es decir, cuándo se activará la regla). Select **[!UICONTROL Agregar]** under [!UICONTROL Eventos].

![Asignar nombre a la regla](./images/e2e/name-rule.png)

Aparece la página de configuración de eventos. Para configurar un evento, primero debe seleccionar el tipo de evento. Las extensiones proporcionan los tipos de eventos. Para configurar un suceso &quot;envío de formulario&quot;, por ejemplo, seleccione la opción **[!UICONTROL Principal]** y, a continuación, seleccione **[!UICONTROL Submit]** tipo de evento en el **[!UICONTROL Formulario]** categoría.

>[!NOTE]
>
>Para obtener más información sobre los distintos tipos de eventos proporcionados por las extensiones web de Adobe, incluido cómo configurarlos, consulte la [Referencia de extensiones de Adobe](../tags/extensions/web/overview.md) en la documentación de etiquetas.

El suceso de envío de formulario permite utilizar un [Selector de CSS](https://www.w3schools.com/css/css_selectors.asp) para hacer referencia a un elemento específico en el que la regla debe activarse. En el ejemplo siguiente, el ID de `add-to-cart-form` se utiliza para que esta regla solo se active para el formulario &quot;Agregar al carro de compras&quot;. Select **[!UICONTROL Conservar cambios]** para agregar el evento a la regla.

![Configuración de eventos](./images/e2e/event-config.png)

La página de configuración de regla vuelve a aparecer y muestra que se ha añadido el evento. Puede reducir el &quot;[!UICONTROL If]&quot; añadiendo más condiciones a la regla.

De lo contrario, el siguiente paso es agregar una acción para que la regla se ejecute cuando se active. Select **[!UICONTROL Agregar]** under **[!UICONTROL Acciones]** para continuar.

![Agregar acción](./images/e2e/add-action.png)

Aparecerá la página de configuración de la acción. Para obtener la regla para enviar datos a la red perimetral, seleccione **[!UICONTROL SDK web de Adobe Experience Platform]** para la extensión y **[!UICONTROL Enviar evento]** para el tipo de acción.

![Tipo de acción](./images/e2e/action-type.png)

La pantalla se actualiza para mostrar opciones adicionales para configurar la acción del evento de envío. En **[!UICONTROL Tipo]**, puede proporcionar un valor de tipo personalizado para rellenar la variable `eventType` Campo XDM. En **[!UICONTROL Datos XDM]**, proporcione el nombre del tipo de datos XDM que creó anteriormente (rodeado de signos de porcentaje) o seleccione el icono de base de datos (![Icono de base de datos](./images/e2e/database-symbol.png)) para seleccionarlo en una lista. Estos son los datos que finalmente se enviarán a la red perimetral.

Select **[!UICONTROL Conservar cambios]** cuando termine.

![Configuración de la acción](./images/e2e/action-config.png)

Una vez que haya terminado de configurar la regla, seleccione **[!UICONTROL Guardar]** para finalizar el proceso.

![Guardar regla](./images/e2e/save-rule.png)

### Creación e instalación de una biblioteca {#library}

Una vez configurada la regla, está listo para agregarla a una biblioteca de etiquetas, crearla en un entorno e instalarla en su sitio web.

>[!NOTE]
>
>Si todavía no ha configurado un entorno en la interfaz de usuario de recopilación de datos, debe hacerlo antes de crear una compilación. Consulte la sección sobre [configuración de un entorno para una propiedad web](../tags/ui/publishing/environments.md#web-configuration) en la documentación de etiquetas para obtener más información.

Para aprender a crear una biblioteca, añadir extensiones y reglas a la biblioteca y crear esa biblioteca en un entorno, consulte la guía de [administración de bibliotecas](../tags/ui/publishing/libraries.md) en la documentación de etiquetas. Al crear la biblioteca, asegúrese de incluir la extensión del SDK web de Platform y las reglas de recopilación de datos que ha creado anteriormente.

Una vez que haya creado la biblioteca y su compilación se haya asignado a un entorno, puede instalar ese entorno en el lado del cliente del sitio web. Consulte la sección sobre [instalación de entornos](../tags/ui/publishing/environments.md#installation) para obtener más información.

Una vez instalado el entorno en el sitio web, puede [probar la implementación](../tags/ui/publishing/embed-code-testing.md) usar Adobe Experience Platform Debugger.

## Configuración del reenvío de eventos (opcional) {#event-forwarding}

>[!NOTE]
>
>El reenvío de eventos solo está disponible para las organizaciones con licencia para él.

Una vez configurado el SDK para que envíe datos a la red perimetral, puede configurar el reenvío de eventos para indicar a la red perimetral dónde desea que se envíen esos datos.

Para utilizar el reenvío de eventos, primero debe crear una propiedad de reenvío de eventos. Select **[!UICONTROL Reenvío de eventos]** en la navegación de la izquierda, seleccione **[!UICONTROL Nueva propiedad]**. Proporcione un nombre a la propiedad antes de seleccionar **[!UICONTROL Guardar]**.

Una vez que se crea una propiedad de reenvío de eventos, el siguiente paso es crear una regla que determine dónde se deben enviar los datos. Las reglas para las propiedades de reenvío de eventos se construyen de la misma manera que las propiedades de etiqueta, con la excepción de que no se puede especificar ningún evento (ya que el reenvío de eventos solo trata los eventos que recibe directamente del conjunto de datos). Para la acción de la regla, puede utilizar una de las extensiones de reenvío de eventos disponibles o utilizar código personalizado para enviar el evento en su lugar.

![Regla de reenvío de eventos](./images/e2e/event-forwarding-rule.png)

Del mismo modo que antes, una vez configurada la regla, debe agregarla a una biblioteca y crearla en un entorno.

Una vez completada la compilación, el paso final es actualizar el conjunto de datos [configurado anteriormente](#datastream) y habilite el reenvío de eventos. Para empezar, vaya a **[!UICONTROL Datastreams]** y seleccione el conjunto de datos en cuestión en la lista. Desde aquí, active la opción para el reenvío de eventos y proporcione los nombres de la propiedad y el entorno que acaba de configurar.

![Almacén de datos de reenvío de eventos](./images/e2e/event-forwarding-datastream.png)

## Pasos siguientes

Esta guía proporciona información general completa sobre cómo enviar datos a la red perimetral mediante el SDK web de Platform. Consulte la documentación vinculada a través de esta guía para obtener más información sobre los distintos componentes y servicios implicados.
