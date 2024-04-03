---
title: Información general sobre la extensión de Adobe Analytics Product String
description: Obtenga información acerca de la extensión de etiqueta Adobe Analytics Product String en Adobe Experience Platform.
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 36ca1e63c043baa776f27b627cdbe493b2ced674
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 96%

---

# Información general sobre la extensión de Adobe Analytics Product String

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La variable `products` realiza el seguimiento de la manera en que los usuarios interaccionan con los productos del sitio. Por ejemplo, la variable `products` puede realizar el seguimiento de cuántas veces se ha visto un producto, se ha agregado al carro de compras, se ha cerrado su compra y se ha comprado. También puede realizar el seguimiento de la eficacia relativa de las categorías de comercialización del sitio.

La variable `products` siempre se debe configurar junto con un evento de éxito.

La extensión de [!DNL Adobe Analytics Product String Builder] establece automáticamente la variable `products` al realizar un bucle en la capa de datos, tomar todos los datos necesarios relacionados con el producto y aplicarle formato con la sintaxis adecuada que se muestra a continuación. Ya no necesita escribir y mantener JavaScript personalizado para realizar estas complejas acciones.

## Sintaxis de la variable Products

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Para obtener toda la documentación, visite [Products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=es).

## Instrucciones de la extensión

### Configuración de la acción

Agregue la acción “Adobe Analytics Product String - Set s.products” a la regla.

![Configuración de la acción](./images/screenshot-action-config.png)

### Configuración de los datos de producto estándar

A continuación, defina las variables de la capa de datos. Después de configurar la acción como se describe en el paso anterior, aparece la siguiente pantalla:

![Campos estándar](./images/screenshot-standard-fields.png)

Para cada uno de los puntos de datos que desee incluir en la cadena de producto, introduzca la ruta a la variable de capa de datos correspondiente.

Por ejemplo, si la capa de datos está estructurada de esta manera:

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

Debe introducir la siguiente ruta en el campo “Variable para ID/nombre del producto” para capturar la variable `productName`:

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>Si utiliza un elemento de datos para rellenar el campo, debe configurarse con el tipo de elemento de datos “Constante” o “Código personalizado” y devolver la ruta de acceso anterior como un literal de cadena.

### Tipo de precio

El parámetro `price` de la cadena de producto de [!DNL Adobe Analytics] debe reflejar el precio total del número de unidades adquiridas, no el precio unitario, de ese producto. Al habilitar el campo Price en la acción de la extensión, debe especificar si la capa de datos expone el precio total o el precio unitario. Al utilizar el precio unitario, la extensión de [!DNL Adobe Analytics Product String] multiplica automáticamente el precio unitario por la cantidad para obtener el precio total y establecer la cadena de producto correctamente.

![Tipo de precio](./images/screenshot-price-type.png)

### eVars de comercialización y eventos personalizados

![eVars y eventos](./images/screenshot-events-evars.png)

Si su implementación utiliza eventos personalizados o eVars de comercialización, siga estos pasos:

1. Seleccione el botón **[!UICONTROL Añadir]** asociado.
1. Elija el evento o la eVar que debe establecer en el menú desplegable.
1. Introduzca la ruta a la variable de capa de datos adecuada utilizando la misma sintaxis descrita anteriormente.

### Secuencia de acciones

Esta acción debe ir acompañada de una acción “Adobe Analytics - Set Variables” que establezca los eventos de éxito correspondientes, así como de una acción “Adobe Analytics - Send Beacon”. A continuación se ilustra la secuencia adecuada de acciones.

![Campos estándar](./images/screenshot-action-type.png)

### Requisitos

* Una [capa de datos](https://theblog.adobe.com/data-layers-buzzword-best-practice/) basada en objetos con variables para todos los datos relacionados con el producto (como el ID del producto, cantidad, precio). Esta extensión no funciona con capas de datos basadas en una matriz.
* Se debe instalar la extensión de [Adobe Analytics](../analytics/overview.md).
