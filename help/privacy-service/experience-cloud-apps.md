---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Aplicaciones Privacy Service y Experience Cloud
description: Este documento proporciona una referencia sobre cómo configurar distintas aplicaciones de Experience Cloud para operaciones relacionadas con la privacidad.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 16985d285cf181547f3692c5ed1910eebe8df210
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 12%

---

# [!DNL Privacy Service] y [!DNL Experience Cloud] aplicaciones

Adobe Experience Platform [!DNL Privacy Service] está diseñada para admitir solicitudes de privacidad de varias aplicaciones de Adobe Experience Cloud. Cada aplicación admite diferentes valores de producto e ID para identificar interesados.

Este documento sirve como referencia para [!DNL Experience Cloud] documentación de la aplicación que describe cómo configurar esa aplicación para operaciones relacionadas con la privacidad. Esto incluye cómo dar formato y etiquetar los datos. Se tratan dos categorías de solicitudes:

* [Aplicaciones integradas con el Privacy Service](#integrated): Aplicaciones que pueden enviar solicitudes de acceso, eliminación o exclusión a [!DNL Privacy Service].
* [Aplicaciones de autoservicio](#self-serve): Aplicaciones que deben administrar sus solicitudes de privacidad internamente y que no pueden comunicarse con [!DNL Privacy Service] directamente.

Revise la documentación de su [!DNL Experience Cloud] para aprender a dar formato a sus solicitudes de privacidad y qué valores se admiten para dichas solicitudes.

## Aplicaciones integradas con [!DNL Privacy Service] {#integrated}

La siguiente es una lista de [!DNL Experience Cloud] aplicaciones integradas con [!DNL Privacy Service], incluido el [!DNL Privacy Service] funcionalidades con las que son compatibles, sus protocolos para procesar solicitudes de eliminación y vínculos a documentación para obtener más información.

>[!NOTE]
>
>Todos los productos integrados responden a solicitudes de privacidad en 30 días o menos.

| Aplicación | Acceso/eliminación | Exclusión de la venta | Eliminar comportamiento | Documentación y otras consideraciones |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | El ID de cookie o el ID de dispositivo del interesado se eliminan del sistema junto con todos los datos de costes, clics e ingresos asociados a la cookie. | <ul><li>[Documentación de acceso/eliminación para el RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Documentación de acceso/eliminación para la CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Documentación de exclusión de la venta para la CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics proporciona herramientas para etiquetar datos según su confidencialidad y las restricciones contractuales. Las etiquetas son un paso importante para:<ol><li>Identificación de sujetos de datos.</li><li>Determinación de qué datos devolver como parte de una solicitud de acceso.</li><li>Identificación de campos de datos que deben eliminarse como parte de una solicitud de eliminación.</li></ol> | <ul><li>[Flujo de trabajo de privacidad](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Etiquetado de Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Exclusión de Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Se eliminan todos los rasgos y segmentos asociados al identificador de Audience Manager incluido en la solicitud. Además, los identificadores respectivos para el individuo se excluyen de una recopilación de datos adicional y se eliminan las asignaciones de ID correspondientes. | <ul><li>[Documentación de acceso/eliminación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Documentación de exclusión](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Documentación de acceso/eliminación](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=es)</li><li>[Documentación de exclusión](../segmentation/consents.md)</li></ul> |
| Atributos del cliente de Adobe (CRS) | ✓ | N/A | Los atributos del interesado se eliminan del sistema. | <ul><li>[Documentación de acceso/eliminación para el RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=es)</li><li>[Documentación de acceso/eliminación para la CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=es)</li><li>Los atributos del cliente no tienen la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Cuando el Experience Platform recibe una solicitud de eliminación del Privacy Service, Platform envía una confirmación al Privacy Service de que la solicitud se ha recibido y que los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del lago de datos o del almacén de perfiles una vez que se haya completado el trabajo de privacidad. Antes de que finalice el trabajo, los datos se eliminan de forma flexible y, por lo tanto, ningún servicio de Platform puede acceder a ellos. | <ul><li>[Documentación de acceso/eliminación para el lago de datos](../catalog/privacy.md)</li><li>[Documentación de acceso o eliminación para el servicio de identidad](../identity-service/privacy.md)</li><li>[Documentación de acceso/eliminación para el perfil del cliente en tiempo real](../profile/privacy.md)</li><li>[!DNL Experience Platform] honores [solicitudes de exclusión para segmentos de audiencia](../segmentation/consents.md).</li></ul> |
| Autenticación de Adobe Primetime | ✓ | N/A | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Documentación de acceso/eliminación](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] no tiene la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Adobe Target | ✓ | N/A | Todos los datos asociados con el ID del interesado se eliminan de su perfil del visitante. Los datos agregados o anonimizados que no identifican al individuo o que no están relacionados (como los datos de contenido) no se aplican a las solicitudes de eliminación. | <ul><li>[Documentación de acceso/eliminación](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=es)</li><li>[!DNL Target] no tiene la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Marketo Engage | ✓ | N/A | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Documentación de acceso/eliminación](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] no tiene la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |

{style="table-layout:auto"}

## Aplicaciones de autoservicio {#self-serve}

La siguiente es una lista de [!DNL Experience Cloud] aplicaciones que no están integradas con [!DNL Privacy Service] y deben administrar internamente sus preocupaciones de privacidad. Se proporcionan vínculos a la documentación de cada aplicación, junto con descripciones del contenido de la documentación.

| Aplicación | Descripción de la documentación |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=es) | Información general sobre las funcionalidades del RGPD para Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Información general sobre cómo un administrador de privacidad del cliente o AEM administrador puede gestionar las solicitudes de RGPD. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Pasos para realizar solicitudes de acceso y eliminación del RGPD mediante Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Asegúrese de que las instalaciones del Magento Commerce cumplan los requisitos de la legislación específica de privacidad. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Descubra cómo se aplican las normas de privacidad a Marketo. |
| [Etiquetas en Adobe Experience Platform](../tags/ui/client-side/consent.md) | Cómo los desarrolladores pueden usar las extensiones y el creador de reglas para definir las soluciones de inclusión y de exclusión. |
| [Workfront](https://www.workfront.com/privacy-notice) | Descubra cómo Workfront recopila datos personales y cómo un interesado puede enviar una solicitud de privacidad a través de un formulario. |

{style="table-layout:auto"}
