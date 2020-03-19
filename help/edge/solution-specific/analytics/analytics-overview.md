---
title: Envío de datos a Adobe Analytics
seo-title: Envío de datos a Adobe Analytics con el SDK web de la plataforma Adobe Experience
description: Descubra cómo enviar datos a Adobe Analytics con el SDK web de la plataforma de experiencia
seo-description: Descubra cómo enviar datos a Adobe Analytics con el SDK web de la plataforma de experiencia
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Envío de datos a Adobe Analytics

>[!IMPORTANT]
>
>El SDK web de la plataforma de experiencia de Adobe se encuentra en fase beta y no está disponible para todos los usuarios. La documentación y la funcionalidad están sujetas a cambios.

El SDK web de Adobe Experience Platform puede enviar datos a Adobe Analytics. Esto funciona traduciendo `xdm` a un formato que Adobe Analytics puede utilizar.

## Configuración

Adobe Analytics recopila automáticamente los datos que envía si tiene un grupo de informes asignado en la interfaz de usuario de configuración del cliente. Aquí puede asignar uno o más informes a una configuración determinada. Una vez asignado un grupo de informes, los datos empezarán a fluir automáticamente.

## Datos asignados automáticamente

Adobe Experience Platform Edge Network asigna automáticamente muchas variables XDM. La lista completa de variables asignadas automáticamente se muestra [aquí](../analytics/automatically-mapped-vars.md).

## Datos asignados manualmente

Se puede acceder a todos los datos recopilados por la red Edge mediante reglas de procesamiento. Los datos se acoplan con notación de puntos y están disponibles como contextData.

Si tuviera un esquema que se viera así.

```javascript
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    v1,
    v2,
    v3
  ],
  arrayofobjects:[
    {
      obj1key:objval1
    },
    {
      obj2key:objval2
    }
  ]
}
```

A continuación, estas serían las claves de datos de contexto disponibles para usted.

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array[0] //v1
a.x.array[1] //v2
a.x.array[3] //v3
a.x.arrayofobjects[1].obj1key //objval1
a.x.arrayofobjects[2].obj2key //objval2
```

Este es un ejemplo de una regla de procesamiento que utilizaría estos datos.

![Interfaz de reglas de procesamiento](../../../assets/edge_analytics_processing_rules.png)
