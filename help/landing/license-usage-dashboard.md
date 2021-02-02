---
keywords: Experience Platform;interfaz de usuario;IU;personalización;panel de uso de licencia;panel;uso de licencia;asignación;consumo
title: Panel de uso de licencias
description: 'Esta guía describe el panel de uso de licencias disponible en la interfaz de usuario de Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 8e4d8d29ca13017d7f6de5ca790efe91b01c129d
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---


# (Alfa) [!UICONTROL Uso de licencias] panel {#license-usage-dashboard}

>[!IMPORTANT]
>
>La funcionalidad de panel descrita en este documento se encuentra actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (UI) de Adobe Experience Platform proporciona un panel a través del cual puede realizar vistas de información importante sobre el uso de licencias de su organización, tal como se obtiene durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el panel de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el panel.

Para obtener una descripción general de la interfaz de usuario de la plataforma, visite la [guía de la interfaz de usuario del Experience Platform](ui-guide.md).

## Datos del panel de uso de licencias

El panel de uso de licencias muestra una instantánea de los datos relacionados con las licencias de su organización para el Experience Platform. Los datos del panel se muestran exactamente como aparecen en el momento concreto en que se realizó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se realizó la instantánea no se reflejarán en el panel hasta que se realice la siguiente instantánea.

## Explorar el panel de uso de licencias

Para navegar hasta el panel de uso de licencias dentro de la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Uso de licencias]** en el carril izquierdo. Se abre con la ficha **[!UICONTROL Información general]** que muestra el panel.

![](images/license-usage-dashboard/dashboard-overview.png)

### Seleccionar un entorno limitado

Para elegir un entorno limitado para la vista en el panel, seleccione [!UICONTROL Producción] o [!UICONTROL Desarrollo]. El simulador para pruebas seleccionado se indica mediante el botón de opción situado junto al nombre del simulador para pruebas.

>[!NOTE]
>
>El sistema de informes de consumo para los entornos limitados es acumulativo para todos los entornos limitados del mismo tipo. En otras palabras, si selecciona [!UICONTROL Producción] o [!UICONTROL Desarrollo] se informará sobre todos los entornos limitados de producción o desarrollo, respectivamente.

![](images/license-usage-dashboard/select-sandbox.png)

### Seleccionar un intervalo de fechas

Después de seleccionar un simulador para pruebas, puede utilizar la lista desplegable de intervalos de fechas para seleccionar el período de tiempo que se mostrará en el panel. Hay tres opciones disponibles: [!UICONTROL Últimos 30 días], [!UICONTROL Últimos 90 días] y [!UICONTROL Últimos 12 meses]. Los últimos 30 días están seleccionados de forma predeterminada.

![](images/license-usage-dashboard/select-date-range.png)

### Widgets y métricas

El panel de uso de licencias está compuesto de utilidades, que muestran métricas de solo lectura que proporcionan información importante sobre el uso de licencias de su organización. Para obtener más información sobre estas utilidades, consulte la sección de utilidades disponibles en esta guía.

## Widgets disponibles {#available-widgets}

Actualmente, Experience Platform proporciona una utilidad que puede utilizar para visualizar el uso de la licencia, y pronto se lanzarán más utilidades.

### [!UICONTROL Audiencias direccionables] {#addressable-audiences}

La utilidad **[!UICONTROL audiencias direccionables]** muestra el número total de perfiles combinados dentro del almacén de datos de Perfil, después de aplicar una directiva de combinación generada por el sistema para combinar fragmentos de perfil de todos los conjuntos de datos actuales mediante un algoritmo de gráficos determinísticos (privados).

Para obtener más información sobre fragmentos y perfiles combinados, lea la sección *fragmentos de Perfil vs. perfiles combinados* de la [información general de Perfil](../profile/home.md).

>[!NOTE]
>
>La directiva de combinación utilizada para calcular esta métrica la genera el Experience Platform y no se puede editar, ni se puede seleccionar una directiva de combinación diferente. Esta directiva de combinación generada por el sistema no es la misma que la directiva de combinación predeterminada utilizada para calcular [!UICONTROL tamaño de Audiencia] en el panel [!DNL Profile], por lo tanto es poco probable que el recuento de audiencias de los paneles [!UICONTROL Uso de licencias] y [!DNL Profile] sea exactamente el mismo.

![](images/license-usage-dashboard/addressable-audiences.png)

## Paneles adicionales

La interfaz de usuario de la plataforma proporciona paneles adicionales para ver instantáneas de los datos en Experience Platform. Estos paneles incluyen Perfiles y segmentos de clientes en tiempo real. Para obtener más información sobre estos paneles, seleccione uno de los vínculos siguientes:

* [[!DNL Profile] panel](../profile/ui/profile-dashboard.md)
* [Panel de segmentos](../segmentation/ui/segment-dashboard.md)

## Pasos siguientes

Siguiendo este documento, debería poder localizar el panel de uso de la licencia y seleccionar un simulador para la vista. También debe comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre la interfaz de usuario del Experience Platform, consulte la [guía de la interfaz de usuario de la plataforma](ui-guide.md).