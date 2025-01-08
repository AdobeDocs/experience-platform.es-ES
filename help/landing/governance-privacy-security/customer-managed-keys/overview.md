---
title: Claves administradas por el cliente en Adobe Experience Platform
description: Obtenga información sobre cómo configurar sus propias claves de cifrado para los datos almacenados en Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f2737355ca0652f434bd5f86acc65139f767e56f
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Claves administradas por el cliente en Adobe Experience Platform

Los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves de nivel de sistema. Si utiliza una aplicación basada en Platform, puede optar por utilizar sus propias claves de cifrado, lo que le proporciona un mayor control sobre la seguridad de los datos.

>[!AVAILABILITY]
>
>Si la implementación de Experience Platform se ejecuta en Amazon Web Service (AWS), tiene la opción de utilizar el Servicio de administración de claves (KMS) para el cifrado de datos de Platform. Un Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información acerca de la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud). Para obtener más información acerca de la creación y administración de claves de cifrado en AWS KMS, consulte la [Guía de cifrado de datos de AWS KMS](../key-management-service/overview.md).

>[!NOTE]
>
>Los datos de perfil del cliente almacenados en el almacén de perfiles [!DNL Azure Data Lake] de Platform y [!DNL Azure Cosmos DB] se cifran exclusivamente mediante CMK, una vez habilitado. La revocación de claves en los almacenes de datos principales puede tardar entre **unos minutos y 24 horas**, y puede tardar más, **hasta 7 días** para los almacenes de datos transitorios o secundarios. Para obtener más información, consulte las [implicaciones de revocar el acceso a claves en la sección](#revoke-access).

Este documento proporciona información general de alto nivel sobre el proceso para habilitar la función de claves administradas por el cliente (CMK) en Platform y la información sobre los requisitos previos necesaria para completar estos pasos.

>[!NOTE]
>
>Para los clientes de Customer Journey Analytics, siga las instrucciones que se encuentran en [documentación de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=es).

## Requisitos previos

Para ver y visitar la sección [!UICONTROL Cifrado] en Adobe Experience Platform, debe haber creado una función y asignado el permiso [!UICONTROL Administrar clave administrada por el cliente] a esa función. Cualquier usuario que tenga el permiso [!UICONTROL Administrar clave administrada por el cliente] puede habilitar CMK para su organización.

Para obtener más información sobre la asignación de funciones y permisos en Experience Platform, consulte la [documentación sobre la configuración de permisos](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar CMK, el almacén de claves [!DNL Azure] debe estar configurado con la siguiente configuración:

* [Habilitar protección contra purgas](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar eliminación suave](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurar el acceso mediante [!DNL Azure] control de acceso basado en roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Lea la documentación vinculada para comprender mejor el proceso.

## Resumen del proceso {#process-summary}

CMK está incluido en las ofertas Healthcare Shield y Privacy and Security Shield desde el Adobe. Una vez que su organización haya adquirido una licencia para una de estas ofertas, puede iniciar un proceso único para configurar la función.

>[!WARNING]
>
>Después de configurar CMK, no puede volver a las claves administradas por el sistema. Usted es responsable de administrar sus claves de forma segura y de proporcionar acceso a su aplicación Key Vault, Key y CMK dentro de [!DNL Azure] para evitar la pérdida de acceso a sus datos.

El proceso es el siguiente:

1. [Configura una [!DNL Azure] Caja fuerte de claves](./azure-key-vault-config.md) basada en las políticas de tu organización y [genera una clave de cifrado](./azure-key-vault-config.md#generate-a-key) que finalmente se compartirá con el Adobe.
1. Configure la aplicación CMK con su inquilino de [!DNL Azure] a través de [llamadas API](./api-set-up.md#register-app) o la [IU](./ui-set-up.md#register-app).
1. Envíe su ID de clave de cifrado al Adobe e inicie el proceso de habilitación de la característica [en la interfaz de usuario](./ui-set-up.md#send-to-adobe) o con una [llamada de API](./api-set-up.md#send-to-adobe).
1. Compruebe el estado de la configuración para comprobar si CMK se ha habilitado en [la interfaz de usuario](./ui-set-up.md#check-status) o con una [llamada API](./api-set-up.md#check-status).

Una vez completado el proceso de configuración, todos los datos incorporados en Platform en todas las zonas protegidas se cifrarán con la configuración de clave de [!DNL Azure]. Para usar CMK, aprovechará la funcionalidad [!DNL Microsoft Azure] que puede formar parte de su [programa de vista previa pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Implicaciones de revocar el acceso a claves {#revoke-access}

Revocar o deshabilitar el acceso a la aplicación Key Vault, key o CMK puede causar interrupciones significativas, que incluyen cambios importantes en las operaciones de la plataforma. Una vez deshabilitadas estas claves, es posible que no se pueda acceder a los datos en Platform y que las operaciones de flujo descendente que dependan de estos datos dejen de funcionar. Es crucial comprender completamente los impactos descendentes antes de realizar cambios en las configuraciones clave.

Si decide revocar el acceso de Platform a sus datos, puede hacerlo eliminando el rol de usuario asociado con la aplicación de Key Vault en [!DNL Azure].

### Escalas de tiempo de propagación {#propagation-timelines}

Una vez revocado el acceso a la clave desde el almacén de claves [!DNL Azure], los cambios se propagarán de la siguiente manera:

| **Tipo de tienda** | **Descripción** | **Cronología** |
|---|---|---|
| Almacenes de datos principales | Estas tiendas incluyen Azure Data Lake y Azure Cosmos DB Profile. Una vez revocado el acceso a las claves, los datos se vuelven inaccesibles. | Entre **pocos minutos y 24 horas**. |
| Almacenes de datos en caché/transitorios | Incluye almacenes de datos utilizados para el rendimiento y la funcionalidad de la aplicación principal. El impacto de la revocación de claves se retrasa. | **Hasta 7 días**. |

Por ejemplo, el panel Perfil seguirá mostrando los datos de su caché durante un máximo de siete días antes de que los datos caduquen y se actualicen. Del mismo modo, volver a habilitar el acceso a la aplicación tarda la misma cantidad de tiempo en restaurar la disponibilidad de los datos en estas tiendas.

>[!NOTE]
>
>Existen dos excepciones específicas de casos de uso a la caducidad de conjuntos de datos de siete días en datos no principales (almacenados en caché/transitorios). Consulte su documentación correspondiente para obtener más información sobre estas funciones.<ul><li>[Abreviador de URL de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=es#message-preset-sms)</li><li>[Proyecciones de Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Pasos siguientes

Para comenzar el proceso, empieza por [configurar una [!DNL Azure] caja fuerte de claves](./azure-key-vault-config.md) y [generar una clave de cifrado](./azure-key-vault-config.md#generate-a-key) para compartirla con el Adobe.
