---
title: Implementar etiquetas de JavaScript para administrar el consentimiento del cliente
description: Obtenga información sobre cómo administrar las señales de inclusión y exclusión de clientes para distintas soluciones de Adobe en Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 93%

---

# Implementar etiquetas de JavaScript para administrar el consentimiento del cliente

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD), requieren que las compañías puedan administrar el consentimiento de los usuarios. Es posible que los clientes de Adobe exijan a los visitantes que acepten su inclusión antes de que se ejecuten las soluciones de Adobe para un visitante determinado. Los visitantes deben tener la capacidad de gestionar su estado de inclusión y exclusión.

Los clientes de Adobe Experience Cloud requieren diversas implementaciones de estos requisitos. Algunos utilizan gestores de consentimiento a nivel empresarial, mientras que otros crean los suyos propios.

Los desarrolladores de extensiones de Adobe Experience Platform usan las extensiones y el generador de reglas para definir las soluciones de inclusión y de exclusión.

Este documento contiene información sobre cómo evitar que las etiquetas de Adobe se activen antes de la adquisición del consentimiento.

## Advertising Cloud

Adobe Experience Platform no activa [!DNL Advertising Cloud] automáticamente. [!DNL Advertising Cloud] solo se activa si lo indica específicamente en una acción de regla. Utilice las condiciones de regla para determinar cuándo y qué se debe activar. Por ejemplo, para utilizar cookies para determinar el estado de inclusión, configure un elemento de datos para que lea esa cookie y úselo como una condición de la regla para determinar cuándo se debe activar la acción Track Conversion.

Las integraciones con los gestores de consentimiento (como OneTrust) pueden configurar y rastrear las cookies de consentimiento de los clientes, que luego pueden utilizarse en el generador de reglas.

## Analytics

En la sección Link Tracking de las opciones de configuración de la extensión de [!DNL Analytics], asegúrese de que las siguientes opciones *no* estén seleccionadas:

* Rastrear vínculos de descarga
* Rastrear vínculos salientes

Cuando estos ajustes no están seleccionados, Platform no activa [!DNL Adobe Analytics] automáticamente. [!DNL Analytics] se activa únicamente si se indica específicamente en una acción de regla. Utilice las condiciones de regla para determinar cuándo y qué se debe activar. Por ejemplo, para utilizar cookies para determinar el estado de inclusión, configure un elemento de datos para que lea esa cookie y utilícelo como una condición en la regla para determinar cuándo activar la acción Send Beacon.

Por otro lado, podría considerar la posibilidad de utilizar el [objeto de inclusión de Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es) para controlar la activación de esta etiqueta de forma conjunta con su plataforma de administración de consentimiento.

Las integraciones con los gestores de consentimiento (como OneTrust) pueden configurar y rastrear las cookies de consentimiento de los clientes, que luego pueden utilizarse en el generador de reglas.

## Audience Manager

DIL está configurado actualmente para activarse automáticamente si se coloca en una página de cliente. Considere la posibilidad de utilizar el [objeto de inclusión de Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es) para controlar la activación de esta etiqueta de forma conjunta con su plataforma de administración de consentimiento.

[!DNL Adobe] recomienda utilizar reenvío del lado del servidor en [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] actualmente se activa automáticamente si se coloca en una página de cliente.

Considere la posibilidad de utilizar el [objeto de inclusión de Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es) para controlar la activación de esta etiqueta de forma conjunta con su plataforma de administración de consentimiento.

## Target

Adobe Experience Platform no activa [!DNL Target] automáticamente. [!DNL Target] se activa únicamente si se indica específicamente en una acción de regla. Utilice las condiciones de regla para determinar cuándo y qué se debe activar. Por ejemplo, para utilizar cookies para determinar el estado de inclusión, configure un elemento de datos para que lea esa cookie y utilícelo como una condición en la regla para determinar cuándo activar la acción Load [!DNL Target].

Por otro lado, podría considerar la posibilidad de utilizar el [objeto de inclusión de Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=es) para controlar la activación de esta etiqueta de forma conjunta con su plataforma de administración de consentimiento.

Las integraciones con los gestores de consentimiento (como OneTrust) pueden configurar y rastrear las cookies de consentimiento de los clientes, que luego pueden utilizarse en el generador de reglas.
