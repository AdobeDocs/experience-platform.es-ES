---
title: Implementación de aplicaciones de una sola página para Adobe Experience Platform Web SDK
description: Obtenga información sobre cómo crear una implementación de aplicación de una sola página (SPA) de Adobe Experience Platform Web SDK mediante Adobe Target.
keywords: target;adobe target;vistas xdm; vistas;aplicaciones de una sola página;SPA;ciclo de vida de SPA;lado del cliente;prueba AB;segmentación de experiencias;XT;VEC
exl-id: cc48c375-36b9-433e-b45f-60e6c6ea4883
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 0%

---


# Implementación de aplicación de una sola página

Adobe Experience Platform Web SDK proporciona funciones enriquecidas que permiten a su empresa personalizar tecnologías de próxima generación del lado del cliente, como aplicaciones de una sola página (SPA).

Los sitios web tradicionales funcionaban en modelos de navegación &quot;página a página&quot;, conocidos como aplicaciones de varias páginas, en las que los diseños de sitios web se asociaban perfectamente a direcciones URL y transiciones de una página web a otra requerida para la carga de páginas.

Las aplicaciones web modernas, como las aplicaciones de una sola página, han adoptado un modelo que impulsa el uso rápido de la representación de la interfaz de usuario del explorador, que a menudo es independiente de las recargas de página. Estas experiencias se pueden activar mediante interacciones de clientes, como desplazamientos, clics y movimientos del cursor. A medida que los paradigmas de la web moderna evolucionan, la importancia de los eventos genéricos tradicionales, como la carga de páginas, para implementar la personalización y la experimentación, ya no es tanta.

![Diagrama que muestra el ciclo de vida de la SPA comparado con el ciclo de vida de la página tradicional.](assets/spa-vs-traditional-lifecycle.png)

## Ventajas de Experience Platform Web SDK para SPA

Estas son algunas ventajas de utilizar Adobe Experience Platform Web SDK para aplicaciones de una sola página:

* Capacidad de almacenar en caché todas las ofertas al cargar la página para reducir el número de llamadas al servidor a una sola llamada.
* Enorme mejora de la experiencia del usuario en su sitio porque las ofertas se muestran inmediatamente a través de la caché sin agotar el tiempo introducido por las llamadas tradicionales al servidor.
* Una sola línea de código y configuración de desarrollador único permite a los especialistas en marketing crear y ejecutar actividades A/B y de segmentación de experiencias (XT) a través del Compositor de experiencias visuales (VEC) en su SPA.

## Vistas de XDM y aplicaciones de una sola página

El VEC de Adobe Target para SPA aprovecha un concepto llamado Vistas: un grupo lógico de elementos visuales que, juntos, constituyen una experiencia de SPA. Por lo tanto, una aplicación de una sola página puede considerarse como una transición entre vistas (en lugar de las direcciones URL) según las interacciones del usuario. Una vista suele representar un sitio completo o elementos visuales agrupados dentro de un sitio.

Para explicar más en detalle cuáles son las vistas, el siguiente ejemplo utiliza un sitio hipotético de comercio electrónico en línea implementado en React para explorar las vistas de ejemplo.

Después de navegar al sitio principal, una imagen promociona una venta de Pascua, así como los productos más recientes disponibles en el sitio. En este caso, se podría definir una Vista para toda la pantalla de inicio. Esta vista podría llamarse simplemente &quot;home&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador.](assets/example-views.png)

A medida que el cliente se interese más por los productos que vende la empresa, decide hacer clic en el vínculo **Productos**. De forma similar a la página de inicio, se puede definir todo el sitio del producto como una vista. Esta vista podría denominarse &quot;products-all&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con todos los productos mostrados.](assets/example-products-all.png)

Dado que una vista puede definirse como un sitio completo o un grupo de elementos visuales en un sitio, los cuatro productos mostrados en el sitio de productos pueden agruparse y considerarse como una vista. Esta vista podría llamarse &quot;productos&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con productos de ejemplo mostrados.](assets/example-products.png)

