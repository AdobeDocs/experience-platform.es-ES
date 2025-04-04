---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;plataforma de datos del cliente en tiempo real;cdp en tiempo real;b2b;cdp
solution: Experience Platform
title: Introducción a Real-Time Customer Data Platform B2B edition
description: Utilice este escenario como ejemplo al configurar la implementación de Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---

# Introducción a Real-Time Customer Data Platform B2B edition

Este documento proporciona un flujo de trabajo completo de alto nivel para empezar a usar Real-Time Customer Data Platform (CDP) B2B edition, con un ejemplo de uso para ilustrar conceptos clave.

La empresa tecnológica Bodea quiere combinar datos de personas y cuentas de diferentes fuentes de datos en silo para dirigirse de forma eficaz a los clientes con un correo electrónico y una campaña publicitaria de LinkedIn para su nuevo producto. Bodea utiliza Marketo Engage como plataforma de automatización de marketing y necesita segmentar una audiencia específica de B2B desde varios CRM que contengan datos de clientes.

## Introducción

Este flujo de trabajo de tutorial se basa en varios servicios de Adobe Experience Platform como parte de la demostración. Si desea continuar, se recomienda tener una buena comprensión de los siguientes servicios:

- [Modelo de datos de experiencia (XDM)](../xdm/home.md)
- [Fuentes](../sources/home.md)
- [Segmentación](../segmentation/home.md)
- [Destinos](../destinations/home.md)

## Creación de esquemas para los datos

Como parte de la configuración inicial, el departamento informático de Bodea debe crear un esquema XDM para garantizar que sus datos sigan un formato estándar cuando se incorporen a Experience Platform y que se puedan llevar a cabo acciones en los distintos servicios de Experience Platform y productos de Adobe Experience Cloud (como Adobe Analytics y Adobe Target).

>[!WARNING]
>
>Debe seguir los patrones de ingesta tal como se describe en la documentación de fuentes relevantes vinculada a través de este tutorial. No se garantiza que funcionen otros métodos de asignación de campos.

Adobe Experience Platform permite generar automáticamente los esquemas y los espacios de nombres necesarios para las fuentes de datos B2B. Esta herramienta garantiza que los esquemas creados describan los datos de una manera reutilizable estructurada. Siga la [documentación de la utilidad de generación automática de esquemas y áreas de nombres B2B](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) para obtener una referencia completa del proceso de instalación.

En la interfaz de usuario de Adobe Experience Platform, el experto en marketing de Bodea selecciona **[!UICONTROL Esquemas]** en el carril izquierdo, seguido de la pestaña **[!UICONTROL Examinar]**. Dado que utilizaban la utilidad de generación automática de Marketo Engage, los nuevos esquemas vacíos aparecen en la lista y todos tienen el prefijo &quot;B2B&quot;.

![Ficha de exploración del espacio de trabajo de esquemas](./assets/b2b-tutorial/empty-b2b-schemas.png)

