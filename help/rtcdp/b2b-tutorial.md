---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;plataforma de datos de clientes en tiempo real;cdp en tiempo real;b2b;cdp
solution: Experience Platform
title: Introducción a Real-time Customer Data Platform B2B Edition
description: Utilice este caso de ejemplo como ejemplo al configurar la implementación de Adobe Real-time Customer Data Platform B2B Edition.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Introducción a Real-time Customer Data Platform B2B Edition

Este documento proporciona un flujo de trabajo completo de alto nivel para empezar a usar Real-time Customer Data Platform (CDP) B2B Edition, utilizando un ejemplo de caso de uso para ilustrar conceptos clave.

La empresa de tecnología Bodea quiere combinar datos de personas y cuentas de diferentes fuentes de datos aisladas para dirigirse de forma eficaz a los clientes con un correo electrónico y una campaña de anuncios de LinkedIn para su nuevo producto. Bodea utiliza Marketo Engage como su plataforma de automatización de marketing y necesita segmentar una audiencia específica de B2B desde múltiples CRM que contengan datos de clientes.

## Primeros pasos

Este flujo de trabajo de tutorial se basa en varios servicios de Adobe Experience Platform como parte de la demostración. Si desea continuar, se recomienda comprender bien los siguientes servicios:

- [Modelo de datos de experiencia (XDM)](../xdm/home.md)
- [Fuentes](../sources/home.md)
- [Segmentación](../segmentation/home.md)
- [Destinos](../destinations/home.md)

## Crear esquemas para los datos

Como parte de la configuración inicial, el departamento de TI de Bodea necesita crear un esquema XDM para garantizar que sus datos sigan un formato estándar cuando se introduzcan en Platform y que se puedan procesar en distintos servicios de Platform y productos de Adobe Experience Cloud (como Adobe Analytics y Adobe Target).

>[!WARNING]
>
>Debe seguir los patrones de ingesta como se describe en la documentación de fuentes relevantes vinculada a través de este tutorial. No se garantiza que funcionen otros métodos de asignación de campos.

Adobe Experience Platform le permite generar automáticamente los esquemas y áreas de nombres necesarios para las fuentes de datos B2B. Esta herramienta garantiza que los esquemas creados describan los datos de una manera reutilizable estructurada. Siga las [Espacios de nombres B2B y documentación de utilidades de generación automática de esquemas](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) para obtener una referencia completa sobre el proceso de configuración.

En la interfaz de usuario de Adobe Experience Platform, el especialista en marketing de Bodea selecciona **[!UICONTROL Esquemas]** en el carril izquierdo, seguido del **[!UICONTROL Examinar]** pestaña . Dado que utilizaron la utilidad de generación automática de Marketo Engage, los nuevos esquemas vacíos aparecen en la lista y todos tienen el prefijo &quot;B2B&quot;.

![Ficha Examinar del espacio de trabajo del esquema](./assets/b2b-tutorial/empty-b2b-schemas.png)