Cuando el cliente decide hacer clic en el botón **Cargar más** para explorar más productos en el sitio, la dirección URL del sitio web no cambia en este caso, pero se puede crear una vista aquí para representar únicamente la segunda fila de productos que se muestran. El nombre de la vista puede ser &quot;products-page-2&quot;.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con productos de ejemplo mostrados en una página adicional.](assets/example-load-more.png)

El cliente decide adquirir algunos productos en el sitio y pasa a la pantalla de pago. En el sitio de cierre de compra, el cliente tiene la opción de elegir entre envío normal o exprés. Una vista puede ser cualquier grupo de elementos visuales en un sitio, por lo que se puede crear una vista para las preferencias de envío y llamarse &quot;Preferencias de envío&quot;.

![Imagen de muestra de una página de desprotección de aplicación de una sola página en una ventana del explorador.](assets/example-check-out.png)

El concepto de Vistas puede ampliarse mucho más. Estos son solo algunos ejemplos de vistas que se pueden definir en un sitio.

## Implementación de vistas XDM

Las vistas XDM se pueden aprovechar en Adobe Target para que los especialistas en marketing puedan ejecutar pruebas A/B y XT en SPA a través del Compositor de experiencias visuales. Esto requiere realizar los siguientes pasos para completar una configuración de desarrollador única:

1. Instalar [Adobe Experience Platform Web SDK](/help/web-sdk/install/overview.md)
2. Determine todas las vistas XDM de la aplicación de una sola página que desee personalizar.
3. Después de definir las vistas XDM, para entregar actividades AB o XT VEC, implemente la función `sendEvent()` con `renderDecisions` establecido en `true` y la vista XDM correspondiente en la aplicación de una sola página. Se debe pasar la vista XDM en `xdm.web.webPageDetails.viewName`. Este paso permite a los especialistas en marketing aprovechar el Compositor de experiencias visuales para iniciar pruebas A/B y XT para esos XDM.

   ```javascript
   alloy("sendEvent", { 
     "renderDecisions": true, 
     "xdm": { 
       "web": { 
         "webPageDetails": { 
         "viewName":"home" 
         }
       } 
     } 
   });
   ```

>[!NOTE]
>
>En la primera llamada de `sendEvent()`, se recuperarán y almacenarán en caché todas las vistas XDM que se deban procesar al usuario final. Las llamadas subsiguientes `sendEvent()` con vistas XDM pasadas se leerán desde la caché y se procesarán sin una llamada al servidor.

## `sendEvent()` ejemplos de funciones

En esta sección se describen tres ejemplos que muestran cómo invocar la función `sendEvent()` en React para un SPA de comercio electrónico hipotético.

### Ejemplo 1: página principal de la prueba A/B

El equipo de marketing desea ejecutar pruebas A/B en toda la página de inicio.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador.](assets/use-case-1.png)

Para ejecutar pruebas A/B en todo el sitio principal, `sendEvent()` debe invocarse con el XDM `viewName` establecido en `home`:

```jsx
function onViewChange() { 
  
  var viewName = window.location.hash; // or use window.location.pathName if router works on path and not hash 

  viewName = viewName || 'home'; // view name cannot be empty 

  // Sanitize viewName to get rid of any trailing symbols derived from URL 

  if (viewName.startsWith('#') || viewName.startsWith('/')) { 
    viewName = viewName.substr(1); 
  }
   
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName":"home" 
        } 
      } 
    }
  }); 
} 

// react router v4 

const history = syncHistoryWithStore(createBrowserHistory(), store); 

history.listen(onViewChange); 

// react router v3 

<Router history={hashHistory} onUpdate={onViewChange} > 
```

### Ejemplo 2: Productos personalizados

El equipo de mercadotecnia desea personalizar la segunda fila de productos cambiando el color de la etiqueta de precio a rojo después de que un usuario haga clic en **Cargar más**.

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, que muestra ofertas personalizadas.](assets/use-case-2.png)