La utilidad de generación automática definió la estructura del modelo de datos para los esquemas que utilizan clases B2B de XDM estándar (como [XDM Business Account](../xdm/classes/b2b/business-account.md) y [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)) que capturan entidades de datos B2B fundamentales. Además, los esquemas B2B generados automáticamente en estas clases tienen relaciones preestablecidas que permiten casos de uso de segmentación avanzada. Cualquier grupo de campos adicional necesario para la estructura de datos se puede crear fácilmente aquí a través de la interfaz de usuario. Consulte la guía de la interfaz de usuario de [XDM, adición de grupos de campos a una sección de esquema](../xdm/ui/resources/schemas.md#add-field-groups) para obtener más información.

>[!NOTE]
> 
>Si no usa la utilidad de generador automático o si necesita crear una nueva relación, consulte el tutorial sobre [creación de relaciones entre esquemas B2B](../xdm/tutorials/relationship-b2b.md).

El Perfil del cliente en tiempo real combina datos de fuentes dispares para crear perfiles consolidados de entidades B2B clave. Dado que los perfiles se generan en función de una sola clase, la utilidad de generación automática configura relaciones entre esquemas en función de casos de uso empresariales comunes. Como resultado, el equipo de Bodea ya está listo para introducir datos basados en sus esquemas B2B.

>[!NOTE]
> 
>Las áreas de nombres de identidad, las claves principales y las relaciones predeterminadas creadas para los esquemas mediante la utilidad de generación automática se pueden detectar fácilmente dentro del espacio de trabajo de esquemas.
>
>![visualización predeterminada de la interfaz de usuario de relación e identidad del esquema](./assets/b2b-tutorial/schema-identity-relationship.png)

## Ingesta de datos en Experience Platform

A continuación, el experto en marketing de Bodea utiliza el [conector Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) para introducir datos en Experience Platform y utilizarlos en servicios descendentes. También puede ingerir datos utilizando una de las fuentes aprobadas para Real-Time CDP B2B edition.

>[!NOTE]
> 
>Para saber qué conectores de origen están disponibles para su organización, puede ver el catálogo de fuentes en la interfaz de usuario de Experience Platform. Para acceder al catálogo, selecciona **Orígenes** en el panel de navegación izquierdo y, a continuación, selecciona **Catálogo**.

Para crear una conexión entre una cuenta de Marketo y Experience Platform, debe adquirir credenciales de autenticación. Consulte la [guía sobre la obtención de credenciales de autenticación del conector de origen de Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) para obtener instrucciones detalladas.

Después de adquirir las credenciales de autenticación, el experto en marketing de Bodea crea una conexión entre la cuenta de Marketo y su organización de Experience Platform. Consulte la documentación para obtener instrucciones sobre [cómo conectar una cuenta de Marketo mediante la interfaz de usuario de Experience Platform](../sources/tutorials/ui/create/adobe-applications/marketo.md).

El conector de origen de Marketo Engage proporciona una función de asignación automática para que el proceso de asignación de todos los campos de datos a los de los esquemas recién creados sea mucho más sencillo.

>[!NOTE]
> 
>Si ha creado grupos de campos personalizados en los esquemas XDM, es posible que tenga campos no conectados en esta fase del proceso. Asegúrese de comprobar todos los valores que rellenan los grupos de campos personalizados.

El experto en marketing de Bodea comprueba que todos los grupos de campos están asignados correctamente y continúa con el proceso de configuración de fuentes inicializando un flujo de datos. Al crear un flujo de datos para introducir datos de Marketo, los servicios de Experience Platform descendentes pueden utilizar los datos entrantes. Durante el proceso de ingesta inicial, los datos se introducen en Experience Platform como un lote. Después, los datos ingeridos posteriores se transmiten al perfil con actualizaciones casi en tiempo real.

## Crear una audiencia para evaluar los datos

La siguiente tarea es crear una audiencia para la nueva campaña de marketing por correo electrónico de Bodea en función de atributos específicos de entidades relacionadas en los datos de origen. En la interfaz de usuario de Experience Platform, el experto en marketing de Bodea selecciona primero **[!UICONTROL Segmentos]** en el panel de navegación izquierdo y, a continuación, **[!UICONTROL Crear segmento]**.

En este ejemplo, la audiencia encuentra todas las personas que trabajan en el departamento de ventas y están relacionadas con cualquier cuenta que tenga al menos una oportunidad abierta. Estas audiencias requieren un vínculo entre la clase Perfil individual de XDM, la clase Cuenta empresarial de XDM y la clase Oportunidad empresarial de XDM.

![Segmento de caso de uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Para obtener instrucciones sobre cómo crear audiencias para evaluar los datos, consulte la [guía de la interfaz de usuario del generador de segmentos](../segmentation/ui/segment-builder.md). Para casos de uso de segmentación B2B más específicos, consulte la [descripción general de segmentación para Real-Time CDP B2B edition](./segmentation/b2b.md).

El Generador de segmentos le permite crear una audiencia comercializable a partir de los datos del perfil del cliente en tiempo real y ver las estimaciones de su audiencia potencial en función de la combinación de atributos, eventos y audiencias existentes que haya definido.

## Activar los datos evaluados en un destino

Una vez que la audiencia se haya creado correctamente, se proporciona un resumen en la sección [!UICONTROL Detalles] del área de trabajo. Como actualmente no hay destinos activados para la definición del segmento, el experto en marketing de Bodea debe exportar la audiencia a un conjunto de datos al que se pueda acceder y sobre el que se pueda actuar.

En el espacio de trabajo [!UICONTROL Segmentos] de la interfaz de usuario de Experience Platform, el experto en marketing de Bodea selecciona **[!UICONTROL Activar en destino]**.

![Activar la audiencia en un destino](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Consulte el tutorial sobre [activación de una audiencia en un destino](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) para ver los pasos detallados sobre cómo hacerlo.

El especialista en marketing de Bodea activa la audiencia en el destino de Marketo, lo que les permite insertar datos de audiencia de Experience Platform en Marketo Engage en forma de lista estática. Consulte la guía del [destino de Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) para obtener más información.

## Pasos siguientes

Al seguir este tutorial, ha aprovechado correctamente los distintos servicios de Adobe Experience Platform utilizados por Real-Time CDP B2B edition. Como resultado, ha aprendido a ingerir, segmentar, evaluar y exportar los datos B2B como audiencias procesables que se pueden activar en diferentes canales.
