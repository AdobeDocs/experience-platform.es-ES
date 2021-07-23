---
title: Envío de datos a Adobe Analytics mediante el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web de Adobe Experience Platform.
keywords: adobe analytics;analytics;datos asignados;vars asignados;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---

# Envío de datos a Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] puede enviar datos a Adobe Analytics. Esto funciona traduciendo `xdm` a un formato que Adobe Analytics puede utilizar.

## Configuración

Adobe Analytics recopila automáticamente los datos que envía si tiene un grupo de informes asignado en la interfaz de usuario de configuración del cliente. Aquí puede asignar uno o más informes a una configuración determinada. Una vez asignado un grupo de informes, los datos empezarán a fluir automáticamente.

## Datos asignados automáticamente

Adobe Experience Platform [!DNL Edge Network] asigna automáticamente muchas variables XDM. La lista completa de estas variables se enumera [aquí](automatically-mapped-vars.md).

## Datos asignados manualmente

Se puede acceder a todos los datos recopilados por la red perimetral mediante reglas de procesamiento. Los datos se acoplan con notación de puntos y están disponibles como contextData.

Si tenía un esquema similar a este.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Estas serían las claves de datos de contexto disponibles para usted.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

A continuación, se muestra un ejemplo de una regla de procesamiento que utilizaría estos datos.

![Interfaz de reglas de procesamiento](./assets/edge_analytics_processing_rules.png)
