---
title: Uso de Adobe Analytics con el SDK web de Platform
description: Obtenga información sobre cómo enviar datos a Adobe Analytics con el SDK web de Adobe Experience Platform.
keywords: adobe analytics;analytics;datos asignados;variables asignadas;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Uso de Adobe Analytics con el SDK web de Platform

El Adobe Experience Platform [!DNL Web SDK] puede enviar datos a Adobe Analytics. Esto funciona traduciendo `xdm` en un formato que Adobe Analytics pueda utilizar.

## Configuración

Adobe Analytics recoge automáticamente los datos que envía si tiene un grupo de informes asignado en la interfaz de usuario de configuración del cliente. Aquí puede asignar uno o más informes a una configuración determinada. Una vez asignado un grupo de informes, los datos comenzarán a fluir automáticamente.

## Grupo de campos XDM

Para facilitar la captura de las métricas de Adobe Analytics más comunes, proporcionamos un grupo de campos de Analytics que puede utilizar. Para obtener más información sobre este esquema, consulte la documentación del [Grupo de campos de esquema de extensión completa de Adobe Analytics ExperienceEvent](../../../xdm/field-groups/event/analytics-full-extension.md)

## Datos asignados automáticamente

El Adobe Experience Platform [!DNL Edge Network] asigna automáticamente muchas variables XDM. Se muestra la lista completa de estas variables [aquí](automatically-mapped-vars.md).

## Datos asignados manualmente

Los datos que no estén asignados automáticamente por el [!DNL Edge Network] se puede acceder a través de reglas de procesamiento. Los datos se acoplan con notación de puntos y están disponibles como contextData.

Si tuviera un esquema con este aspecto.

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

Este es un ejemplo de regla de procesamiento que utilizaría estos datos.

![Interfaz de reglas de procesamiento](./assets/edge_analytics_processing_rules.png)

>[!NOTE]
>
>Con la colección Edge Network, todos los eventos se envían a Analytics, así como a cualquier otro servicio que haya configurado para su flujo de datos. Por ejemplo, si tiene Analytics y Target configurados como servicios y realiza llamadas independientes para la personalización y para Analytics, ambos eventos se enviarán a Analytics y a Target. Estos eventos se registrarán en los informes de Analytics y pueden afectar a métricas como la tasa de salida hacia otro sitio.
