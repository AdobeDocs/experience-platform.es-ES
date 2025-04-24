---
title: Activación de audiencias en destinos de personalización de Edge
description: Obtenga información sobre cómo activar audiencias de Adobe Experience Platform en destinos de personalización Edge para casos de uso de personalización de la misma página y de la siguiente.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 25697d341b2970eeb20d9f2507ee701ade8046d3
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 2%

---


# Activación de audiencias en destinos de personalización de Edge

## Información general {#overview}

Adobe Experience Platform usa [segmentación de Edge](../../segmentation/methods/edge-segmentation.md) junto con [destinos Edge](/help/destinations/destination-types.md#edge-personalization-destinations) para permitir que los clientes creen y segmenten audiencias a gran escala en tiempo real. Esta capacidad le ayuda a configurar casos de uso de personalización de la misma página y de la siguiente.

Algunos ejemplos de destinos Edge son las conexiones [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y [Personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md).

>[!NOTE]
>
>Al [configurar la conexión de Adobe Target](../catalog/personalization/adobe-target-connection.md) *sin* mediante un ID de secuencia de datos, no se admiten los casos de uso descritos en este artículo. En ausencia de un conjunto de datos, solo se admiten los casos de uso de personalización de la sesión siguiente.

>[!IMPORTANT]
> 
> * Para activar los datos y habilitar el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [para ver los destinos](/help/access-control/home.md#permissions).
> * Para activar datos sin pasar por el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de vista de destinos]**, **[!UICONTROL activar segmento sin asignación]**, **[!UICONTROL ver perfiles]** y **[!UICONTROL ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}
> 
> Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

En este artículo se explica el flujo de trabajo necesario para activar audiencias en destinos Edge de Adobe Experience Platform. Cuando se usan junto con [segmentación de Edge](../../segmentation/methods/edge-segmentation.md) y la asignación de atributos de perfil [opcional](#mapping), estos destinos habilitan casos de uso de personalización de la misma página y de la siguiente página en las propiedades web y móviles.

Para obtener una breve descripción general sobre cómo configurar la conexión de Adobe Target para la personalización de Edge, vea el siguiente vídeo.

>[!NOTE]
>
>La interfaz de usuario de Experience Platform se actualiza con frecuencia y puede haber cambiado desde que se grabó este vídeo. Para obtener la información más actualizada, consulte los pasos de configuración descritos en las secciones siguientes.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Vea el siguiente vídeo para obtener una breve descripción general de cómo compartir audiencias y atributos de perfil en Adobe Target y destinos de personalización personalizados.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Casos de uso {#use-cases}

Utilice soluciones de personalización de Adobe, como Adobe Target, o sus propias plataformas de socios de personalización (por ejemplo, [!DNL Optimizely], [!DNL Pega]), así como sistemas propietarios (por ejemplo, CMS interno) para impulsar una experiencia de personalización del cliente más profunda mediante el destino de [Personalization personalizado](../catalog/personalization/custom-personalization.md). Todo esto mientras también aprovecha las funcionalidades de segmentación y recopilación de datos de Experience Platform Edge Network.

Los casos de uso que se describen a continuación incluyen personalización del sitio y publicidad en el sitio segmentada.

Para habilitar estos casos de uso, los clientes necesitan una forma rápida y sencilla de recuperar información de audiencias y atributos de perfil de Experience Platform y de enviar esta información a las conexiones de [Adobe Target](../catalog/personalization/adobe-target-connection.md) o [Personalization personalizado](../catalog/personalization/custom-personalization.md) en la interfaz de usuario de Experience Platform.

### Personalización en la misma página {#same-page}

Un usuario visita una página del sitio web. Puede utilizar la información de visita a la página actual (por ejemplo, la dirección URL de referencia, el idioma del explorador o la información de producto incrustada) para seleccionar la siguiente acción o decisión (por ejemplo, personalización), mediante la conexión de [Personalización personalizada](../catalog/personalization/custom-personalization.md) para plataformas que no sean de Adobe (por ejemplo, [!DNL Pega], [!DNL Optimizely] u otras).

### Personalización de la página siguiente {#next-page}

Un usuario visita la página A del sitio web. En función de esta interacción, el usuario cumple los requisitos para un conjunto de audiencias. A continuación, el usuario hace clic en un vínculo que le lleva de la página A a la B. Las audiencias para las que el usuario estuvo cualificado durante la interacción anterior en la página A, junto con las actualizaciones de perfil determinadas por la visita actual al sitio web, se utilizan para activar la siguiente acción o decisión (por ejemplo, qué titular de publicidad se mostrará al visitante o, en el caso de las pruebas A/B, qué versión de la página se mostrará).

### Personalización de la sesión siguiente {#next-session}

Un usuario visita varias páginas del sitio web. En función de estas interacciones, el usuario cumple los requisitos para un conjunto de audiencias. A continuación, el usuario finaliza la sesión de exploración actual.

Al día siguiente, el usuario vuelve al mismo sitio web del cliente. Las audiencias para las que se habían clasificado durante la interacción anterior con todas las páginas del sitio web visitado, junto con las actualizaciones de perfil determinadas por la visita del sitio web actual, se utilizan para seleccionar la siguiente acción/decisión (por ejemplo, qué banner publicitario mostrar al visitante o, en el caso de las pruebas A/B, qué versión de la página mostrar).

### Personalizar un titular de página de inicio {#home-page-banner}

Una empresa de venta y alquiler de viviendas quiere personalizar su página de inicio con un banner, según las cualificaciones de audiencia en Adobe Experience Platform. La empresa puede seleccionar qué audiencias deben obtener una experiencia personalizada y enviarlas a Adobe Target como criterios de segmentación para su oferta de Target.

## Requisitos previos {#prerequisites}

### Configuración de una secuencia de datos en la IU de recopilación de datos {#configure-datastream}

El primer paso para configurar el destino de personalización es configurar una secuencia de datos para Experience Platform Web SDK. Esto se realiza en la IU de recopilación de datos.

Al configurar la secuencia de datos, en **[!UICONTROL Adobe Experience Platform]**, asegúrese de que tanto **[!UICONTROL Segmentación de Edge]** como **[!UICONTROL Destinos de Personalization]** estén seleccionados.

>[!TIP]
>
>A partir de la versión de abril de 2024, no es necesario que active la casilla Segmentación de Edge al [configurar la conexión con Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md). En este caso, la [personalización de la próxima sesión](#next-session) es el único caso de uso de personalización disponible.

![Configuración de flujo de datos con segmentación Edge y destinos Personalization resaltados.](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Para obtener más información sobre cómo configurar una secuencia de datos, siga las instrucciones que se describen en la [documentación de Experience Platform Web SDK](../../datastreams/configure.md#aep).

### Crear una política de combinación [!DNL Active-On-Edge] {#create-merge-policy}

Después de crear la conexión de destino, debe crear una política de combinación de [!DNL Active-On-Edge]. La política de combinación [!DNL Active-On-Edge] garantiza que las audiencias se evalúen constantemente [en el perímetro](../../segmentation/methods/edge-segmentation.md) y que estén disponibles para casos de uso de personalización en tiempo real y de la página siguiente.

>[!IMPORTANT]
>
>Actualmente, los destinos perimetrales solo admiten la activación de audiencias que usen la [directiva de combinación activa en Edge](../../segmentation/ui/segment-builder.md#merge-policies) establecida como predeterminada. Si asigna audiencias que utilizan una política de combinación diferente a destinos Edge, esas audiencias no se evalúan.

Siga las instrucciones de [creación de una política de combinación](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) y asegúrese de habilitar la opción **[!UICONTROL Política de combinación activa en Edge]**.

### Creación de una nueva audiencia en Experience Platform {#create-audience}

Después de crear la política de combinación [!DNL Active-On-Edge], debe crear una audiencia nueva en Experience Platform.

Siga la guía de [generador de audiencias](../../segmentation/ui/segment-builder.md) para crear su nueva audiencia y asegúrese de [asignarla](../../segmentation/ui/segment-builder.md#merge-policies) a la política de combinación [!DNL Active-On-Edge] que creó en el paso anterior.

### Creación de una conexión de destino {#connect-destination}

Una vez configurada la secuencia de datos, puede empezar a configurar el destino de personalización.

Siga el [tutorial de creación de conexión de destino](../ui/connect-destination.md) para obtener instrucciones detalladas sobre cómo crear una nueva conexión de destino.

Según el destino que esté configurando, consulte los siguientes artículos para conocer los requisitos previos específicos del destino y la información relacionada:

* [Conexión de Adobe Target](../catalog/personalization/adobe-target-connection.md#parameters)
* [Conexión de personalización personalizada](../catalog/personalization/custom-personalization.md#parameters)

## Seleccione su destino {#select-destination}

Después de completar los requisitos previos, ahora puede seleccionar el destino de personalización de Edge que desea utilizar para la personalización de la misma página y de la página siguiente.

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Ficha Catálogo de destino resaltada en la interfaz de usuario de Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar audiencias]** en la tarjeta correspondiente al destino de personalización en el que desee activar las audiencias, como se muestra en la imagen siguiente.

   ![Activar el control de audiencia resaltado en una tarjeta de destino del catálogo.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Seleccione la conexión de destino que desee usar para activar las audiencias y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Seleccionar paso de destino en el flujo de trabajo de activación.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Pasa a la siguiente sección para [seleccionar tus audiencias](#select-audiences).

## Selección de audiencias {#select-audiences}

Utilice las casillas de verificación de la izquierda de los nombres de audiencia para seleccionar las audiencias que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

Para seleccionar las audiencias que desea activar en el destino, utilice las casillas de verificación que aparecen a la izquierda de los nombres de audiencia y luego seleccione **[!UICONTROL Siguiente]**.

Puede seleccionar entre varios tipos de audiencias, según su origen:

* **[!UICONTROL Servicio de segmentación]**: Audiencias generadas en Experience Platform por el servicio de segmentación. Consulte la [documentación de segmentación](../../segmentation/ui/overview.md) para obtener más información.
* **[!UICONTROL Carga personalizada]**: audiencias generadas fuera de Experience Platform y cargadas en Experience Platform como archivos CSV. Para obtener más información sobre audiencias externas, consulte la documentación sobre [importación de una audiencia](../../segmentation/ui/audience-portal.md#import-audience).
* Otros tipos de audiencias, originadas en otras soluciones de Adobe, como [!DNL Audience Manager].

![Seleccione el paso de audiencias del flujo de trabajo de activación con varias audiencias resaltadas.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Asignar atributos {#mapping}

>[!IMPORTANT]
>
>Los atributos de perfil pueden contener datos confidenciales. Para proteger estos datos, el destino **[!UICONTROL Personalization personalizado]** requiere que uses la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/) al configurar el destino para la personalización basada en atributos. Todas las llamadas a la API de Edge Network deben realizarse en un [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/).
>
><br>Si ya utiliza Web SDK o Mobile SDK para la integración, puede recuperar atributos mediante la API de Edge Network agregando una integración del lado del servidor.
>
><br>Si no cumple los requisitos anteriores, la personalización se basará únicamente en el abono a audiencias.

Seleccione los atributos en función de los cuales desea habilitar casos de uso de personalización para los usuarios. Esto significa que si el valor de un atributo cambia o si se añade un atributo a un perfil, ese perfil se convierte en miembro de la audiencia y se activa en el destino de personalización.

Añadir atributos es opcional y aún puede continuar con el siguiente paso y habilitar la personalización de la misma página y de la página siguiente sin seleccionar atributos. Si no agrega ningún atributo en este paso, la personalización se seguirá produciendo en función de la pertenencia a la audiencia y de las cualificaciones del mapa de identidad de los perfiles.

![Imagen que muestra el paso de asignación con un atributo seleccionado.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Seleccionar atributos de origen {#select-source-attributes}

Para agregar atributos de origen, seleccione el control **[!UICONTROL Agregar nuevo campo]** en la columna **[!UICONTROL Campo de Source]** y busque o navegue hasta el campo de atributo XDM que desee, como se muestra a continuación.

![Grabación de pantalla que muestra cómo seleccionar un atributo de destino en el paso de asignación.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Seleccionar atributos de destino {#select-target-attributes}

Para agregar atributos de destino, seleccione el control **[!UICONTROL Agregar nuevo campo]** en la columna **[!UICONTROL Campo de destino]** y escriba el nombre de atributo personalizado al que desea asignar el atributo de origen.

>[!NOTE]
>
>La selección de atributos de destino solo se aplica al flujo de trabajo de activación de [Personalization personalizado](../catalog/personalization/custom-personalization.md) para admitir la asignación de campos de nombre descriptivo en la plataforma de destino.

![Grabación de pantalla que muestra cómo seleccionar un atributo XDM en el paso de asignación](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Programar exportación de público {#scheduling}

De manera predeterminada, la página [!UICONTROL Programación de audiencias] muestra solamente las audiencias recién seleccionadas que eligió en el flujo de activación actual.

Para ver todas las audiencias que se están activando en su destino, use la opción de filtrado y deshabilite el filtro **[!UICONTROL Mostrar solo nuevas audiencias]**.

![Filtro de todas las audiencias resaltado.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

En la página **[!UICONTROL Programación de audiencias]**, seleccione cada audiencia y luego use los selectores **[!UICONTROL Fecha de inicio]** y **[!UICONTROL Fecha de finalización]** para configurar el intervalo de tiempo para enviar datos a su destino.

![Paso de programación de audiencia del flujo de trabajo de activación con las fechas de inicio y finalización resaltadas.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Seleccione **[!UICONTROL Siguiente]** para ir a la página [!UICONTROL Revisar].

## Revisar {#review}

En la página **[!UICONTROL Revisar]**, puedes ver un resumen de tu selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

![Resumen de la selección en el paso de revisión.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Lea acerca de [evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el paso **[!UICONTROL Revisar]**, Experience Platform también comprueba si hay alguna infracción de la directiva de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de audiencia hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, lea acerca de [infracciones de directivas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección de documentación de control de datos.

![Ejemplo de infracción de directiva de datos.](../assets/common/data-policy-violation.png)

### Filtrado de audiencias {#filter-audiences}

En este paso puede utilizar los filtros disponibles en la página para mostrar solo las audiencias cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de audiencia disponibles en el paso de revisión.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Si está satisfecho con su selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
