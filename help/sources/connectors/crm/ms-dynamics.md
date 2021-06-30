---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dinámica;Dynamics
solution: Experience Platform
title: Información general del conector de origen de Microsoft Dynamics
topic-legacy: overview
description: Obtenga información sobre cómo conectar Microsoft Dynamics a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---

# Conector de Microsoft Dynamics

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

[!DNL Experience Platform] proporciona asistencia para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Microsoft Dynamics].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

>[!IMPORTANT]
>
>El conector de origen [!DNL Microsoft Dynamics] actualmente no admite conectividad de la misma región con Platform. Esto significa que si la instancia de Azure está usando la misma región de red que Platform, no se puede establecer una conexión con orígenes de Platform. Actualmente, solo se admite la conectividad entre regiones. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información.

La documentación siguiente proporciona información sobre cómo conectar [!DNL Microsoft Dynamics] a [!DNL Platform] mediante API o la interfaz de usuario:

## Conectar [!DNL Microsoft Dynamics] a [!DNL Platform] mediante API

- [Creación de una conexión base de Microsoft Dynamics mediante la API de servicio de flujo](../../tutorials/api/create/crm/ms-dynamics.md)
- [Explorar la estructura de datos y el contenido de un origen de CRM mediante la API de servicio de flujo](../../tutorials/api/explore/crm.md)
- [Crear un flujo de datos para un origen CRM mediante la API de servicio de flujo](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Microsoft Dynamics] a [!DNL Platform] mediante la interfaz de usuario

- [Crear una conexión de origen de Microsoft Dynamics en la interfaz de usuario](../../tutorials/ui/create/crm/dynamics.md)
- [Crear un flujo de datos para una conexión CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
