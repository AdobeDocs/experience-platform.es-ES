---
title: Preparación de datos para la recopilación de datos
description: Obtenga información sobre cómo asignar los datos a un esquema de evento del Modelo de datos de Experience (XDM) al configurar un conjunto de datos para los SDK web y móviles de Adobe Experience Platform.
exl-id: 87a70d56-1093-445c-97a5-b8fa72a28ad0
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# Preparación de datos para la recopilación de datos

Preparación de datos es un servicio de Adobe Experience Platform que le permite asignar, transformar y validar datos desde y hacia [Modelo de datos de experiencia (XDM)](../../xdm/home.md). Al configurar una plataforma habilitada [datastream](./overview.md), puede utilizar las funciones de preparación de datos para asignar los datos de origen a XDM al enviarlos a la red perimetral de plataforma.

>[!NOTE]
>
>Para obtener una guía completa sobre todas las funciones de preparación de datos, incluidas las funciones de transformación para campos calculados, consulte la siguiente documentación:
>
>* [Resumen de la preparación de datos](../../data-prep/home.md)
>* [Funciones de asignación de preparación de datos](../../data-prep/functions.md)
>* [Gestión de formatos de datos con la preparación de datos](../../data-prep/data-handling.md)


Esta guía explica cómo asignar los datos dentro de la interfaz de usuario de . Para seguir los pasos, inicie el proceso de creación de un conjunto de datos hasta (e incluido) el [paso básico de configuración](./overview.md#create).

Para ver una demostración rápida del proceso de preparación de datos para la recopilación de datos, consulte el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/342120?quality=12&enable10seconds=on&speedcontrol=on)

## [!UICONTROL Selección de datos] {#select-data}

Select **[!UICONTROL Guardar y agregar asignaciones]** después de completar la configuración básica de un conjunto de datos, y **[!UICONTROL Seleccionar datos]** aparece. A partir de aquí, debe proporcionar un objeto JSON de muestra que represente la estructura de los datos que planea enviar a Platform.

Para capturar propiedades directamente desde la capa de datos, el objeto JSON debe tener una sola propiedad raíz `data`. Las subpropiedades de la variable `data` a continuación, debe crearse de forma que se asigne a las propiedades de la capa de datos que desee capturar. Seleccione la sección siguiente para ver un ejemplo de un objeto JSON con un formato correcto con un `data` raíz.

+++Ejemplo de archivo JSON con `data` root

```json
{
  "data": {
    "eventMergeId": "cce1b53c-571f-4f36-b3c1-153d85be6602",
    "eventType": "view:load",
    "timestamp": "2021-09-30T14:50:09.604Z",
    "web": {
      "webPageDetails": {
        "siteSection": "Product section",
        "server": "example.com",
        "name": "product home",
        "URL": "https://www.example.com"
      },
      "webReferrer": {
        "URL": "https://www.adobe.com/index2.html",
        "type": "external"
      }
    },
    "commerce": {
      "purchase": 1,
      "order": {
        "orderID": "1234"
      }
    },
    "product": [
      {
        "productInfo": {
          "productID": "123"
        }
      },
      {
        "productInfo": {
          "productID": "1234"
        }
      }
    ],
    "reservation": {
      "id": "anc45123xlm",
      "name": "Embassy Suits",
      "SKU": "12345-L",
      "skuVariant": "12345-LG-R",
      "priceTotal": "112.99",
      "currencyCode": "USD",
      "adults": 2,
      "children": 3,
      "productAddMethod": "PDP",
      "_namespace": {
        "test": 1,
        "priceTotal": "112.99",
        "category": "Overnight Stay"
      },
      "freeCancellation": false,
      "cancellationFee": 20,
      "refundable": true
    }
  }
}
```

+++

Para capturar propiedades de un elemento de datos de objeto XDM, se aplican las mismas reglas al objeto JSON, pero la propiedad raíz debe tener una clave que `xdm` en su lugar. Seleccione la sección siguiente para ver un ejemplo de un objeto JSON con un formato correcto con un `xdm` raíz.

+++Ejemplo de archivo JSON con `xdm` root

```json
{
  "xdm": {
    "environment": {
      "type": "browser",
      "browserDetails": {
        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_5) AppleWebkit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.112 Safari/537.36",
        "javaScriptEnabled": true,
        "javaScriptVersion": "1.8.5",
        "cookiesEnabled": true,
        "viewportHeight": 900,
        "viewportWidth": 1680,
        "javaEnabled": true
      },
      "domain": "adobe.com",
      "colorDepth": 24,
      "viewportHeight": 1050,
      "viewportWidth": 1680
    },
    "device": {
      "screenHeight": 1050,
      "screenWidth": 1680
    }
  }
}
```

+++

Puede seleccionar la opción para cargar el objeto como archivo o pegar el objeto sin procesar en el cuadro de texto proporcionado. Si el JSON es válido, se muestra un esquema de vista previa en el panel derecho. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![Ejemplo de JSON de datos entrantes esperados](../images/datastreams/data-prep/select-data.png)

