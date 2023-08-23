---
title: Resumen de origen de SugarCRM
description: Aprenda a conectar SugarCRM a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# [!DNL SugarCRM]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde una aplicación CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) es un sistema de administración de la relación con los clientes (CRM). [!DNL SugarCRM]La funcionalidad de incluye automatización de la fuerza de ventas, campañas de marketing, asistencia al cliente, colaboración, CRM móvil, CRM social y creación de informes.

El [!DNL SugarCRM] Esta fuente de datos permite introducir datos de cuentas, contactos y eventos de los siguientes extremos de API:

* [Cuentas](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [Contactos](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [Eventos](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM] utiliza tokens de portador como mecanismo de autenticación para comunicarse con el [!DNL SugarCRM] Las API de cuenta y contacto y [!DNL SugarCRM] API de eventos.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos

Antes de crear un [!DNL SugarCRM] conexión de origen, primero debe asegurarse de que dispone de lo siguiente:

* A [!DNL SugarMarket] cuenta. Debe ponerse en contacto con [!DNL SugarCRM] Administrador de cuentas para obtener un válido [!DNL SugarMarket] cuenta si aún no dispone de una.

* Un nombre de usuario y una cuenta de API únicos separados de cualquier cuenta de usuario asociada con el proceso de marketing o ventas. Esta combinación única de nombre de usuario y cuenta debe tener permisos de acceso a API. Para obtener más información sobre el proceso para configurar una cuenta, visite la [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) documentación.

## Connect [!DNL SugarCRM Accounts & Contacts] a Platform

* [Cree una conexión de origen para traer [!DNL SugarCRM Accounts & Contacts] datos a Platform mediante API](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [Cree una conexión de origen para traer [!DNL SugarCRM Accounts & Contacts] datos a Platform mediante la interfaz de usuario de](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)


## Connect [!DNL SugarCRM Events] a Platform

* [Cree una conexión de origen para traer [!DNL SugarCRM Events] datos a Platform mediante API](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Cree una conexión de origen para traer [!DNL SugarCRM Events] datos a Platform mediante la interfaz de usuario de](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [Crear un flujo de datos para una conexión de origen CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
