---
title: Extensión de SDK web de Adobe Experience Platform Información general
description: Obtenga información sobre Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 53%

---


# Información general sobre la extensión del SDK web de Adobe Experience Platform

Adobe Experience Platform Web SDK Extension envía datos al Adobe Experience Cloud desde las propiedades web, a través de Adobe Experience Platform Edge Network. La extensión SDK para web de Adobe Experience Platform permite la transmisión de datos a la plataforma, la sincronización de identidades, la inclusión y la recopilación automática de datos de contexto.

## Configurar la extensión de

Esta sección proporciona una referencia sobre las opciones disponibles al configurar la extensión SDK para web de Adobe Experience Platform.

Si la extensión del SDK web de Adobe Experience Platform aún no está instalada, abra la propiedad y, a continuación, seleccione **[!UICONTROL Extensiones > Catálogo]**, pase el ratón sobre la extensión del SDK web de Adobe Experience Platform y seleccione **[!UICONTROL Instalar]**.

Para configurar la extensión, abra la ficha **[!UICONTROL Extensiones]**, pase el ratón sobre la extensión y seleccione **[!UICONTROL Configurar]**.

![](./assets/ext-aep-config.png)

### Nombre de la instancia

La extensión Adobe Experience Platform Web SDK admite varias instancias en la página. Se utiliza para enviar datos a varias organizaciones con una sola configuración de Adobe Experience Platform Launch. El **[!UICONTROL Nombre]** toma el valor predeterminado de aleación. Sin embargo, puede cambiar el nombre de la instancia a cualquier nombre de objeto JavaScript válido. La extensión de Adobe Experience Platform requiere que cada instancia tenga un **[!UICONTROL ID de configuración]** diferente y un **[!UICONTROL ID de organización]** diferente.

## **[!UICONTROL Id. de configuración]**

El **[!UICONTROL ID de configuración]** es lo que indica a Adobe Experience Platform dónde se deben enrutar los datos y qué configuraciones se deben usar en el servidor. Esto es necesario para que funcione la extensión de Adobe Experience Platform. Puede obtener un ID de configuración poniéndose en contacto con el servicio de atención al cliente.


### **[!UICONTROL ID de organización]**

El **[!UICONTROL identificador de organización]** es la organización a la que desea que se envíen los datos en el Adobe. La mayoría de las veces, debe utilizar el valor predeterminado que se propaga automáticamente. Cuando tenga varias instancias en la página, rellénelas con el valor de la segunda organización a la que desee enviar datos.

### **[!UICONTROL Dominio de Edge]**

El **[!UICONTROL Dominio de Edge]** es el dominio desde el que la extensión de Adobe Experience Platform envía y recibe datos. La extensión requiere que utilice un CNAME de origen para el tráfico de producción. El dominio de terceros predeterminado funciona para entornos de desarrollo, pero no es adecuado para entornos de producción. Las instrucciones sobre cómo configurar un CNAME de origen se enumeran [aquí](https://docs.adobe.com/content/help/es-ES/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Habilitar errores]**

De forma predeterminada, si hay un error con la extensión, se registra el error en la consola. Si desea ocultar los errores en un entorno de producción, puede desmarcar la casilla **[!UICONTROL Habilitar errores]**. Los errores se seguirán mostrando cuando la depuración esté activada en Platform Launch.

### **[!UICONTROL Habilitar inclusión]**

Si **[!UICONTROL Habilitar inclusión]** está habilitado, la extensión puede retener visitas hasta que se reciba la inclusión. La extensión muestra un cuadro de diálogo para establecer las preferencias de inclusión.

### **[!UICONTROL Habilitar Migrar ECID]**

La extensión del SDK web de plataforma utiliza una nueva cookie para almacenar el ECID. Esta configuración habilita la compatibilidad entre la nueva cookie y la cookie antigua para fines de migración. Adobe recomienda habilitar esta opción, a menos que no tenga visitantes con un ECID.

### **[!UICONTROL Usar cookies de terceros]**

Adobe Experience Platform siempre almacenará una cookie en el dominio de origen. Esta opción le permite utilizar una cookie de terceros definida en demdex.net además de la cookie en el dominio de origen. Esto puede resultar útil cuando hay usuarios que se trasladan de un dominio a otro. Esto deshabilitará las llamadas a demdex.net.

### **[!UICONTROL Contexto]**

La extensión recopila automáticamente información sobre el contexto de la solicitud (por ejemplo, detalles sobre la URL y el explorador). Esto se puede desactivar si se anula la selección de contextos específicos.

- **[!UICONTROL web]** : detalles sobre la página web como url, remitente del reenvío, etc.
- **[!UICONTROL dispositivo]** : detalles sobre el dispositivo, como la orientación de la pantalla, la altura de la pantalla y la anchura de la pantalla.
- **[!UICONTROL entorno]** : información sobre el entorno informático (explorador, conexión, etc.)
- **[!UICONTROL ubicación]** : información limitada sobre la ubicación del usuario

## Qué sigue

1. Configure [tipos de acción](action-types.md).
2. Configure [tipos de elementos de datos](data-element-types.md).
