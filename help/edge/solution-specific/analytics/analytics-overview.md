---
title: Envío de datos a Adobe Analytics
seo-title: Envío de datos a Adobe Analytics con el SDK web de Adobe Experience Platform
description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web Experience Platform
seo-description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Envío de datos a Adobe Analytics

El Adobe Experience Platform [!DNL Web SDK] puede enviar datos a Adobe Analytics. Esto funciona traduciendo `xdm` a un formato que el Adobe Analytics puede utilizar.

## Configuración

Adobe Analytics recopila automáticamente los datos que envía si tiene un grupo de informes asignado en la interfaz de usuario de configuración del cliente. Aquí puede asignar uno o más sistemas de informes a una configuración determinada. Una vez asignado un grupo de informes, los datos empezarán a fluir automáticamente.

## Datos asignados automáticamente

El Adobe Experience Platform [!DNL Edge Network] asigna automáticamente muchas variables XDM. La lista completa de las variables asignadas automáticamente aparece [aquí](../analytics/automatically-mapped-vars.md).

## Datos asignados manualmente

Se puede acceder a todos los datos recopilados por la red Edge mediante reglas de procesamiento. Los datos se acoplan con notación de puntos y están disponibles como contextData.

Si tuvieras un esquema así.

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

A continuación, estas serían las claves de datos de contexto disponibles para usted.

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

Este es un ejemplo de una regla de procesamiento que utilizaría estos datos.

![Interfaz de reglas de procesamiento](../../../assets/edge_analytics_processing_rules.png)
