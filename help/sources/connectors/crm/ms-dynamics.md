---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Información general sobre el conector Microsoft Dynamics Source
description: Obtenga información sobre cómo conectar Microsoft Dynamics a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# Conector de Microsoft Dynamics

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona soporte para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Microsoft Dynamics].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Asignación de campos de [!DNL Microsoft Dynamics] a XDM

Para establecer una conexión de origen entre [!DNL Microsoft Dynamics] y Experience Platform, los campos de datos de origen [!DNL Microsoft Dynamics] deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Experience Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Microsoft Dynamics] conjuntos de datos y Experience Platform:

- [Contactos](../adobe-applications/mapping/dynamics.md#contacts)
- [Posibles clientes](../adobe-applications/mapping/dynamics.md#leads)
- [Cuentas](../adobe-applications/mapping/dynamics.md#accounts)
- [Oportunidades](../adobe-applications/mapping/dynamics.md#opportunities)
- [Funciones de contacto de oportunidad](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campañas](../adobe-applications/mapping/dynamics.md#campaigns)
- [Lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Miembros de lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La siguiente documentación proporciona información sobre cómo conectar [!DNL Microsoft Dynamics] a [!DNL Experience Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Microsoft Dynamics] a [!DNL Experience Platform] mediante API

- [Crear una conexión base de Microsoft Dynamics mediante la API de Flow Service](../../tutorials/api/create/crm/ms-dynamics.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Microsoft Dynamics] a [!DNL Experience Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario](../../tutorials/ui/create/crm/dynamics.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
