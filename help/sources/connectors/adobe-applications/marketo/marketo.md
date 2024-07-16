---
keywords: Experience Platform;inicio;temas populares;Marketo Engage;marketo engage;marketo
solution: Experience Platform
title: conector del Marketo Engage
description: Este documento proporciona información general sobre el conector de origen del Marketo Engage, incluida la información sobre su autenticación, asignación y latencia de datos.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Conector [!DNL Marketo Engage]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) es una solución completa para la administración de posibles clientes y para los especialistas en marketing B2B que buscan transformar las experiencias de los clientes al interactuar en todas las etapas de los recorridos de compra complejos.

Con el conector de origen [!DNL Marketo Engage], puede llevar los datos B2B de [!DNL Marketo Engage] a Platform y mantenerlos actualizados mediante aplicaciones conectadas a Platform.

>[!IMPORTANT]
>
>Debe tener acceso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) para usar todos los conjuntos de datos de Marketo para la segmentación con el [Perfil del cliente en tiempo real](../../../../profile/home.md). Sin Real-Time CDP B2B Edition, aún puede utilizar el origen de Marketo para llevar los datos de los conjuntos de datos de personas y actividades al Perfil del cliente en tiempo real para la segmentación.

Este documento proporciona información general sobre el conector de origen [!DNL Marketo Engage], incluida información sobre cómo autenticar el conector, cómo asignar campos de [!DNL Marketo Engage] al modelo de datos de experiencia (XDM) y la latencia de datos del conector.

## Configurar asignación de organización de Adobe

Para poder establecer conjuntos de asignaciones para [!DNL Marketo Engage], primero debe configurar la asignación de organización de Adobe. Para ver los pasos detallados sobre cómo completar esto, consulte la guía de [configuración de la asignación de organización de Adobe para [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autenticar el conector [!DNL Marketo Engage]

Para conectar [!DNL Marketo Engage] a Platform, primero debe recuperar los valores de `munchkinId`, `clientId` y `clientSecret`.

Consulte los pasos descritos en el documento [Autenticar el conector de origen de Marketo](./marketo-auth.md) para recuperar sus credenciales.

## Configurar áreas de nombres B2B y la utilidad de generación automática de esquemas

A continuación, utilice el área de nombres B2B y la utilidad de generación automática de esquemas para configurar la consola del desarrollador de Platform y el entorno de Postman. Esto le permite rellenar automáticamente los espacios de nombres y esquemas B2B. Para obtener instrucciones detalladas, consulte la guía sobre [configuración de las áreas de nombres B2B y la utilidad de generación automática de esquemas](./marketo-namespaces.md)

## Modelo de datos de experiencia (XDM)

XDM es una especificación documentada públicamente que proporciona estructuras y definiciones comunes que le permiten introducir datos de fuentes de terceros para utilizarlos en servicios de Platform secundarios.

El cumplimiento de los estándares XDM permite que los datos se incorporen de manera uniforme al ecosistema de Platform, lo que facilita la entrega de datos y la recopilación de información.

Para obtener más información sobre XDM y su función en Platform, consulte la [descripción general del sistema XDM](../../../../xdm/home.md).

## Asignación de campos de [!DNL Marketo Engage] a XDM

Para establecer una conexión de origen entre [!DNL Marketo Engage] y Platform, los campos de datos de origen de Marketo deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Marketo Engage] conjuntos de datos y Platform:

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

## Latencia esperada de [!DNL Marketo Engage] datos en la plataforma

En la tabla siguiente se describe la latencia esperada para llevar los datos de [!DNL Marketo Engage] a Platform, según la naturaleza de la ingesta y el destino deseado:

| Destino | Latencia esperada |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minutos |
| Lago de datos | &lt; 60 minutos |

>[!NOTE]
>
>Las cifras de latencia anteriores representan expectativas con un nivel de confianza del 95 %. Las latencias reales variarán y pueden superar esas cifras en un 50 % en casos excepcionales.

## Pasos siguientes y recursos adicionales

La siguiente documentación proporciona más información sobre cómo crear una conexión de origen de [!DNL Marketo Engage]:

* Para obtener información sobre cómo conectar tus datos de [!DNL Marketo Engage] a Platform, lee el tutorial sobre [creación de una conexión de origen en la interfaz de usuario [!DNL Marketo Engage] .](../../../tutorials/ui/create/adobe-applications/marketo.md)
   * Para obtener información sobre cómo configurar los esquemas e ingerir datos de actividad personalizados, lea el tutorial sobre [creación de una conexión de origen y un flujo de datos para [!DNL Marketo Engage] datos de actividad personalizados](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Para obtener información sobre cómo migrar su asignación ECID del conjunto de datos [!DNL Person] al conjunto de datos [!DNL Activity], lea la [guía de migración de asignación ECID](./migration.md).
* Para obtener información sobre la configuración subyacente de los esquemas y áreas de nombres B2B utilizados con [!DNL Marketo Engage], lea la documentación de [esquemas y áreas de nombres B2B](./marketo-namespaces.md).
* Para obtener información sobre cómo encontrar tu ID de munchkin [!DNL Marketo Engage] y generar tus credenciales, lee la [[!DNL Marketo Engage] guía de autenticación](./marketo-auth.md).
* Para obtener información sobre las reglas de asignación específicas que se aplican a [!DNL Marketo Engage] conjuntos de datos, lea la documentación sobre [[!DNL Marketo Engage] asignaciones de campos](../mapping/marketo.md).
* Para obtener información general sobre [!DNL Real-Time Customer Data Platform B2B Edition] y sus características, lea la documentación sobre [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
