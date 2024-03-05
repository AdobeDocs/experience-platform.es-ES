---
title: Instalación del SDK web mediante el paquete NPM
description: Utilice un paquete NPM para instalar y hacer referencia a la biblioteca del SDK web.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# Instalación del SDK web mediante el paquete NPM

El SDK web de Adobe Experience Platform está disponible como [Paquete NPM](https://www.npmjs.com). La instalación del paquete NPM permite controlar el proceso de compilación de la biblioteca JavaScript del SDK web de Adobe Experience Platform. El paquete NPM expone módulos EcmaScript versión 5 o módulos EcmaScript versión 2015 (ES6) pensados para ejecutarse en el navegador.

```bash
npm install @adobe/alloy
```

El paquete NPM del SDK web de Adobe Experience Platform expone un `createInstance` función. La opción de nombre pasada a la función controla el prefijo utilizado en el registro. A continuación se muestran ejemplos de uso del paquete.

## Uso del paquete como módulo ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>El paquete NPM se basa en módulos CommonJS; por lo tanto, cuando utilice un paquete, asegúrese de que el paquete admita módulos CommonJS. Algunos paquetes, como [Resumen](https://rollupjs.org), requiere un [plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs) que proporciona compatibilidad con CommonJS.

## Uso del paquete como módulo ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```
