---
title: Acceso al ECID
description: Obtenga información sobre cómo acceder al ID de Experience Cloud desde la preparación de datos o las etiquetas
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---


# Acceso al ECID

El [!DNL Experience Cloud Identity (ECID)] es un identificador persistente asignado a un usuario cuando visita su sitio web. En determinadas circunstancias, es posible que prefiera acceder a [!DNL ECID] (para enviarlo a un tercero, por ejemplo). Otro caso de uso es la configuración de [!DNL ECID] en un campo XDM personalizado, además de tenerlo en el mapa de identidad.

Puede acceder al ECID a través de [Preparación de datos para la recopilación de datos](../../../../datastreams/data-prep.md) (recomendado) o mediante etiquetas.

## Acceso al ECID a través de la preparación de datos (método preferido) {#accessing-ecid-data-prep}

Si desea establecer el ECID en un campo XDM personalizado, además de tenerlo en el mapa de identidad, puede hacerlo estableciendo el `source` a la siguiente ruta:

```js
xdm.identityMap.ECID[0].id
```

A continuación, establezca el objetivo en una ruta XDM donde el campo sea del tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Etiquetas

Si necesita acceder a la [!DNL ECID] en el lado del cliente, utilice el método de etiquetas como se describe a continuación.

1. Asegúrese de que la propiedad esté configurada con [Secuencia de componentes de regla](../../../ui/managing-resources/rules.md#sequencing) activado.
1. Cree una regla nueva. Esta regla debe utilizarse exclusivamente para capturar el [!DNL ECID] sin ninguna otra acción importante.
1. Añadir un [!UICONTROL Library Loaded] a la regla.
1. Añadir un [!UICONTROL Código personalizado] acción a la regla con el siguiente código (suponiendo que el nombre configurado para la instancia del SDK sea `alloy` y no hay ningún elemento de datos (del mismo nombre):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Guarde la regla.

A continuación, debería poder acceder a la [!DNL ECID] en reglas subsiguientes utilizando `%ECID%` o `_satellite.getVar("ECID")`, como si tuviera acceso a cualquier otro elemento de datos.
