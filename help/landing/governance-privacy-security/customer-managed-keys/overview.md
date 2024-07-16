---
title: Claves administradas por el cliente en Adobe Experience Platform
description: Obtenga información sobre cómo configurar sus propias claves de cifrado para los datos almacenados en Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Claves administradas por el cliente en Adobe Experience Platform

Los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves de nivel de sistema. Si utiliza una aplicación basada en Platform, puede optar por utilizar sus propias claves de cifrado, lo que le proporciona un mayor control sobre la seguridad de los datos.

>[!NOTE]
>
>Los datos del lago de datos de Adobe Experience Platform y del almacén de perfiles se cifran con CMK. Se consideran sus almacenes de datos principales.

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

## Revocar acceso {#revoke-access}

Si desea revocar el acceso de Platform a sus datos, puede quitar el rol de usuario asociado con la aplicación del almacén de claves en [!DNL Azure].

>[!WARNING]
>
>Deshabilitar el almacén de claves, la clave o la aplicación CMK puede provocar un cambio importante. Una vez que la aplicación key vault, Key o CMK esté deshabilitada y ya no se pueda acceder a los datos en Platform, ya no será posible realizar ninguna operación descendente relacionada con esos datos. Asegúrese de comprender el impacto descendente de la revocación del acceso de Platform a la clave antes de realizar cambios en la configuración.

Después de quitar el acceso a la clave o de deshabilitar o eliminar la clave del almacén de claves [!DNL Azure], esta configuración puede tardar entre unos minutos y 24 horas en propagarse a los almacenes de datos principales. Los flujos de trabajo de Platform también incluyen los almacenes de datos en caché y transitorios necesarios para el rendimiento y la funcionalidad de la aplicación principal. La propagación de la revocación de CMK a través de estos almacenes en caché y transitorios puede tardar hasta siete días, según lo determinado por sus flujos de trabajo de procesamiento de datos. Por ejemplo, esto significa que el panel Perfil conservaría y mostraría datos de su almacén de datos de caché y tardaría siete días en caducar los datos que se mantienen en los almacenes de datos de caché como parte del ciclo de actualización. El mismo retraso de tiempo se aplica a los datos que vuelven a estar disponibles cuando se vuelve a habilitar el acceso a la aplicación.

>[!NOTE]
>
>Existen dos excepciones específicas de casos de uso a la caducidad de conjuntos de datos de siete días en datos no principales (almacenados en caché/transitorios). Consulte su documentación correspondiente para obtener más información sobre estas funciones.<ul><li>[Abreviador de URL de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=es#message-preset-sms)</li><li>[Proyecciones de Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Pasos siguientes

Para comenzar el proceso, empieza por [configurar una [!DNL Azure] caja fuerte de claves](./azure-key-vault-config.md) y [generar una clave de cifrado](./azure-key-vault-config.md#generate-a-key) para compartirla con el Adobe.
