---
title: Claves gestionadas por el cliente en Adobe Experience Platform
description: Obtenga información sobre cómo configurar sus propias claves de cifrado para los datos almacenados en Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c1a28a4b1ce066a87bb7b34b2524800f9d8f1ca0
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# Claves gestionadas por el cliente en Adobe Experience Platform

Los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves de nivel de sistema. Si utiliza una aplicación basada en Platform, puede optar por utilizar sus propias claves de cifrado, lo que le proporciona un mayor control sobre la seguridad de los datos.

>[!AVAILABILITY]
>
>Adobe Experience Platform admite claves administradas por el cliente (CMK) tanto para Microsoft Azure como para Amazon Web Service (AWS). Un Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Si la implementación se ejecuta en AWS, tiene la opción de utilizar el Servicio de administración de claves (KMS) para el cifrado de datos de Platform. Para obtener más información sobre la infraestructura compatible, consulte la [descripción general de la nube múltiple de Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Para obtener más información acerca de la creación y administración de claves de cifrado en AWS KMS, consulte la [Guía de cifrado de datos de AWS KMS](./aws/configure-kms.md). Para implementaciones de Azure, consulte la [Guía de configuración de Azure Key Vault](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Para [!DNL Azure] instancias de Platform alojadas, los datos de perfil de cliente almacenados en Platform [!DNL Azure Data Lake] y el almacén de perfiles [!DNL Azure Cosmos DB] se cifran exclusivamente mediante CMK una vez habilitado. La revocación de claves en los almacenes de datos principales puede tardar entre **unos minutos y 24 horas**, y entre **hasta 7 días** para los almacenes de datos transitorios o secundarios. Para obtener más información, consulte las [implicaciones de revocar el acceso a claves en la sección](#revoke-access).

Este documento proporciona información general de alto nivel sobre el proceso para habilitar la función Claves administradas por el cliente (CMK) en Platform en [!DNL Azure] y AWS, junto con la información sobre los requisitos previos necesaria para completar estos pasos.

>[!NOTE]
>
>Para los clientes de Customer Journey Analytics, siga las instrucciones que se encuentran en [documentación de Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=es).

## Requisitos previos

Para habilitar CMK, el entorno de alojamiento de su plataforma ([!DNL Azure] o AWS) debe cumplir con los requisitos de configuración específicos:

### Requisitos previos generales

Para ver y obtener acceso a la sección [!UICONTROL Cifrado] en Adobe Experience Platform, debe haber creado una función y asignado el permiso [!UICONTROL Administrar clave administrada por el cliente] a esa función.  Cualquier usuario con el permiso [!UICONTROL Administrar clave administrada por el cliente] puede habilitar CMK para su organización.

Para obtener más información sobre la asignación de funciones y permisos en Experience Platform, consulte la [documentación sobre la configuración de permisos](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Requisitos previos específicos de Azure

Para implementaciones alojadas en Azure, configure el almacén de claves [!DNL Azure] con la siguiente configuración:

- [Habilitar protección contra purgas](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Habilitar eliminación suave](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Configurar el acceso mediante [!DNL Azure] control de acceso basado en roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### Requisitos previos específicos de AWS

En implementaciones alojadas en AWS, configure su entorno de AWS de la siguiente manera:

- Asegúrese de que tiene permisos para administrar claves de cifrado mediante AWS Identity and Access Management (IAM). Para obtener más información, consulte las [directivas de IAM para AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Configure AWS KMS compatible con CMK. Consulte la [Guía de cifrado de datos de AWS KMS](./aws/configure-kms.md).

## Resumen del proceso {#process-summary}

Claves gestionadas por el cliente (CMK) está disponible a través de las ofertas Escudo de atención sanitaria y Escudo de privacidad y seguridad de Adobe. En Azure, CMK es compatible tanto con Healthcare Shield como con Privacy and Security Shield. En AWS, CMK solo es compatible con el Escudo de privacidad y seguridad, y no está disponible para Healthcare Shield. Una vez que su organización compre una licencia para una de estas ofertas, puede iniciar el proceso de configuración único para habilitar CMK.

>[!WARNING]
>
>Después de configurar CMK, no puede volver a las claves administradas por el sistema. Usted es responsable de administrar de forma segura sus claves para evitar la pérdida de acceso a sus datos.

El proceso es el siguiente:

### Para Azure {#azure-process-summary}

1. [Configura un [!DNL Azure] depósito de claves](./azure/azure-key-vault-config.md) basado en las políticas de tu organización y [genera una clave de cifrado](./azure/azure-key-vault-config.md#generate-a-key) para compartirla con el Adobe.
1. Configure la aplicación CMK con su inquilino de [!DNL Azure] a través de [llamadas API](./azure/api-set-up.md#register-app) o la [IU](./azure/ui-set-up.md#register-app).
1. Envíe su ID de clave de cifrado al Adobe e inicie el proceso de habilitación de la función, ya sea [en la interfaz de usuario](./azure/ui-set-up.md#send-to-adobe) o con una [llamada API](./azure/api-set-up.md#send-to-adobe).
1. Compruebe el estado de la configuración para comprobar si CMK se ha habilitado, ya sea [en la interfaz de usuario](./azure/ui-set-up.md#check-status) o con una [llamada API](./azure/api-set-up.md#check-status).

Una vez completado el proceso de configuración de las instancias de Platform alojadas en Azure, todos los datos incorporados en Platform en todas las zonas protegidas se cifrarán con la configuración de clave de [!DNL Azure]. Para usar CMK, aprovechará la funcionalidad [!DNL Microsoft Azure] que puede formar parte de su [programa de vista previa pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

### Para AWS {#aws-process-summary}

1. [Configure AWS KMS](./aws/configure-kms.md) configurando una clave de cifrado para compartirla con el Adobe.
2. Siga las instrucciones específicas de AWS en la [guía de configuración de la interfaz de usuario](./aws/ui-set-up.md).
3. Valide la configuración para confirmar que los datos de Platform se cifran con la clave alojada en AWS.

<!--  Pending: or [API setup guide]() -->

Una vez completado el proceso de configuración de las instancias de Platform alojadas en AWS, todos los datos incorporados en Platform en todas las zonas protegidas se cifrarán con la configuración del servicio de administración de claves (KMS) de AWS. Para utilizar CMK en AWS, utilizará el Servicio de administración de claves de AWS para crear y administrar las claves de cifrado de acuerdo con los requisitos de seguridad de su organización.

## Implicaciones de revocar el acceso a claves {#revoke-access}

Revocar o deshabilitar el acceso a la aplicación Key Vault, key o CMK en Azure o a la clave de cifrado en AWS puede provocar interrupciones significativas, que incluyen cambios importantes en las operaciones de la plataforma. Una vez deshabilitadas las claves, es posible que no se pueda acceder a los datos en Platform y que las operaciones de flujo descendente que dependan de estos datos dejen de funcionar. Es crucial comprender completamente los impactos descendentes antes de realizar cambios en las configuraciones clave.

Para revocar el acceso de plataforma a sus datos en [!DNL Azure], quite el rol de usuario asociado a la aplicación de Key Vault. Para AWS, puede deshabilitar la clave o actualizar la instrucción de directiva. Para obtener instrucciones detalladas sobre el proceso de AWS, consulte la [sección de revocación de claves](./aws/ui-set-up.md#key-revocation).


### Escalas de tiempo de propagación {#propagation-timelines}

Una vez revocado el acceso a la clave desde el almacén de claves [!DNL Azure], los cambios se propagarán de la siguiente manera:

| **Tipo de tienda** | **Descripción** | **Cronología** |
|---|---|---|
| Almacenes de datos principales | Incluye lagos de datos (Azure Data Lake, AWS S3) y tiendas de perfil de Azure Cosmos DB. Una vez revocado el acceso a las claves, los datos se vuelven inaccesibles. | Entre **pocos minutos y 24 horas**. |
| Almacenes de datos en caché/transitorios | Incluye almacenes de datos secundarios utilizados para el rendimiento y la funcionalidad principal de la aplicación. El impacto de la revocación de claves se retrasa. | **Hasta 7 días**. |

Por ejemplo, el panel Perfil seguirá mostrando los datos de su caché durante un máximo de siete días antes de que los datos caduquen y se actualicen. Del mismo modo, volver a habilitar el acceso a la aplicación tarda la misma cantidad de tiempo en restaurar la disponibilidad de los datos en estas tiendas.

>[!NOTE]
>
>Volver a habilitar el acceso a la aplicación puede llevar la misma cantidad de tiempo que la revocación para restaurar la disponibilidad de los datos en estas tiendas.

>[!TIP]
>
>Existen dos excepciones específicas de casos de uso a la caducidad de conjuntos de datos de siete días en datos no principales (almacenados en caché/transitorios). Consulte su documentación correspondiente para obtener más información sobre estas funciones.<ul><li>[Abreviador de URL de Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=es#message-preset-sms)</li><li>[Proyecciones de Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Pasos siguientes

Para iniciar el proceso:

- Para Azure: Comience por [configurar una [!DNL Azure] caja fuerte de claves](./azure/azure-key-vault-config.md) y [generar una clave de cifrado](./azure/azure-key-vault-config.md#generate-a-key) para compartirla con el Adobe.
- Para AWS: [Configure AWS KMS](./aws/configure-kms.md) y asegúrese de que las configuraciones de IAM y KMS sean las correctas antes de seguir las guías de configuración de la interfaz de usuario o la API.
