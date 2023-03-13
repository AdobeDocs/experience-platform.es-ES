---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: conector del Marketo Engage
description: Este documento proporciona información general sobre el conector de origen del Marketo Engage, incluida la información sobre su autenticación, asignación y latencia de datos.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: d8cd69524d984fdb828447287f3f4a4fe5913d61
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# [!DNL Marketo Engage] conector

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (en lo sucesivo, &quot;[!DNL Marketo]&quot;) es una solución completa para la gestión de clientes potenciales y para los especialistas en marketing B2B que buscan transformar las experiencias de los clientes al interactuar en todas las etapas de los recorridos de compra complejos.

Con el [!DNL Marketo] conector de origen, puede traer datos B2B desde [!DNL Marketo] Vaya a Platform y mantenga estos datos actualizados mediante aplicaciones conectadas a Platform.

>[!IMPORTANT]
>
>Debe tener acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para utilizar todos los conjuntos de datos de Marketo para la segmentación con [Perfil del cliente en tiempo real](../../../../profile/home.md). Sin Real-Time CDP B2B Edition, aún puede utilizar el origen de Marketo para llevar los datos de los conjuntos de datos de personas y actividades al Perfil del cliente en tiempo real para la segmentación.

Este documento proporciona información general sobre [!DNL Marketo] conector de origen, incluida información sobre cómo autenticar el conector, cómo asignar [!DNL Marketo] a Experience Data Model (XDM) y la latencia de datos del conector.

## Autentique su [!DNL Marketo] conector

Para poder conectarse [!DNL Marketo] a Platform, primero debe recuperar los valores de la `munchkinId`, `clientId`, y `clientSecret`.

Consulte los pasos descritos en la sección [Autenticar el conector de origen de Marketo](./marketo-auth.md) para recuperar sus credenciales.

## Configurar asignación de organización de Adobe

Antes de poder establecer conjuntos de asignaciones para [!DNL Marketo], primero debe configurar Asignación de organización de Adobe. Para ver los pasos detallados sobre cómo completar esto, consulte la guía de [configuración de la asignación de organización de Adobe para [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Configurar áreas de nombres B2B y la utilidad de generación automática de esquemas

A continuación, utilice el área de nombres B2B y la utilidad de generación automática de esquemas para configurar la consola del desarrollador de Platform y el entorno de Postman. Esto le permite rellenar automáticamente los espacios de nombres y esquemas B2B. Para obtener instrucciones detalladas, consulte la guía de [configuración de las áreas de nombres B2B y la utilidad de generación automática de esquemas](./marketo-namespaces.md)

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes que le permiten introducir datos de fuentes de terceros para utilizarlos en servicios de Platform secundarios.

El cumplimiento de los estándares XDM permite que los datos se incorporen de manera uniforme al ecosistema de Platform, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM y su función en Platform, consulte la [Información general del sistema XDM](../../../../xdm/home.md).

## Asignación de campos desde [!DNL Marketo] a XDM

Para establecer una conexión de origen entre [!DNL Marketo] y Platform, los campos de datos de origen de Marketo deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Marketo] conjuntos de datos y Platform:

* [Actividades](../mapping/marketo.md#activities)
* [Programas](../mapping/marketo.md#programs)
* [Pertenencia a programas](../mapping/marketo.md#program-memberships)
* [Compañías](../mapping/marketo.md#companies)
* [Listas estáticas](../mapping/marketo.md#static-lists)
* [Pertenencia a lista estática](../mapping/marketo.md#static-list-memberships)
* [Cuentas con nombre](../mapping/marketo.md#named-accounts)
* [Oportunidades](../mapping/marketo.md#opportunities)
* [Funciones de contacto de oportunidad](../mapping/marketo.md#opportunity-contact-roles)
* [Personas](../mapping/marketo.md#persons)

## Latencia esperada de [!DNL Marketo] datos en Platform

En la tabla siguiente se describe la latencia esperada para traer [!DNL Marketo] en Platform, en función de la naturaleza de la ingesta y el destino deseado:

| Destino | Latencia esperada |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1 minuto |
| Lago de datos | &lt; 60 minutos |

## Pasos siguientes y recursos adicionales

La siguiente documentación proporciona más información sobre la creación de un [!DNL Marketo] conexión de origen:

* Para obtener información sobre cómo conectar su [!DNL Marketo] datos en Platform, lea el tutorial sobre [creación de un [!DNL Marketo] conexión de origen en la interfaz de usuario](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Para obtener información sobre cómo configurar los esquemas e introducir datos de actividad personalizados, lea el tutorial sobre [crear una conexión de origen y un flujo de datos para [!DNL Marketo] datos de actividad personalizados](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* Para obtener información sobre la configuración subyacente de los espacios de nombres B2B y esquemas utilizados con [!DNL Marketo], lea la documentación de [Espacios de nombres y esquemas B2B](./marketo-namespaces.md).
* Para obtener información sobre cómo encontrar su [!DNL Marketo] munchkin ID y, a continuación, para generar sus credenciales, lea la [[!DNL Marketo] guía de autenticación](./marketo-auth.md).
* Para obtener información sobre las reglas de asignación específicas aplicables a [!DNL Marketo] conjuntos de datos, lea la documentación sobre [[!DNL Marketo] asignaciones de campos](../mapping/marketo.md).
* Para obtener información general sobre [!DNL Real-Time Customer Data Platform B2B Edition] y sus funciones, lea la documentación sobre [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