```jsx
function onViewChange(viewName) { 

  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName
        }
      } 
    } 
  }); 
} 

class Products extends Component { 
  
  render() { 
    return ( 
      <button type="button" onClick={this.handleLoadMoreClicked}>Load more</button> 
    ); 
  } 

  handleLoadMoreClicked() { 
    var page = this.state.page + 1; // assuming page number is derived from component's state 
    this.setState({page: page}); 
    onViewChange('PRODUCTS-PAGE-' + page); 
  } 

} 
```

### Ejemplo 3: Preferencias de envío de la prueba A/B

El equipo de marketing desea ejecutar una prueba A/B para ver si el cambio del color del botón de azul a rojo cuando se selecciona **Envío exprés** puede mejorar las conversiones (en lugar de mantener el botón de color azul en ambas opciones de envío).

![Imagen de muestra de una aplicación de una sola página en una ventana del explorador, con pruebas A/B.](assets/use-case-3.png)

Para personalizar el contenido del sitio según las preferencias de envío que esté seleccionada, se puede crear una vista para cada preferencia de entrega. Cuando se selecciona **Envío normal**, la vista puede llamarse &quot;checkout-normal&quot;. Si se selecciona **Envío exprés**, la vista puede llamarse &quot;checkout-express&quot;.

```jsx
function onViewChange(viewName) { 
  alloy("sendEvent", { 
    "renderDecisions": true, 
    "xdm": { 
      "web": { 
        "webPageDetails": { 
          "viewName": viewName 
        }
      }
    }
  }); 
} 

class Checkout extends Component { 

  render() { 
    return ( 
      <div onChange={this.onDeliveryPreferenceChanged}> 
        <label> 
          <input type="radio" id="normal" name="deliveryPreference" value={"Normal Delivery"} defaultChecked={true}/> 
          <span> Normal Delivery (7-10 business days)</span> 
        </label> 
        <label> 
          <input type="radio" id="express" name="deliveryPreference" value={"Express Delivery"}/> 
          <span> Express Delivery* (2-3 business days)</span> 
        </label> 
      </div> 
    ); 
  } 

  onDeliveryPreferenceChanged(evt) { 
    var selectedPreferenceValue = evt.target.value; 
    onViewChange(selectedPreferenceValue); 
  } 

} 
```

## Uso del Compositor de experiencias visuales para una SPA

Cuando haya terminado de definir las vistas XDM e implementado `sendEvent()` con esas vistas XDM pasadas, el VEC podrá detectar estas vistas y permitir a los usuarios crear acciones y modificaciones para actividades A/B o XT.

