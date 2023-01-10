---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;Dynamics
solution: Experience Platform
title: Información general del conector de origen de Microsoft Dynamics
description: Obtenga información sobre cómo conectar Microsoft Dynamics a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Conector de Microsoft Dynamics

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona asistencia para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con los proveedores de CRM incluye [!DNL Microsoft Dynamics].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Asignación de campos desde [!DNL Microsoft Dynamics] a XDM

Para establecer una conexión de origen entre [!DNL Microsoft Dynamics] y Platform, [!DNL Microsoft Dynamics] los campos de datos de origen deben asignarse a los campos XDM de destino correspondientes antes de ingerirse en Platform.

Consulte lo siguiente para obtener información detallada sobre las reglas de asignación de campos entre [!DNL Microsoft Dynamics] conjuntos de datos y plataforma:

- [Contactos](../adobe-applications/mapping/dynamics.md#contacts)
- [Posibles clientes](../adobe-applications/mapping/dynamics.md#leads)
- [Cuentas](../adobe-applications/mapping/dynamics.md#accounts)
- [Oportunidades](../adobe-applications/mapping/dynamics.md#opportunities)
- [Funciones de contacto de oportunidad](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campañas](../adobe-applications/mapping/dynamics.md#campaigns)
- [Lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Miembros de la lista de marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La siguiente documentación proporciona información sobre cómo conectar [!DNL Microsoft Dynamics] a [!DNL Platform] mediante API o la interfaz de usuario:

## Connect [!DNL Microsoft Dynamics] a [!DNL Platform] uso de API

- [Creación de una conexión base de Microsoft Dynamics mediante la API de servicio de flujo](../../tutorials/api/create/crm/ms-dynamics.md)
- [Exploración de tablas de datos mediante la API de servicio de flujo](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen CRM mediante la API de servicio de flujo](../../tutorials/api/collect/crm.md)

## Connect [!DNL Microsoft Dynamics] a [!DNL Platform] uso de la interfaz de usuario

- [Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario](../../tutorials/ui/create/crm/dynamics.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
