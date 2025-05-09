---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Aplicaciones de Privacy Service y Experience Cloud
description: Este documento proporciona una referencia sobre cómo configurar diferentes aplicaciones de Experience Cloud para operaciones relacionadas con la privacidad.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 10%

---

# [!DNL Privacy Service] y [!DNL Experience Cloud] aplicaciones

Adobe Experience Platform [!DNL Privacy Service] se ha creado para admitir solicitudes de privacidad para varias aplicaciones de Adobe Experience Cloud. Cada aplicación admite distintos valores e ID de productos para identificar a los interesados.

Este documento sirve como referencia para la documentación de la aplicación [!DNL Experience Cloud] que describe cómo configurar esa aplicación para operaciones relacionadas con la privacidad. Esto incluye cómo dar formato y etiquetar los datos. Se cubren dos categorías de aplicaciones:

* [Aplicaciones integradas con Privacy Service](#integrated): Aplicaciones que pueden enviar solicitudes de acceso, eliminación o exclusión a [!DNL Privacy Service].
* [Aplicaciones de autoservicio](#self-serve): Aplicaciones que deben administrar sus solicitudes de privacidad internamente y no pueden comunicarse con [!DNL Privacy Service] directamente.

Consulte la documentación de las aplicaciones de [!DNL Experience Cloud] para obtener información sobre cómo dar formato a las solicitudes de privacidad y los valores que se admiten en dichas solicitudes.

## Aplicaciones integradas con [!DNL Privacy Service] {#integrated}

A continuación se muestra una lista de [!DNL Experience Cloud] aplicaciones integradas con [!DNL Privacy Service], incluidas las capacidades de [!DNL Privacy Service] con las que son compatibles, sus protocolos para procesar solicitudes de eliminación y los vínculos a la documentación para obtener más información.

>[!NOTE]
>
>Todos los productos integrados responden a las solicitudes de privacidad en 30 días o menos.

| Aplicación | Acceso o eliminación | Exclusión de la venta | Eliminar comportamiento | Documentación y otras consideraciones |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | La ID de cookie del interesado o la ID de dispositivo se eliminan del sistema, junto con todos los datos de costes, clics e ingresos asociados con la cookie. | <ul><li>[Acceder o eliminar la documentación de RGPD](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html?lang=es)</li><li>[Acceder o eliminar la documentación de la CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html?lang=es)</li><li>[Documentación de exclusión de la venta para CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html?lang=es)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics proporciona herramientas para etiquetar datos según su confidencialidad y las restricciones contractuales. Las etiquetas son un paso importante para lo siguiente:<ol><li>Identificación de sujetos de datos.</li><li>Determinar qué datos se devuelven como parte de una solicitud de acceso.</li><li>Identificación de campos de datos que deben eliminarse como parte de una solicitud de eliminación.</li></ol> | <ul><li>[Flujo de trabajo de privacidad](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html?lang=es)</li><li>[Etiquetado de Analytics](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html?lang=es)</li><li>[Exclusión de Analytics](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html?lang=es)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Se eliminan todos los rasgos y segmentos asociados con el identificador de Audience Manager incluido en la solicitud. Además, los identificadores respectivos de la persona se excluyen de cualquier recopilación de datos adicional y se eliminan las asignaciones de ID correspondientes. | <ul><li>Documentación de [acceso](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=es#access-data) / [eliminación](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=es#delete-data)</li><li>[Documentación de exclusión](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html?lang=es#opt-out-calls)</li><li>[Solicitudes de exclusión](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html?lang=es#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Administración de la privacidad](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=es)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Acceder o eliminar documentación](https://experienceleague.adobe.com/es/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[Documentación de exclusión](https://experienceleague.adobe.com/es/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Atributos del cliente de Adobe (CRS) | ✓ | N/A | Los atributos del interesado se eliminan del sistema. | <ul><li>[Acceder o eliminar la documentación de RGPD](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=es)</li><li>[Acceder o eliminar la documentación de la CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=es)</li><li>Los atributos del cliente no tienen la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Cuando Experience Platform recibe una solicitud de eliminación de Privacy Service, Experience Platform envía una confirmación a Privacy Service de que la solicitud se ha recibido y de que los datos afectados se han marcado para su eliminación. A continuación, los registros se eliminan del repositorio de datos o del almacén de perfiles una vez que se ha completado el trabajo de privacidad. Antes de que se complete el trabajo, los datos se eliminan de forma suave y, por lo tanto, ningún servicio de Experience Platform puede acceder a ellos. | <ul><li>[Acceder o eliminar la documentación del lago de datos](../catalog/privacy.md)</li><li>[Acceder o eliminar la documentación del servicio de identidad](../identity-service/privacy.md)</li><li>[Acceder o eliminar la documentación de Real-Time Customer Profile](../profile/privacy.md)</li><li>[!DNL Experience Platform] acepta [solicitudes de exclusión para segmentos de audiencia](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/A | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Acceder o eliminar documentación](https://experienceleague.adobe.com/es/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass Authentication | ✓ | N/A | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Acceder o eliminar documentación](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass no tiene la capacidad de transferir datos, por lo tanto las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Adobe Target | ✓ | N/A | Todos los datos asociados con el ID del interesado se eliminan de su perfil del visitante. Los datos agregados o anonimizados que no identifican a la persona o que no están relacionados (como los datos de contenido) no se aplican a las solicitudes de eliminación. | <ul><li>[Acceder o eliminar documentación](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=es)</li><li>[!DNL Target] no tiene la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |
| Commerce (Personalization) | ✓ | N/A | Privacy Service elimina los datos de [!DNL Commerce] almacenados en los servicios SaaS de Commerce con fines de marketing, lo que significa que los perfiles y pedidos de los interesados ya no se envían a las aplicaciones de marketing de Adobe para su uso en campañas y recorridos de clientes. Sin embargo, Privacy Service no elimina datos en la aplicación [!DNL Commerce], ya que podrían ser necesarios para las necesidades transaccionales de los comerciantes. Los comerciantes son responsables de cualquier solicitud de eliminación/acceso de datos en la aplicación [!DNL Commerce]. | <ul><li>[Acceder o eliminar la documentación de Commerce](https://experienceleague.adobe.com/es/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/A | Los datos almacenados del interesado se eliminan del sistema. | <ul><li>[Acceder o eliminar documentación](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html?lang=es)</li><li>[!DNL Marketo] no tiene la capacidad de transferir datos, por lo que las solicitudes de exclusión de la venta no son aplicables.</li></ul> |

{style="table-layout:auto"}

## Aplicaciones de autoservicio {#self-serve}

La siguiente es una lista de [!DNL Experience Cloud] aplicaciones que no están integradas con [!DNL Privacy Service] y deben administrar internamente sus problemas de privacidad. Se proporcionan vínculos a la documentación de cada aplicación, junto con descripciones del contenido de la documentación.

| Aplicación | Descripción de documentación |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html?lang=es) | Una visión general de cómo un administrador de privacidad del cliente o un administrador de AEM puede gestionar las solicitudes de RGPD. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html?lang=es) | Pasos para realizar solicitudes de acceso y eliminación de RGPD utilizando Livefyre. |
| [Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-operations/security-and-compliance/overview) | Asegúrese de que las instalaciones de Adobe Commerce cumplan con los requisitos de las legislaciones de privacidad específicas. |
| [Etiquetas en Adobe Experience Platform](../tags/ui/client-side/consent.md) | Cómo los desarrolladores pueden usar las extensiones y el creador de reglas para definir las soluciones de inclusión y de exclusión. |
| [Workfront](https://www.workfront.com/privacy-notice) | Descubra cómo Workfront recopila datos personales y cómo un interesado puede enviar una solicitud de privacidad mediante un formulario. |

{style="table-layout:auto"}
