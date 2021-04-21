---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketing para interactuar;marketing
solution: Experience Platform
title: Conector del Marketo Engage
topic-legacy: overview
description: Este documento proporciona información general sobre el conector de origen del Marketo Engage, incluida información sobre su autenticación, asignación y latencia de datos.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---


# Conector (Beta) [!DNL Marketo Engage]

>[!IMPORTANT]
>
>El origen [!DNL Marketo Engage] está actualmente en versión beta. Sus características y la documentación están sujetas a cambios.

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (en adelante, &quot;[!DNL Marketo]&quot;) es una solución completa para la gestión de clientes potenciales y para los especialistas en marketing B2B que buscan transformar las experiencias de los clientes al interactuar en todas las etapas de los recorridos de compra complejos.

Con el conector de origen [!DNL Marketo], puede traer datos B2B de [!DNL Marketo] a Platform y mantenerlos actualizados mediante aplicaciones conectadas a Platform.

Este documento proporciona información general sobre el conector de origen [!DNL Marketo], incluida información sobre cómo autenticar el conector, cómo asignar campos [!DNL Marketo] al Modelo de datos de experiencia (XDM) y la latencia de datos del conector.

## Autenticar el conector [!DNL Marketo]

Para conectar [!DNL Marketo] a Platform, primero debe recuperar los valores de `munchkinId`, `clientId` y `clientSecret`.

Consulte los pasos descritos en el documento [Autenticar el conector de origen de Marketo](./marketo-auth.md) para recuperar las credenciales.

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes que le permiten introducir datos de fuentes de terceros para usarlos en servicios de Platform descendentes.

El cumplimiento de las normas XDM permite incorporar los datos de manera uniforme al ecosistema de la Plataforma, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM y su función en Platform, consulte la [información general del sistema XDM](../../../../xdm/home.md).

## Asignación de campos de [!DNL Marketo] a XDM

Para establecer una conexión de origen entre [!DNL Marketo] y Platform, los campos de datos de origen de Marketo deben asignarse a los campos XDM de destino adecuados antes de ingerirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Marketo] conjuntos de datos y Platform:

* [Actividades](../mapping/marketo.md#activities)
* [Programas](../mapping/marketo.md#programs)
* [Pertenencia a programas](../mapping/marketo.md#program-memberships)
* [Compañías](../mapping/marketo.md#companies)
* [Listas estáticas](../mapping/marketo.md#static-lists)
* [Pertenencia a listas estáticas](../mapping/marketo.md#static-list-memberships)
* [Cuentas con nombre](../mapping/marketo.md#named-accounts)
* [Oportunidades](../mapping/marketo.md#opportunities)
* [Funciones de contacto de oportunidad](../mapping/marketo.md#opportunity-contact-roles)
* [Personas](../mapping/marketo.md#persons)

## Latencia esperada de [!DNL Marketo] datos en Platform

La siguiente tabla describe la latencia esperada para incorporar [!DNL Marketo] datos a Platform, según la naturaleza de la ingesta y el destino deseado:

| Destino | Latencia esperada |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Lago de datos | &lt; 60 minutos |

## Pasos siguientes y recursos adicionales

La siguiente documentación proporciona más información sobre la creación de una conexión de origen [!DNL Marketo]:

* Para obtener información sobre cómo conectar los datos [!DNL Marketo] a Platform, consulte el tutorial sobre la [creación de un conector de origen de Marketo en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Para obtener información sobre la configuración subyacente de los espacios de nombres y esquemas B2B utilizados con [!DNL Marketo], consulte la documentación de [Espacios de nombres B2B y esquemas](./marketo-namespaces.md).
* Para obtener información sobre cómo encontrar su [!DNL Marketo] ID de munchkin y generar sus credenciales, consulte la [[!DNL Marketo] guía de autenticación](./marketo-auth.md).
* Para obtener información sobre las reglas de asignación específicas que se aplican a los conjuntos de datos [!DNL Marketo], consulte la documentación sobre [[!DNL Marketo] asignaciones de campo](../mapping/marketo.md).