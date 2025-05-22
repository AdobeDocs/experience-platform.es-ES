---
title: Instalación de Web SDK mediante el paquete NPM
description: Utilice un paquete NPM para instalar y hacer referencia a la biblioteca Web SDK.
exl-id: 4c70ec5d-33fd-4ef7-ba9e-5b92ff6c3e86
source-git-commit: 8b6c958613923127880263679ce00ce359151300
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Instalación de Web SDK mediante el paquete NPM

Adobe Experience Platform Web SDK está disponible como [paquete NPM](https://www.npmjs.com). La instalación del paquete NPM permite controlar el proceso de compilación de la biblioteca JavaScript de Adobe Experience Platform Web SDK. El paquete NPM expone módulos EcmaScript versión 5 o módulos EcmaScript versión 2015 (ES6) pensados para ejecutarse en el navegador.

```bash
npm install @adobe/alloy
```

El paquete NPM de Adobe Experience Platform Web SDK expone una función `createInstance`. La opción de nombre pasada a la función controla el prefijo utilizado en el registro. A continuación se muestran ejemplos de uso del paquete.

## Uso del paquete como módulo ECMAScript 2015 (ES6)

```js
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>El paquete NPM se basa en módulos CommonJS; por lo tanto, cuando utilice un paquete, asegúrese de que el paquete admita módulos CommonJS. Algunos paquetes, como [Rollup](https://rollupjs.org), requieren un [complemento](https://www.npmjs.com/package/@rollup/plugin-commonjs) que proporcione compatibilidad con CommonJS.

## Uso del paquete como módulo ECMAScript 5

```js
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("configure", { ... });
alloy("sendEvent", { ... });
```