>[!NOTE]
>
>Para usar el VEC para tu SPA, debes instalar y activar la extensión [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) o [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper.

### Panel de modificaciones

El panel Modificaciones captura las acciones creadas para una vista en particular. Todas las acciones de una vista se agrupan debajo de esa vista.

![Panel Modificaciones con opciones de carga de página mostradas en la barra lateral de la ventana del explorador.](assets/modifications-panel.png)

### Acciones

Al hacer clic en una acción se resalta el elemento del sitio donde se aplicará esta acción. Cada acción del VEC creada en una vista tiene los iconos siguientes: **Información**, **Editar**, **Clonar**, **Mover** y **Eliminar**. Estos iconos se explican con más detalle en la tabla siguiente.

![Iconos de acción](assets/action-icons.png)

| Icono | Descripción |
|---|---|
| Información | Muestra los detalles de la acción. |
| Editar | Permite editar las propiedades de la acción directamente. |
| Clonar | Clona la acción a una o varias vistas del panel Modificaciones o a una o varias vistas a las que ha llegado a través del VEC. La acción no tiene que incluirse necesariamente en el panel Modificaciones.<br/><br/>**Nota:** Después de realizar una operación de clonación, debe navegar a la vista en el VEC a través de Examinar para ver si la acción clonada era una operación válida. Si la acción no se puede aplicar a la vista, aparecerá un error. |
| Mover | Mueve la acción a un Evento de carga de página o a cualquier otra Vista que ya exista en el panel Modificaciones.<br/><br/>**Evento de carga de página:** Todas las acciones correspondientes al evento de carga de página se aplican en la carga inicial de la página web. <br/><br/>**Nota:** Después de realizar una operación de movimiento, debe navegar a la vista en el VEC a través de Examinar para ver si el movimiento era una operación válida. Si la acción no se puede aplicar a la vista, aparecerá un error. |
| Eliminar | Elimina la acción. |

## Uso del VEC para ejemplos de SPA

En esta sección se describen tres ejemplos de cómo usar el Compositor de experiencias visuales para crear acciones y modificaciones para actividades A/B o XT.

### Ejemplo 1: Actualizar la vista &quot;principal&quot;

Anteriormente en este documento, se definía una vista denominada &quot;inicio&quot; para todo el sitio principal. Ahora, el equipo de marketing desea actualizar la vista &quot;principal&quot; de las siguientes maneras:

* Cambie los botones **Agregar al carro** y **Me gusta** por una parte más clara de azul. Esto debería suceder durante la carga de la página, ya que implica cambiar los componentes del encabezado.
* Cambie la etiqueta **Productos más recientes para 2019** por **Productos de prueba para 2019** y cambie el color del texto a morado.

Para realizar estas actualizaciones en el VEC, seleccione **Componer** y aplique esos cambios a la vista &quot;Inicio&quot;.

![Página de muestra del Compositor de experiencias visuales.](assets/vec-home.png)

### Ejemplo 2: Cambiar etiquetas de producto

Para la vista &quot;products-page-2&quot;, al equipo de mercadotecnia le gustaría cambiar la etiqueta de **Price** a **Sale Price** y cambiar el color de la etiqueta a rojo.

Para realizar estas actualizaciones en el VEC, se requieren los siguientes pasos:

1. Seleccione **Examinar** en el VEC.
2. Seleccione **Productos** en la barra de navegación superior del sitio.
3. Seleccione **Cargar más** una vez para ver la segunda fila de productos.
4. Seleccione **Componer** en el VEC.
5. Aplique acciones para cambiar la etiqueta de texto a **Precio de venta** y el color a rojo.

![Página de muestra del Compositor de experiencias visuales con etiquetas de producto.](assets/vec-products-page-2.png)

### Ejemplo 3: Personalizar el estilo de preferencias de entrega

Las vistas se pueden definir a nivel granular, como un estado o una opción de un botón de opción. Anteriormente, en este documento, las vistas se definían para las preferencias de entrega, &quot;cierre de compra normal&quot; y &quot;cierre de compra exprés&quot;. El equipo de marketing desea cambiar el color del botón a rojo para la vista &quot;checkout-express&quot;.

Para realizar estas actualizaciones en el VEC, se requieren los siguientes pasos:

1. Seleccione **Examinar** en el VEC.
2. Agregar productos al carro de compras en el sitio.
3. Seleccione el icono de carro de compras en la esquina superior derecha del sitio.
4. Seleccione **Finalizar compra**.
5. Seleccione el botón de opción **Envío exprés** en **Preferencias de envío**.
6. Seleccione **Componer** en el VEC.
7. Cambia el color del botón **Pagar** a rojo.

>[!NOTE]
>
>La vista &quot;checkout-express&quot; no aparece en el panel Modificaciones hasta que se selecciona el botón de opción **Envío exprés**. Esto se debe a que la función `sendEvent()` se ejecuta cuando se selecciona el botón de opción **Envío exprés**, por lo que el VEC no tiene en cuenta la vista &quot;Pago y envío exprés&quot; hasta que se selecciona el botón de opción.

![Compositor de experiencias visuales muestra el selector de preferencias de envío.](assets/vec-delivery-preference.png)
