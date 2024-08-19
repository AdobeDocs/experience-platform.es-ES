---
title: Acceso al ECID
description: Obtenga información sobre cómo acceder al ID de Experience Cloud desde la preparación de datos o las etiquetas
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e53ae6053a4b00e7e75242b95496c6795953005a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Acceso al ECID

[!DNL Experience Cloud Identity (ECID)] es un identificador persistente asignado a un usuario cuando visita su sitio web. En determinadas circunstancias, es posible que prefiera acceder a [!DNL ECID] (para enviarlo a un tercero, por ejemplo). Otro caso de uso es configurar [!DNL ECID] en un campo XDM personalizado, además de tenerlo en el mapa de identidad.

Puede acceder al ECID a través de [Preparación de datos para la recopilación de datos](../../../../datastreams/data-prep.md) (recomendado) o mediante etiquetas.

## Acceso al ECID a través de la preparación de datos (método preferido) {#accessing-ecid-data-prep}

Este método usa [preparación de datos para la recopilación de datos](../../../../datastreams/data-prep.md) para configurar una asignación personalizada para `ECID`.

Consulte la documentación de [Preparación de datos para la recopilación de datos](../../../../datastreams/data-prep.md) para aprender a utilizar esta función.

Si desea establecer el ECID en un campo XDM personalizado, además de tenerlo en el mapa de identidad, puede hacerlo estableciendo `source` en la siguiente ruta:

```js
xdm.identityMap.ECID[0].id
```

A continuación, establezca el destino en una ruta XDM donde el campo sea del tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Etiquetas

Si necesita acceder a [!DNL ECID] en el lado del cliente, utilice el método de etiquetas como se describe a continuación.

1. Asegúrese de que la propiedad esté configurada con la secuencia de componentes de regla [habilitada](../../../ui/managing-resources/rules.md#sequencing).
1. Cree una regla nueva. Esta regla debe usarse exclusivamente para capturar [!DNL ECID] sin ninguna otra acción importante.
1. Agregue un evento [!UICONTROL Library Loaded] a la regla.
1. Agregue una acción [!UICONTROL Custom Code] a la regla con el siguiente código (suponiendo que el nombre que configuró para la instancia del SDK es `alloy` y que aún no hay un elemento de datos con el mismo nombre):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Guarde la regla.

Debería poder tener acceso a [!DNL ECID] en reglas subsiguientes usando `%ECID%` o `_satellite.getVar("ECID")`, como lo haría con cualquier otro elemento de datos.
