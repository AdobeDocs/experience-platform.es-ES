---
title: Conexión De Demandbase Intent A Experience Platform Mediante La IU
description: Aprenda a conectar Demandbase Intent a Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 11%

---

# Conectar [!DNL Demandbase Intent] a Experience Platform mediante la interfaz de usuario

Lea esta guía para obtener información sobre cómo conectar su cuenta de [!DNL Demandbase Intent] a Adobe Experience Platform mediante la interfaz de usuario.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a públicos específicos con precisión y captarlos en todos los canales disponibles.
* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

## Navegar por el catálogo de fuentes {#navigate}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Sources]. Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

Seleccione **[!DNL Demandbase Intent]** en la categoría *[!UICONTROL B2B]* y luego seleccione **[!UICONTROL Configurar]**.

>[!TIP]
>
>Los orígenes del catálogo de orígenes muestran la opción **[!UICONTROL Set up]** cuando un origen determinado aún no tiene una cuenta autenticada. Una vez que existe una cuenta autenticada, esta opción cambia a **[!UICONTROL Agregar datos]**.



## Usar una cuenta existente {#existing}

## Crear una nueva cuenta {#create}

## Proporcionar detalles del flujo de datos {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_domain"
>title="Fuente de dominio"
>abstract="Aunque Adobe utiliza el sitio web accountOrganization.website de XDM, puede haber clientes que utilicen campos personalizados para sus respectivos sitios web. Por lo tanto, debe asegurarse de que el origen del dominio sea el campo dominio/sitio web que coincidirá con los registros de cuenta de Demandbase respecto a las cuentas de Experience Platform."

## Programar flujo de datos {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_schedule"
>title="Programación del flujo de datos"
>abstract="Demandbase envía datos una vez a la semana el lunes por la mañana a las 17:00 UTC. Por lo tanto, debe configurar la hora de inicio de la ingesta después de las 17:00 UTC. Además, debe confirmar el tiempo de ingesta con Demandbase, ya que puede modificar su programación al soltar archivos en Adobe."

## Revisar flujo de datos {#review-dataflow}
