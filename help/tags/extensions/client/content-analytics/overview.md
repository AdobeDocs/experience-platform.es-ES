---
title: Información general sobre la extensión Adobe Content Analytics
description: Obtenga información acerca de la extensión de etiquetas Adobe Content Analytics en Adobe Experience Platform.
exl-id: fcc46c86-e765-4bc7-bfdf-b8b10e8afacc
source-git-commit: 415b02ecd28946c965bd3d7d3ff9efdc7d2f313f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Información general sobre la extensión Adobe Content Analytics

La extensión de etiqueta [!DNL Adobe Content Analytics] permite el seguimiento de eventos relacionados con contenido en un sitio web. La extensión envía datos de contenido (experiencias y recursos) a un conjunto de datos en Adobe Experience Cloud desde propiedades web a través de Experience Platform Edge Network.

La extensión le permite transmitir datos de evento específicos relacionados con contenido a Experience Platform para que pueda utilizar esos datos en los informes de análisis de contenido en Customer Journey Analytics.

En este documento se explica cómo configurar la extensión de etiqueta en la interfaz de usuario de Etiquetas.

## Instalación de la extensión de etiquetas de Adobe Content Analytics {#install}

La extensión de etiquetas de Adobe Content Analytics se instala automáticamente como parte de la propiedad de etiquetas que se crea automáticamente al usar el [asistente de configuración guiada de Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided).

<!--
### Manual installation

In case of a manual configuration, the Adobe Content Analytics tag extension needs a property to be installed on. If you have not done so already, see the documentation on [creating a tag property](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/create-a-property).

After you have created a property or when you select the property created using the [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided), open the property and select the **[!UICONTROL Extensions]** tab on the left side bar.

Select the **[!UICONTROL Catalog]** tab. From the list of available extensions, find the **[!DNL Adobe Content Analytics]** extension and select **[!UICONTROL Install]**.

![Image showing the Tags UI with the Web SDK extension selected](assets/aca-tag-install.png)

After selecting **[!UICONTROL Install]**, you must configure the Adobe Content Analytics tag extension and save the configuration.
-->

<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## Configuración de flujos de datos

El [asistente de configuración guiada de Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) selecciona automáticamente el valor adecuado para **[!UICONTROL espacio aislado]** y **[!UICONTROL secuencia de datos de producción]**. Opcionalmente, puede configurar una secuencia de datos de ensayo **[!UICONTROL adicional]** y una secuencia de datos de desarrollo **[!UICONTROL 3&rbrace;.]**

![Imagen que muestra la configuración de flujos de datos de la extensión de etiquetas de Adobe Content Analytics en la interfaz de usuario de etiquetas](assets/aca-tag-datastreams.png)

Puede anular los valores seleccionados automáticamente para **[!UICONTROL espacio aislado]** y **[!UICONTROL secuencia de datos de producción]** en caso de que desee usar Content Analytics en un espacio aislado diferente y con flujos de datos diferentes. Al hacerlo, puede seleccionar una zona protegida y flujos de datos en los menús desplegables disponibles, o seleccionar **[!UICONTROL Introducir valores]** e introducir un ID de flujo de datos personalizado para cada entorno.

>[!IMPORTANT]
>
>Al configurar otra zona protegida y flujos de datos, asegúrese de que
>
>* la zona protegida seleccionada no está ya asociada a otra configuración de Content Analytics, y
>* cualquier flujo de datos seleccionado tiene el servicio Experience Platform configurado con un conjunto de datos de evento de experiencia de Content Analytics habilitado.

Consulte la guía de [flujos de datos](../../../../datastreams/overview.md) para obtener información sobre cómo configurar un flujo de datos.

## Configurar la captura y definición de experiencias

En la sección **[!UICONTROL Captura y definición de experiencias]**, puede habilitar **[!UICONTROL Incluir experiencias]** para incluir experiencias al recopilar datos para Content Analytics.

![Imagen que muestra la sección Captura de experiencias y definición en la extensión](assets/aca-tag-experiencecapture.png)

1. Habilitar **[!UICONTROL Incluir experiencias]**.
1. Opcionalmente. especifique los parámetros de cómo se procesa el contenido en el sitio web. Los parámetros son cero o más combinaciones de una **[!UICONTROL expresión regular de dominio]** y **[!UICONTROL parámetros de consulta]**.
   1. Escriba una **[!UICONTROL expresión regular de dominio]**, por ejemplo `^(?!.*\b(store|help|admin)\b)`.
   1. Especifique una lista separada por comas de **[!UICONTROL parámetros de consulta]**, por ejemplo `outdoors, patio, kitchen`.
Use ![Cerrar](./assets/CrossSize300.svg) para eliminar parámetros individuales o **[!UICONTROL Borrar todo]** para eliminar todos los parámetros.
1. Seleccione **[!UICONTROL Remove]** si desea quitar una combinación de parámetros de consulta y expresión regular de dominio.
1. Seleccione **[!UICONTROL Agregar regex]** si desea agregar otra combinación de una expresión regular y parámetros de consulta.

## Configuración del filtrado de eventos

En la sección **[!UICONTROL Filtrado de eventos]**, puede modificar las expresiones regulares para filtrar **[!UICONTROL URL de la página]** y **[!UICONTROL URL de Assets]** al recopilar datos para Content Analytics. Las expresiones regulares definidas en el [asistente de configuración guiada de Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) se rellenan automáticamente.

![Imagen que muestra la configuración de filtrado de eventos de la extensión de etiquetas Adobe Content Analytics en la interfaz de usuario de etiquetas](assets/aca-tag-eventfiltering.png)


### Ejemplos

* Desea excluir todas las páginas de documentación de Content Analytics.<br/>Use la siguiente expresión regular: `^(?!.*documentation).*`
* Desea excluir todas las imágenes de logotipo de JPEG de Content Analytics.<br/>Use la siguiente expresión regular: `^(?!.*(logo\.jpg|)).*$`

Puede usar **[!UICONTROL Test Regex]** para probar su expresión regular en el **[!UICONTROL Probador de expresiones regulares]**.

![Imagen que muestra el comprobador de expresión regular de la extensión de etiquetas Adobe Content Analytics en la interfaz de usuario de etiquetas](assets/aca-tag-regextester.png)

