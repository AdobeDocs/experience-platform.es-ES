---
solution: Experience Platform
title: Información general sobre Adobe Experience Platform multi-cloud
description: Descubra cuáles son las diferencias entre ejecutar Experience Platform en Microsoft Azure y Amazon Web Service.
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---


# Información general sobre Adobe Experience Platform multi-cloud

Adobe Experience Platform es un producto de varias nubes que le ofrece la opción de ejecutar en [[!DNL Microsoft Azure]](https://azure.microsoft.com/en-us) o en [[!DNL Amazon Web Services (AWS)]](https://aws.amazon.com/). Esta flexibilidad le permite elegir la mejor opción para sus necesidades técnicas y empresariales.

>[!AVAILABILITY]
>
>Adobe Experience Platform que se ejecuta en Amazon Web Service (AWS) está disponible actualmente para un número limitado de clientes. Para obtener más información sobre Experience Platform en AWS, póngase en contacto con el equipo de cuenta de Adobe.

Esta página proporciona información general de alto nivel sobre las dos infraestructuras en la nube disponibles e incluye instrucciones sobre cómo elegir la adecuada para su negocio.

## ¿Qué implementación en la nube es adecuada para mí? {#which-cloud-is-right}

La elección entre Experience Platform en Azure o AWS depende de varios factores específicos de su empresa:

* **Necesidades empresariales y técnicas**: Evalúe los requisitos de su organización y la estrategia de nube a largo plazo.
* **Infraestructura existente**: considere sus necesidades actuales de integración e infraestructura en la nube.
* **Confianza en la tecnología de la nube**: Si su empresa depende en gran medida de las tecnologías de Microsoft, Azure podría ser la mejor opción. Si confía más en los servicios de Amazon, AWS podría ser la mejor opción.
* **Consideraciones sobre la residencia de datos**: evalúe los requisitos de residencia de datos para su organización y asegúrese de que la plataforma de nube elegida ofrezca regiones que cumplan con estas regulaciones.

Teniendo en cuenta los factores anteriores, utilice este árbol de decisión simplificado para decidir la implementación en la nube adecuada para sus necesidades comerciales.

![Imagen que muestra la distribución geográfica de las ubicaciones de alojamiento.](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## Ubicaciones de alojamiento {#available-cloud-regions}

La elección de la región de nube adecuada es crucial para cumplir los requisitos de residencia de datos y garantizar un rendimiento óptimo.

![Imagen que muestra la distribución geográfica de las ubicaciones de alojamiento.](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

Experience Platform está disponible en seis ubicaciones de alojamiento de Microsoft Azure, una ubicación de alojamiento de Amazon Web Service (AWS) y enruta los datos a los servicios de Adobe a través de siete [nodos de Edge Network](../collection/home.md#edge) distribuidos por todo el mundo.

### Regiones de Microsoft Azure {#azure-regions}

La siguiente tabla indica las regiones de Microsoft Azure en las que está alojado Experience Platform.

| País | Código de región | Ubicación |
|---------|-------------|----------|
| Estados Unidos de América | VA7 | Virginia |
| Reino Unido | GBR9 | Londres |
| Países Bajos | NDL2 | Ámsterdam |
| Canadá | CAN2 | Toronto |
| India | IND2 | Maharashtra |
| Australia | AUS5 | Nueva Gales del Sur |

{style="table-layout:auto"}

### Regiones de Amazon Web Service (AWS) {#aws-regions}

La siguiente tabla indica las regiones de AWS en las que está alojado Experience Platform. Vuelva regularmente para ver si se han añadido ubicaciones adicionales.

| País | Código de región | Ubicación |
|---------|-------------|----------|
| Estados Unidos de América | VA6 | Virginia |

{style="table-layout:auto"}

## Paridad de características {#feature-parity}

Adobe se compromete a ofrecer paridad de funciones en todas las plataformas de la nube, para todas las aplicaciones que se ejecuten en Experience Platform, como:

* [Real-Time Customer Data Platform](../rtcdp/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-landing)

Sin embargo, algunas funcionalidades pueden diferir entre las implementaciones de Azure y AWS. Estas diferencias se describen en la sección siguiente y en otras partes de la documentación del producto, si corresponde.

### Diferencias entre ejecutar Experience Platform en Microsoft Azure y AWS {#azure-aws-differences}

La siguiente tabla resalta las principales diferencias entre la ejecución de Experience Platform en Microsoft Azure y AWS.

| Funcionalidad / Funcionalidad | Microsoft Azure | Amazon Web Service |
| --- | --- | --- |
| [Cumplimiento de HIPAA](https://www.adobe.com/trust/compliance/hipaa-ready.html) | Admitido | No compatible |
| [Catálogo de conectores de origen](/help/sources/home.md) | Todos los conectores del catálogo de fuentes son compatibles | Hay un número limitado de conectores de origen disponibles. Todos los conectores de origen disponibles para las implementaciones de AWS se llaman en una nota de la parte superior de la página en sus respectivas páginas de documentación. |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## Conclusión {#conclusion}

Experience Platform proporciona flexibilidad y opciones al darle la opción de ejecutar en Microsoft Azure o Amazon Web Service. Evalúe sus necesidades empresariales y la infraestructura existente para tomar una decisión informada sobre la plataforma en la nube que debe utilizar.