## [!UICONTROL Asignación]

La variable **[!UICONTROL Asignación]** , lo que le permite asignar los campos de los datos de origen a los del esquema de evento de destino en Platform. Desde aquí puede configurar la asignación de dos formas:

* [Crear nuevas reglas de asignación](#create-mapping) para este conjunto de datos a través de un proceso manual.
* [Importar reglas de asignación](#import-mapping) de un conjunto de datos existente.

### Crear una nueva asignación {#create-mapping}

Para empezar, seleccione **[!UICONTROL Añadir nueva asignación]** para crear una nueva fila de asignación.

![Adición de una nueva asignación](../images/datastreams/data-prep/add-new-mapping.png)

Seleccione el icono de origen (![Icono de origen](../images/datastreams/data-prep/source-icon.png)) y, en el cuadro de diálogo que aparece, seleccione el campo de origen que desea asignar en el lienzo proporcionado. Una vez que haya elegido un campo, utilice la variable **[!UICONTROL Select]** para continuar.

![Selección del campo a asignar en el esquema de origen](../images/datastreams/data-prep/source-mapping.png)

A continuación, seleccione el icono de esquema (![Icono de esquema](../images/datastreams/data-prep/schema-icon.png)) para abrir un cuadro de diálogo similar para el esquema de eventos de destino. Elija el campo al que desea asignar los datos antes de confirmar con **[!UICONTROL Select]**.

![Selección del campo a asignar en el esquema de destino](../images/datastreams/data-prep/target-mapping.png)

La página de asignación vuelve a aparecer con la asignación de campo completada que se muestra. La variable **[!UICONTROL Asignación del progreso]** actualizaciones de sección para reflejar el número total de campos que se han asignado correctamente.

![Campo asignado correctamente con progreso reflejado](../images/datastreams/data-prep/field-mapped.png)

>[!TIP]
>
>Si desea asignar una matriz de objetos (en el campo de origen) a una matriz de diferentes objetos (en el campo de destino), agregue `[*]` después del nombre de la matriz en las rutas de los campos de origen y destino, como se muestra a continuación.
>
>![Asignación de objetos de matriz](../images/datastreams/data-prep/array-object-mapping.png)

### Importar reglas de asignación existentes {#import-mapping}

Si ya ha creado un conjunto de datos, puede reutilizar las reglas de asignación configuradas para un nuevo conjunto de datos.

>[!WARNING]
>
>La importación de reglas de asignación desde otro conjunto de datos sobrescribirá cualquier asignación de campo que haya agregado antes de la importación.

Para empezar, seleccione **[!UICONTROL Importar asignación]**.

![Imagen que muestra la variable [!UICONTROL Importar asignación] botón seleccionado](../images/datastreams/data-prep/import-mapping-button.png)

En el cuadro de diálogo que aparece, seleccione el conjunto de datos cuyas reglas de asignación desea importar. Una vez elegido el conjunto de datos, seleccione **[!UICONTROL Vista previa]**.

![Imagen que muestra un conjunto de datos existente seleccionado](../images/datastreams/data-prep/select-mapping-rules.png)

>[!NOTE]
>
>Los conjuntos de datos solo se pueden importar dentro de un mismo [entorno limitado](../../sandboxes/home.md). En otras palabras, no se puede importar un conjunto de datos de un entorno limitado a otro.

La siguiente pantalla muestra una vista previa de las reglas de asignación guardadas para el conjunto de datos seleccionado. Asegúrese de que las asignaciones mostradas sean las que espera y, a continuación, seleccione **[!UICONTROL Importar]** para confirmar y agregar las asignaciones al nuevo conjunto de datos.

![Imagen que muestra las reglas de asignación que se van a importar](../images/datastreams/data-prep/import-mapping-rules.png)

>[!NOTE]
>
>Si algún campo de origen de las reglas de asignación importadas no está incluido en los datos JSON de muestra que usted [proporcionado anteriormente](#select-data), esas asignaciones de campo no se incluirán en la importación.

### Complete la asignación

Siga los pasos anteriores para asignar el resto de los campos al esquema de destino. Aunque no es necesario asignar todos los campos de origen disponibles, cualquier campo del esquema de destino que esté configurado como necesario debe asignarse para completar este paso. La variable **[!UICONTROL Campos requeridos]** counter indica cuántos campos obligatorios aún no están asignados en la configuración actual.

Una vez que el recuento de campos requerido alcance cero y esté satisfecho con la asignación, seleccione **[!UICONTROL Guardar]** para finalizar los cambios.

![Asignación finalizada](../images/datastreams/data-prep/mapping-complete.png)

## Pasos siguientes

En esta guía se explica cómo asignar los datos a XDM al configurar un conjunto de datos en la interfaz de usuario. Si estaba siguiendo el tutorial de conjuntos de datos generales, ahora puede volver al paso [ver detalles del almacén de datos](./overview.md).
