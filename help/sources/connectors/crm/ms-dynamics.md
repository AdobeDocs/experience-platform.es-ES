---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Información general sobre el conector de origen de Microsoft Dynamics
description: Obtenga información sobre cómo conectar Microsoft Dynamics a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Conector de Microsoft Dynamics

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona compatibilidad con la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Microsoft Dynamics].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Asignación de campos desde [!DNL Microsoft Dynamics] a XDM

Para establecer una conexión de origen entre [!DNL Microsoft Dynamics] y Platform, la [!DNL Microsoft Dynamics] Los campos de datos de origen deben asignarse a sus campos XDM de destino adecuados antes de introducirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Microsoft Dynamics] conjuntos de datos y Platform:

- [Contactos](../adobe-applications/mapping/dynamics.md#contacts)
- [Posibles clientes](../adobe-applications/mapping/dynamics.md#leads)
- [Cuentas](../adobe-applications/mapping/dynamics.md#accounts)
- [Oportunidades](../adobe-applications/mapping/dynamics.md#opportunities)
- [Funciones de contacto de oportunidad](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campañas](../adobe-applications/mapping/dynamics.md#campaigns)
- [Lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Miembros de lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Microsoft Dynamics] hasta [!DNL Platform] mediante las API de o la interfaz de usuario de:

## Connect [!DNL Microsoft Dynamics] hasta [!DNL Platform] uso de API

- [Crear una conexión base de Microsoft Dynamics mediante la API de Flow Service](../../tutorials/api/create/crm/ms-dynamics.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

## Connect [!DNL Microsoft Dynamics] hasta [!DNL Platform] uso de la IU

- [Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario](../../tutorials/ui/create/crm/dynamics.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
