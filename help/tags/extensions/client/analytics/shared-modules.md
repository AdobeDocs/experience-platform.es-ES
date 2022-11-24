---
title: Módulos compartidos para la extensión Adobe Analytics
description: Obtenga información acerca de los módulos de biblioteca compartidos que proporciona la extensión de etiqueta de Adobe Analytics en Adobe Experience Platform.
exl-id: f1d7cb2b-0058-46f9-983c-079079e06057
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 95%

---

# Módulos compartidos para la extensión Adobe Analytics

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La [extensión de Adobe Analytics](./overview.md) proporciona dos [módulos compartidos](../../../extension-dev/web/shared.md) diferentes que puede integrar en la aplicación de experiencia. Estos módulos se tratan en las secciones siguientes.

## [!DNL get-tracker]

Antes de que Adobe Analytics envíe señalizaciones, debe inicializar el objeto tracker. El proceso de inicialización comienza cargando [AppMeasurement](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es), seguido de la creación de un objeto tracker.

Puede acceder al objeto tracker después de inicializarlo completamente mediante el módulo compartido `get-tracker` de la siguiente manera:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

getTracker().then(function(tracker) {
  // Use tracker in some way
});
```

### Verificación de la instalación de Adobe Analytics

Es posible que Adobe Analytics no se haya instalado o incluido en la misma biblioteca de etiquetas que la extensión. Debido a esto, es muy recomendable que verifique este caso en su código y lo gestione correctamente. El siguiente JavaScript es un ejemplo de cómo se puede implementar esto:

```js
var getTracker = turbine.getSharedModule('adobe-analytics', 'get-tracker');

if (getTracker) {
  getTracker().then(function(tracker) {
    // Use tracker in some way
  });
} else {
  turbine.logger.error("The Adobe Analytics extension is required for Extension XYZ to function properly.");
}
```

Si `getTracker` es `undefined`, la extensión de Adobe Analytics no existe en la biblioteca de etiquetas. Puede personalizar el mensaje registrado para que refleje con precisión qué funcionalidad se puede perder si Adobe Analytics no está instalado.


## [!DNL augment-tracker]

Una vez inicializado el objeto tracker, el siguiente paso en el proceso es el aumento. Este paso permite que su extensión aumente el rastreador con todo lo necesario antes de que se haya aplicado alguna variable desde la configuración de la extensión de Adobe Analytics o antes de que se haya enviado alguna baliza.

Además, la extensión tiene la oportunidad de pausar el proceso de inicialización del rastreador mientras la extensión realiza cualquier tarea asincrónica propia, como recuperar datos o JavaScript desde un servidor.

Puede implementar el módulo `augment-tracker` de esta manera:

```js
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  // Augment tracker in some way
});
```

La función pasada a `augmentTracker()` se invocará en cuanto se alcance la fase de aumento del proceso de inicialización del rastreador.

Si la extensión necesita completar una tarea asincrónica antes de aumentar el rastreador, puede devolver una promesa de su función de la siguiente manera:

```js
var Promise = require('@adobe/reactor-promise');
var augmentTracker = turbine.getSharedModule('adobe-analytics', 'augment-tracker');

augmentTracker(function(tracker) {
  return new Promise(function(resolve) {
    // Augment the tracker object, then call resolve()
  });
});
```

Al devolver una promesa, la extensión le indica a Adobe Analytics que debe pausar el proceso de inicialización del rastreador hasta que se resuelva la promesa.

>[!WARNING]
>
>Tenga cuidado al pausar el proceso de inicialización del rastreador, ya que puede retrasar el envío de las balizas y, por lo tanto, generar datos no recopilados (por ejemplo, si el usuario sale de la página antes de que se envíe la baliza).
