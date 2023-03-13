---
title: Usar datos meteorológicos de DNL The Weather Channel
description: Utilice los datos meteorológicos de DNL The Weather Channel para mejorar los datos que recopila a través de flujos de datos.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# Usar datos meteorológicos de [!DNL The Weather Channel]

El Adobe se ha asociado con [!DNL [The Weather Company]](https://www.ibm.com/weather) para añadir el contexto adicional del clima de Estados Unidos a los datos recopilados a través de flujos de datos. Puede utilizar estos datos para realizar análisis, segmentar y crear segmentos en Experience Platform.

Existen tres tipos de datos disponibles en [!DNL The Weather Channel]:

* **[!UICONTROL Tiempo actual]**: Las condiciones meteorológicas actuales del usuario, según su ubicación. Esto incluye la temperatura actual, la precipitación, la cobertura de nubes y más.
* **[!UICONTROL Pronóstico del tiempo]**: La previsión incluye la previsión a 1, 2, 3, 5, 7 y 10 días para la ubicación del usuario.
* **[!UICONTROL Déclencheur]**: los Déclencheur son combinaciones específicas que se asignan a diferentes condiciones meteorológicas semánticas. Existen tres tipos diferentes de déclencheur meteorológicos:

   * **[!UICONTROL Déclencheur meteorológicos]**: Condiciones semánticamente significativas, como clima frío o lluvioso. Estas pueden diferir en sus definiciones entre diversos climas.
   * **[!UICONTROL Déclencheur del producto]**: Condiciones que llevarían a la compra de diferentes tipos de productos. Por ejemplo: los pronósticos de clima frío podrían significar que las compras de abrigos de lluvia son más probables.
   * **[!UICONTROL Déclencheur meteorológicos severos]**: Advertencias meteorológicas graves, como tormentas de invierno o huracanes.

## Requisitos previos {#prerequisites}

Antes de usar los datos meteorológicos, asegúrese de cumplir los siguientes requisitos previos:

* Debe autorizar los datos meteorológicos que va a utilizar, desde [!DNL The Weather Channel]. Luego lo habilitarán en su cuenta.
* Los datos meteorológicos solo están disponibles a través de flujos de datos. Para utilizar datos meteorológicos, debe utilizar [!DNL Web SDK], [!DNL Mobile Edge Extension] o el [API de servidor](../../../server-api/overview.md) para aprovechar estos datos.
* La secuencia de datos debe tener [[!UICONTROL Ubicación geográfica]](../configure.md#advanced-options) activado.
* Añada el [grupo de campo meteorológico](#schema-configuration) al esquema que está utilizando.

## Aprovisionamiento {#provisioning}

Una vez adquirida la licencia de los datos de [!DNL The Weather Channel], habilitarán su cuenta para acceder a los datos. A continuación, debe ponerse en contacto con el Servicio de atención al cliente de Adobe para habilitar los datos en su conjunto de datos. Una vez activados, los datos se adjuntan automáticamente.

Puede validar que se está agregando ejecutando un seguimiento de Edge con el depurador o utilizando Assurance para rastrear una visita a través de [!DNL Edge Network].

### Configuración del esquema {#schema-configuration}

Debe agregar los grupos de campos meteorológicos al esquema del Experience Platform correspondiente al conjunto de datos de evento que esté utilizando en el conjunto de datos. Hay cinco grupos de campos disponibles:

* [!UICONTROL Pronóstico del tiempo]
* [!UICONTROL Tiempo actual]
* [!UICONTROL Déclencheur del producto]
* [!UICONTROL Déclencheur relativos]
* [!UICONTROL Déclencheur meteorológicos severos]

## Acceso a los datos meteorológicos {#access-weather-data}

Una vez que los datos tengan licencia y estén disponibles, puede acceder a ellos de varias formas mediante los servicios de Adobe.

### Adobe Analytics {#analytics}

Entrada [!DNL Adobe Analytics], los datos meteorológicos están disponibles para su asignación mediante reglas de procesamiento, junto con el resto de sus [!DNL XDM] esquema.

Puede encontrar la lista de campos que puede asignar en la [referencia meteorológica](weather-reference.md) página. Como con todos [!DNL XDM] esquemas, las claves llevan el prefijo `a.x`. Por ejemplo, un campo denominado `weather.current.temperature.farenheit` aparecería en [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Interfaz de regla de procesamiento](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

Entrada [!DNL Adobe Customer Journey Analytics]Sin embargo, los datos meteorológicos están disponibles en el conjunto de datos especificado en la secuencia de datos. Siempre y cuando los atributos del tiempo sean [añadido a su esquema](#prerequisites-prerequisites), estarán disponibles para [agregar a una vista de datos](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=es) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Los datos meteorológicos están disponibles en el [Real-time Customer Data Platform](../../../rtcdp/overview.md), para su uso en segmentos. Los datos meteorológicos se adjuntan a los eventos.

![Generador de segmentos que muestra eventos meteorológicos](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Dado que las condiciones meteorológicas cambian a menudo, Adobe recomienda establecer restricciones temporales en los segmentos, como se muestra en el ejemplo anterior. Tener un día frío en el último día o dos es mucho más impactante que tener un día frío hace 6 meses.

Consulte la [referencia meteorológica](weather-reference.md) para los campos disponibles.

### Adobe Target {#target}

Entrada [!DNL Adobe Target]Además, puede utilizar los datos meteorológicos para impulsar la personalización en tiempo real. Los datos meteorológicos se pasan a [!DNL Target] as [!UICONTROL mBox] y puede acceder a ella mediante un [!UICONTROL mBox] parámetro.

![Generador de audiencias de Target](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

El parámetro es el [!DNL XDM] ruta a un campo específico. Consulte la [referencia meteorológica](weather-reference.md) para los campos disponibles y sus rutas correspondientes.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora comprende mejor cómo puede utilizar los datos meteorológicos en varias soluciones de Adobe. Para obtener más información sobre la asignación de campos de datos meteorológicos, consulte la [referencia de asignación de campos](weather-reference.md).