---
title: Configuración de la compatibilidad con la mensajería web en la aplicación en el SDK web
description: Obtenga información sobre cómo configurar la extensión de etiqueta del SDK web para admitir la mensajería en la aplicación web.
exl-id: 90a19ef4-e94c-4f16-a26a-8919ad2dbd6f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---

# Configuración de la compatibilidad con la mensajería web en la aplicación en el SDK web

Los mensajes en la aplicación son notificaciones que puede enviar a los usuarios dentro de su aplicación web, guiándolos a puntos de interés específicos.

Puede utilizar estas notificaciones para diferentes fines, como promocionar nuevas funciones, presentar ofertas especiales o facilitar la incorporación del usuario.

Con los mensajes en la aplicación, puede interactuar de forma eficaz con su audiencia y dirigirla a aspectos importantes de su aplicación.

>[!IMPORTANT]
>
>La mensajería web en la aplicación es una característica de [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es) que usa el SDK web para entregar el contenido personalizado.
>
>Para obtener instrucciones detalladas sobre cómo configurar su campaña de mensajería en la aplicación web, consulte la [documentación de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Requisitos previos {#prerequisites}

### Versión de extensión de etiqueta de SDK web {#extension-version}

La funcionalidad de mensajería en la aplicación web requiere la última versión de la extensión de etiqueta del SDK web.

### Configuración de un CSP para mensajería web en la aplicación {#csp}

Al configurar [Mensajería en la aplicación web](../personalization/web-in-app-messaging.md), debe incluir la siguiente directiva en su CSP:

```
default-src  blob:;
```

Para obtener más información acerca de cómo configurar un CSP, consulte la [documentación dedicada](../use-cases/configuring-a-csp.md).

## Configuración de la mensajería web en la aplicación mediante la extensión de etiqueta del SDK web {#tag-extension}

Consulte la [página de configuración de la extensión de etiquetas del SDK web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para saber dónde puede encontrar la configuración que se describe a continuación.

Después de haber [instalado](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) la extensión de etiqueta del SDK web, siga los pasos a continuación para configurar la extensión para la mensajería web en la aplicación.

En la sección **[!UICONTROL Personalization]**, marque la opción **[!UICONTROL Habilitar almacenamiento personalizado]**. Esta opción permite al SDK web realizar un seguimiento de las experiencias que el usuario ha visto en las cargas de página.

![Imagen que muestra la opción de almacenamiento personalizado en la página de configuración de la extensión de etiqueta.](assets/web-in-app-messaging/enable-personalization-storage.png)


La mensajería web en la aplicación admite dos tipos de déclencheur:

* [Envío de datos a Platform](#send-data-platform)
* [Activación manual de mensajes](#manual-trigger)

Consulte las secciones siguientes para configurar la extensión de etiquetas del SDK web según los déclencheur que desee utilizar.

### Pasos de configuración para el déclencheur **[!UICONTROL Enviar datos a la plataforma]** {#send-data-platform}

Seleccione la propiedad de etiqueta que contiene su extensión del SDK web y [cree una nueva regla](../../tags/ui/managing-resources/rules.md##create-a-rule) con la siguiente configuración:

1. **[!UICONTROL Extensión]**: [!UICONTROL Principal]
2. **[!UICONTROL Tipo de evento]**: [!UICONTROL Biblioteca cargada (Principio de página)]

   ![Imagen que muestra la pantalla de configuración del evento.](assets/web-in-app-messaging/rule-configuration.png)

3. Seleccione **[!UICONTROL Conservar cambios]** para guardar la configuración del evento.

A continuación, debe agregar una acción a la regla que ha creado.

1. En la sección [!DNL Actions], seleccione **[!UICONTROL Agregar]**.
   ![Imagen que muestra la pantalla de edición de regla.](assets/web-in-app-messaging/add-action.png)

2. Usar la siguiente configuración de **[!UICONTROL Acción]**:
   * **[!UICONTROL Extensión]**: [!UICONTROL SDK web de Adobe Experience Platform]
   * **[!UICONTROL Tipo de acción]**: [!UICONTROL Enviar evento]

     ![Imagen que muestra la pantalla de configuración de la acción.](assets/web-in-app-messaging/action-configuration.png)

3. En el lado derecho de la pantalla, en la sección **[!UICONTROL Personalization]**, habilite la opción **[!UICONTROL Procesar decisiones de personalización visuales]**.
   ![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/render-visual-personalization.png)

4. En el lado derecho de la pantalla, en la sección **[!UICONTROL Contexto de decisión]**, defina los pares de **[!UICONTROL Clave]**/**[!UICONTROL Valor]** que utilizó en la configuración de su campaña para cumplir los requisitos para el mensaje en la aplicación.
   ![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/decision-context.png)

5. Seleccione **[!UICONTROL Conservar cambios]** para guardar la configuración.


A continuación, debe agregar la regla recién creada a la biblioteca de propiedades de etiquetas. Para ello, vaya a **[!UICONTROL Flujo de publicación]** y seleccione la regla que creó anteriormente.

![Imagen que muestra la pantalla de la biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Después de agregar la regla a la biblioteca, seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/publish-flow.png)

El proceso de configuración se ha completado y el mensaje está listo para mostrarse a los usuarios.

### Pasos de configuración para utilizar déclencheur manuales {#manual-trigger}

Seleccione la propiedad de etiqueta que contiene su extensión del SDK web y [cree una nueva regla](../../tags/ui/managing-resources/rules.md##create-a-rule) con la siguiente configuración:

1. **[!UICONTROL Extensión]**: [!UICONTROL Principal]
2. **[!UICONTROL Tipo de evento]**: [!UICONTROL Haga clic]
3. Establezca el déclencheur de un elemento específico de la página, identificado por un selector CSS de su elección.

   ![Imagen que muestra la pantalla de configuración del evento.](assets/web-in-app-messaging/event-configuration-manual.png)


A continuación, debe agregar una acción a la regla que ha creado.

1. En la sección [!DNL Actions], seleccione **[!UICONTROL Agregar]**.
   ![Imagen que muestra la pantalla de edición de regla.](assets/web-in-app-messaging/add-action.png)

2. Usar la siguiente configuración de **[!UICONTROL Acción]**:
   * **[!UICONTROL Extensión]**: [!UICONTROL SDK web de Adobe Experience Platform]
   * **[!UICONTROL Tipo de acción]**: [!UICONTROL Evaluar conjuntos de reglas]

     ![Imagen que muestra la pantalla de configuración de la acción.](assets/web-in-app-messaging/manual-trigger-action.png)

3. En el lado derecho de la pantalla, habilite la opción **[!UICONTROL Procesar decisiones de personalización visuales]**.
   ![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/manual-trigger-render.png)


4. En el lado derecho de la pantalla, en la sección **[!UICONTROL Contexto de decisión]**, defina los pares de **[!UICONTROL Clave]**/**[!UICONTROL Valor]** que utilizó en la configuración de su campaña para cumplir los requisitos para el mensaje en la aplicación.
   ![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Seleccione **[!UICONTROL Conservar cambios]** para guardar la configuración.

A continuación, debe agregar la regla recién creada a la biblioteca de propiedades de etiquetas. Para ello, vaya a **[!UICONTROL Flujo de publicación]** y seleccione la regla que creó anteriormente.

![Imagen que muestra la pantalla de la biblioteca.](assets/web-in-app-messaging/add-rule-to-library.png)

Después de agregar la regla a la biblioteca, seleccione **[!UICONTROL Guardar y generar en desarrollo]**.

![Imagen que muestra la pantalla de configuración de personalización.](assets/web-in-app-messaging/publish-flow.png)

El proceso de configuración se ha completado y el mensaje está listo para mostrarse a los usuarios.

## Configuración de la mensajería web en la aplicación mediante la biblioteca JavaScript del SDK web {#js-library}

Como alternativa al uso de la extensión de etiqueta del SDK web, también puede configurar la mensajería en la aplicación web directamente desde la biblioteca de JavaScript del SDK web.



Puede mostrar mensajes web en la aplicación desde Adobe Journey Optimizer de dos formas.

### Método 1: Recuperación automática del contenido personalizado {#automatic}

Para que el SDK web recupere automáticamente el contenido de personalización al cargar la página, utilice el comando `sendEvent`, como se muestra en el ejemplo siguiente.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Método 2: Recuperación manual del contenido de personalización en función de la acción del usuario {#manual}

Para mostrar el contenido personalizado solo después de que el usuario realice una acción específica, utilice el comando `evaluateRulesets` como se muestra en el ejemplo siguiente.

En este ejemplo, el contenido de personalización se muestra cuando un usuario hace clic en el botón **[!UICONTROL Comprar ahora]** del sitio web.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Configuración del almacenamiento de personalización {#personalization-storage}

Puede elegir mostrar mensajes en la aplicación a los usuarios una cantidad determinada de veces, o cada vez que visiten una página, mediante la opción de configuración `personalizationStorageEnabled`.

En la [configuración del SDK web](../commands/configure/overview.md) establezca la opción `personalizationStorageEnabled` según sus necesidades:

* `personalizationStorageEnabled: true` almacena en déclencheur el mensaje en la aplicación con la frecuencia que definió en [Adobe Journey Optimizer campaign](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` almacena en déclencheur el mensaje en la aplicación en cada carga de página.