La utilidad de generación automática definió la estructura del modelo de datos para los esquemas que utilizan clases XDM B2B estándar (como [Cuenta comercial XDM](../xdm/classes/b2b/business-account.md) y [Oportunidad comercial XDM](../xdm/classes/b2b/business-opportunity.md)) que capturan entidades de datos B2B fundamentales. Además, los esquemas B2B autogenerados basados en estas clases tienen relaciones preestablecidas que permiten casos de uso de segmentación avanzada. Aquí se puede realizar fácilmente cualquier grupo de campos adicional requerido para la estructura de datos a través de la interfaz de usuario. Consulte la [Guía de IU XDM, adición de grupos de campos a una sección de esquema](../xdm/ui/resources/schemas.md#add-field-groups) para obtener más información.

>[!NOTE]
> 
>Si no utiliza la utilidad de generador automático o si es necesario crear una nueva relación, consulte el tutorial en [creación de relaciones entre esquemas B2B](../xdm/tutorials/relationship-b2b.md).

El perfil del cliente en tiempo real combina datos de fuentes diferentes para crear perfiles consolidados de entidades B2B clave. Dado que los perfiles se generan en función de una sola clase, la utilidad de generación automática establece relaciones entre esquemas basadas en casos de uso comercial comunes. Como resultado, el equipo de Bodea está listo para introducir datos en función de sus esquemas B2B.

>[!NOTE]
> 
>Los espacios de nombres de identidad predeterminados, las claves principales y las relaciones creadas para los esquemas por la utilidad de generación automática se pueden descubrir fácilmente en el espacio de trabajo del esquema.
>
>![visualización de la identidad del esquema predeterminado y la interfaz de usuario de la relación](./assets/b2b-tutorial/schema-identity-relationship.png)

## Ingesta de datos en el Experience Platform

A continuación, el especialista en marketing de Bodea utiliza la variable [Conector del Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) para introducir datos en Platform para usarlos en servicios descendentes. También puede introducir datos utilizando una de las fuentes aprobadas para Real-Time CDP B2B Edition.

>[!NOTE]
> 
>Para saber qué conectores de origen están disponibles para su organización, puede ver el catálogo de fuentes en la interfaz de usuario de Platform. Para acceder al catálogo, seleccione **Fuentes** en el panel de navegación izquierdo, seleccione **Catálogo**.

Para crear una conexión entre una cuenta de Marketo y Platform, debe adquirir credenciales de autenticación. Consulte la [guía para obtener las credenciales de autenticación del conector de origen de Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) para obtener instrucciones detalladas.

Después de adquirir las credenciales de autenticación, el especialista en marketing de Bodea crea una conexión entre la cuenta de Marketo y la organización IMS de su plataforma. Consulte la documentación para obtener instrucciones sobre [cómo conectar una cuenta de Marketo mediante la interfaz de usuario de Platform](../sources/tutorials/ui/create/adobe-applications/marketo.md).

El conector de origen del Marketo Engage proporciona una función de asignación automática para facilitar el proceso de asignación de todos los campos de datos a los de los esquemas recién creados.

>[!NOTE]
> 
>Si ha realizado grupos de campos personalizados en sus esquemas XDM, es posible que tenga campos desconectados en esta fase del proceso. Asegúrese de comprobar todos los valores que rellenan los grupos de campos personalizados.

El especialista en marketing de Bodea comprueba que todos los grupos de campos estén correctamente asignados y continúa el proceso de configuración de fuentes inicializando un flujo de datos. Al crear un flujo de datos para incorporar datos de Marketo, los datos entrantes se pueden utilizar en los servicios de Platform descendentes. Durante el proceso de ingesta inicial, los datos se introducen en Experience Platform como un lote. Después de esto, los datos ingestados subsiguientes se transmiten al perfil con actualizaciones casi en tiempo real.

## Cree un segmento para evaluar los datos

La siguiente tarea es crear una audiencia para la nueva campaña de marketing por correo electrónico de Bodea basada en atributos específicos de entidades relacionadas en los datos de origen. Dentro de la interfaz de usuario de Platform, el especialista en marketing de Bodea selecciona primero **[!UICONTROL Segmentos]** en la navegación izquierda, **[!UICONTROL Crear segmento]**.

En este ejemplo, el segmento encuentra todas las personas que trabajan en el departamento de ventas y están relacionadas con cualquier cuenta que tenga al menos una oportunidad abierta. Este segmento requiere un vínculo entre la clase de Perfil individual XDM, la clase de cuenta empresarial XDM y la clase de oportunidad empresarial XDM.

![Segmento de caso de uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Para obtener instrucciones sobre cómo crear segmentos para evaluar los datos, consulte la [Guía de la interfaz de usuario del Generador de segmentos](../segmentation/ui/segment-builder.md). Para casos de uso de segmentación B2B más específicos, consulte la [información general sobre segmentación para Real-Time CDP B2B Edition](./segmentation/b2b.md).

El Generador de segmentos le permite crear una audiencia comercializable a partir de datos de Perfil del cliente en tiempo real y ver estimaciones de la audiencia potencial en función de la combinación de atributos, eventos y audiencias existentes que haya definido.

## Activar los datos evaluados en un destino

Una vez creado correctamente el segmento, se proporciona un resumen en la variable [!UICONTROL Detalles] del espacio de trabajo. Como no hay destinos activados actualmente para el segmento, el especialista en marketing de Bodea debe exportar la audiencia a un conjunto de datos al que se pueda acceder y en el que se pueda actuar.

Dentro de [!UICONTROL Segmentos] espacio de trabajo de la interfaz de usuario de la plataforma, el experto en marketing de Bodea selecciona **[!UICONTROL Activar en destino]**.

![Activar el segmento en un destino](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Consulte el tutorial en [activación de un segmento en un destino](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) para obtener información detallada sobre cómo hacerlo.

El especialista en marketing de Bodea activa el segmento en el destino de Marketo, lo que les permite insertar datos de segmento de Platform a Marketo Engage en forma de lista estática. Consulte la guía de [Destino de Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) para obtener más información.

## Pasos siguientes

Al seguir este tutorial, ha aprovechado correctamente los distintos servicios de Adobe Experience Platform utilizados por Real-Time CDP B2B Edition. Como resultado, ha aprendido a ingerir, segmentar, evaluar y exportar sus datos B2B como audiencias procesables que se pueden utilizar en distintos canales.
