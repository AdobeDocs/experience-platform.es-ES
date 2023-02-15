---
title: Uso de datos meteorológicos de DNL The Weather Channel
description: Utilice los datos meteorológicos de DNL The Weather Channel para mejorar los datos que recopila a través de conjuntos de datos.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# Usar datos meteorológicos de [!DNL The Weather Channel]

Adobe se ha asociado con [!DNL [The Weather Company]](https://www.ibm.com/weather) para aportar el contexto adicional del clima de los Estados Unidos a los datos recopilados mediante conjuntos de datos. Puede utilizar estos datos para análisis, segmentación y creación de segmentos en Experience Platform.

Hay 3 tipos de datos disponibles en [!DNL The Weather Channel]:

* **[!UICONTROL Tiempo actual]**: Las condiciones climáticas actuales del usuario, según su ubicación. Esto incluye la temperatura actual, la anticipación, la cobertura de la nube y mucho más.
* **[!UICONTROL Tiempo previsto]**: La previsión incluye la previsión de 1,2,3,5,7 y 10 días para la ubicación del usuario.
* **[!UICONTROL Déclencheur]**: Los déclencheur son combinaciones específicas que se asignan a diferentes condiciones climáticas semánticas. Hay tres tipos diferentes de déclencheur meteorológicos:

   * **[!UICONTROL Déclencheur meteorológicos]**: Condiciones semánticamente significativas, como clima frío o lluvioso. Estas pueden diferir en sus definiciones entre distintos climas.
   * **[!UICONTROL Déclencheur del producto]**: Condiciones que conducirían a la compra de diferentes tipos de productos. Por ejemplo: los pronósticos del clima frío podrían significar que es más probable que se compren abrigos para lluvia.
   * **[!UICONTROL Déclencheur meteorológicos graves]**: Advertencias meteorológicas severas, como tormenta de invierno o advertencias de huracán.

## Requisitos previos {#prerequisites}

Antes de utilizar los datos del tiempo, asegúrese de cumplir los siguientes requisitos previos:

* Debe obtener una licencia de los datos meteorológicos que utilizará, desde [!DNL The Weather Channel]. Luego lo habilitarán en su cuenta.
* Los datos meteorológicos solo están disponibles mediante conjuntos de datos. Para usar datos meteorológicos, debe usar [!DNL Web SDK], [!DNL Mobile Edge Extension] o [API de servidor](../../../server-api/overview.md) para aprovechar estos datos.
* El conjunto de datos debe tener [[!UICONTROL Ubicación geográfica]](../configure.md#advanced-options) activada.
* Agregue la variable [grupo de campos meteorológicos](#schema-configuration) al esquema que está utilizando.

## Aprovisionamiento {#provisioning}

Una vez que haya obtenido la licencia de los datos desde [!DNL The Weather Channel], permitirán que su cuenta acceda a los datos. A continuación, debe ponerse en contacto con el Servicio de atención al cliente de Adobe para que los datos estén activados en su conjunto de datos. Una vez habilitados, los datos se adjuntan automáticamente.

Puede validar que se está añadiendo ejecutando un seguimiento perimetral con el depurador o utilizando Assurance para rastrear una visita a través del [!DNL Edge Network].

### Configuración del esquema {#schema-configuration}

Debe añadir los grupos de campos meteorológicos al esquema de Experience Platform correspondiente al conjunto de datos de evento que está utilizando en el conjunto de datos de su conjunto de datos. Hay cinco grupos de campos disponibles:

* [!UICONTROL Tiempo previsto]
* [!UICONTROL Tiempo actual]
* [!UICONTROL Déclencheur del producto]
* [!UICONTROL Déclencheur relativos]
* [!UICONTROL Déclencheur meteorológicos graves]

## Acceso a los datos meteorológicos {#access-weather-data}

Una vez que los datos tengan licencia y estén disponibles, puede acceder a ellos de diversas formas a través de los servicios de Adobe.

### Adobe Analytics {#analytics}

En [!DNL Adobe Analytics], los datos meteorológicos están disponibles para asignarse mediante reglas de procesamiento, junto con el resto de [!DNL XDM] esquema.

Puede encontrar la lista de campos que puede asignar en la [referencia meteorológica](weather-reference.md) página. Como con todos [!DNL XDM] esquemas, las claves tienen el prefijo `a.x`. Por ejemplo, un campo denominado `weather.current.temperature.farenheit` aparecería en [!DNL Analytics] como `a.x.weather.current.temperature.farenheit`.

![Interfaz de regla de procesamiento](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

En [!DNL Adobe Customer Journey Analytics], los datos meteorológicos están disponibles en el conjunto de datos especificado en el conjunto de datos. Siempre y cuando los atributos meteorológicos sean [añadida al esquema](#prerequisites-prerequisites), estarán disponibles para [agregar a una vista de datos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=es) en [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Los datos meteorológicos están disponibles en la [Real-time Customer Data Platform](../../../rtcdp/overview.md), para usar en segmentos. Los datos del tiempo se adjuntan a los eventos.

![Generador de segmentos que muestra eventos meteorológicos](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Dado que las condiciones climáticas cambian con frecuencia, el Adobe recomienda establecer restricciones de tiempo en los segmentos, como se muestra en el ejemplo anterior. Tener un día frío en el último día o dos es mucho más impactante que tener un día frío hace 6 meses.

Consulte la [referencia meteorológica](weather-reference.md) para los campos disponibles.

### Adobe Target {#target}

En [!DNL Adobe Target], puede utilizar datos meteorológicos para personalizar en tiempo real. Los datos del tiempo se pasan a [!DNL Target] como [!UICONTROL mBox] parámetros y puede acceder a ellos a través de una [!UICONTROL mBox] parámetro.

![Generador de audiencias de Target](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

El parámetro es [!DNL XDM] ruta a un campo específico. Consulte la [referencia meteorológica](weather-reference.md) para los campos disponibles y sus rutas correspondientes.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora tiene una mejor comprensión de cómo puede utilizar los datos meteorológicos en varias soluciones de Adobe. Para obtener más información sobre la asignación de campos de datos meteorológicos, consulte la [referencia de asignación de campos](weather-reference.md).