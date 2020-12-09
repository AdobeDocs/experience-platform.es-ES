---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Panel perfil
description: 'Esta guía describe el panel de datos de Perfil del cliente en tiempo real disponible en la interfaz de usuario de Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 983b357f2f17aad273f0465dc9250240a062dcd2
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# (Alfa) [!DNL Real-time Customer Profile] panel {#profile-dashboard}

>[!IMPORTANT]
>
>La funcionalidad de panel descrita en este documento se encuentra actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario (IU) de Adobe Experience Platform proporciona un panel a través del cual puede realizar la vista de información importante sobre sus [!DNL Real-time Customer Profile] datos, tal como se obtiene durante una instantánea diaria. Esta guía describe cómo acceder y trabajar con el [!DNL Profile] panel en la interfaz de usuario y proporciona más información sobre las métricas que se muestran en el panel.

Para obtener una descripción general de todas las funciones de Perfil de la interfaz de usuario de Experience Platform, visite la guía [de la interfaz de usuario de Perfil del cliente en tiempo](user-guide.md)real.

## Datos de panel de perfil

El panel Perfil muestra una instantánea de los datos de atributos (registros) que su organización tiene dentro del almacén de Perfiles en Experience Platform. La instantánea no incluye datos de eventos (series temporales).

Los datos de atributo de la instantánea muestran los datos exactamente como aparecen en el momento concreto en que se realizó la instantánea. En otras palabras, la instantánea no es una aproximación o muestra de los datos y el panel de Perfil no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se realizó la instantánea no se reflejarán en el panel hasta que se realice la siguiente instantánea.

Las métricas que se muestran en el panel de Perfil se basan en la directiva de combinación predeterminada para su organización. Para obtener más información sobre las directivas de combinación y cómo seleccionar o cambiar la directiva de combinación predeterminada, visite la guía [de la interfaz de usuario de directivas de](merge-policies.md)combinación.

## Explorar el panel de Perfil

Para desplazarse al panel de Perfil dentro de la interfaz de usuario de la plataforma, seleccione **[!UICONTROL Perfiles]** en el carril izquierdo y, a continuación, seleccione la ficha **[!UICONTROL Información general]** para mostrar el panel.

![](../images/profile-dashboard/dashboard-overview.png)

### Widgets y métricas

El panel está compuesto de utilidades, que son métricas de solo lectura que proporcionan información importante con respecto a los datos del Perfil. La fecha y hora &quot;última actualización&quot; de la utilidad muestran cuándo se realizó la última instantánea de los datos.

![](../images/profile-dashboard/dashboard-timestamp.png)

## Widgets disponibles

Experience Platform proporciona varias utilidades que puede utilizar para visualizar distintas métricas relacionadas con los datos de Perfil. Seleccione el nombre de una utilidad a continuación para obtener más información:

* [[!UICONTROL Tamaño de audiencia]](#audience-size)
* [[!UICONTROL Perfiles por Área de nombres]](#profiles-by-namespace)

### [!UICONTROL Tamaño de audiencia] {#audience-size}

El widget de tamaño **[!UICONTROL de]** Audiencia muestra el número total de perfiles combinados dentro del almacén de datos de Perfil en el momento en que se realizó la instantánea. Este número es el resultado de que la directiva de combinación predeterminada de su organización se está aplicando a los datos de Perfil para combinar los fragmentos de perfil juntos y formar un único perfil para cada individuo.

Para obtener más información sobre fragmentos y perfiles combinados, lea la sección de fragmentos de [perfil vs. perfiles](../home.md#profile-fragments-vs-merged-profiles) combinados de la descripción general [del](../home.md)Perfil.

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL Perfiles por Área de nombres] {#profiles-by-namespace}

La utilidad **[!UICONTROL Perfiles por Área de nombres]** muestra el desglose de Áreas de nombres en todos los perfiles combinados del almacén de Perfiles. El número total de perfiles por Área de nombres [!UICONTROL de] ID (es decir, sumar los valores mostrados para cada Área de nombres) siempre será mayor que el número total de perfiles de combinación porque un perfil podría tener varias Áreas de nombres asociadas. Por ejemplo, si un cliente interactúa con su marca en más de un canal, se asociarán varias Áreas de nombres con ese cliente individual.

Para obtener más información sobre las Áreas de nombres de identidad, visite la documentación [de](../../identity-service/home.md)Adobe Experience Platform Identity Service.

![](../images/profile-dashboard/profiles-by-namespace.png)

## Paneles adicionales

La interfaz de usuario de la plataforma proporciona paneles adicionales para ver instantáneas de los datos en Experience Platform. Estos paneles incluyen la segmentación y el uso de licencias. Para obtener más información sobre estos paneles adicionales, seleccione uno de los vínculos siguientes:

* [Panel de segmentos](../../segmentation/ui/segment-dashboard.md)
* [Panel de uso de licencias](../../landing/license-usage-dashboard.md)

## Pasos siguientes

Al seguir este documento ahora debería poder localizar el panel de Perfil y comprender las métricas que se muestran en los widgets disponibles. Para obtener más información sobre el trabajo con [!DNL Profile] datos en la interfaz de usuario del Experience Platform, consulte la guía [[!DNL Profile] de la](user-guide.md)interfaz de usuario.