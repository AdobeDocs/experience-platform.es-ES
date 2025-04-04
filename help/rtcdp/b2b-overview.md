---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;plataforma de datos del cliente en tiempo real;cdp en tiempo real;b2b;cdp;inteligencia artificial aplicada al cliente
title: Información general sobre Real-Time CDP B2B edition
description: Descripción general de la cuenta de Real-time Customer Data Platform B2B Edition
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 4%

---

# Información general sobre Real-Time Customer Data Platform B2B edition

Real-Time CDP B2B edition, que se creó en Adobe Real-Time Customer Data Platform (Real-Time CDP), está diseñado específicamente para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse a públicos específicos con precisión y captarlos en todos los canales disponibles.

Se han realizado mejoras en una variedad de funciones de Adobe Experience Platform que distinguen a Real-Time CDP B2B edition de su homólogo B2C. Incluyen mejoras en el Experience Data Model (XDM) para casos de uso B2B, actualizaciones en la resolución de identidades y segmentación de perfiles, así como un conector y un destino creados a medida para [!DNL Marketo Engage]. El conector [!DNL Marketo] permite a las marcas B2B conectar sus datos de participación B2B líderes del sector con información de comportamiento para fomentar posibles clientes y mejorar las operaciones de marketing basadas en cuentas.

Con Real-Time CDP B2B edition, puede:

* Combine los datos recopilados de varias fuentes en una sola vista para crear personas y perfiles de cuenta integrales.
* Enriquezca, segmente y exporte todos sus datos de fuentes cruzadas desde un almacén centralizado de perfiles de cuenta unificados.
* Administre sus datos con las herramientas de control de datos disponibles en cada paso del proceso de centralización para garantizar que los datos se ajusten a las regulaciones legales y a las políticas empresariales.

Los detalles más completos sobre las mejoras realizadas para Real-Time CDP B2B edition se dividen en secciones a continuación.

## XDM

Real-Time CDP B2B edition proporciona varias clases de esquema XDM, grupos de campos y tipos de relación nuevos para capturar y estructurar los datos específicamente para fines B2B. Consulte la descripción general del [XDM en Real-Time CDP B2B edition](./schemas/b2b.md) para ver un desglose de cada una de estas mejoras.

Mediante esquemas B2B preconfigurados, puede introducir datos en una estructura estandarizada y procesable. Muchas de las nuevas clases de esquema se asignan casi directamente a las que se encuentran en los CRM principales, como [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] y otras fuentes de datos B2B. Con Real-Time CDP B2B edition, puede introducir datos de fuentes B2B en Experience Platform de forma directa y con resultados fáciles de auditar.

Estas mejoras de XDM permiten una mejor ingesta y activación de datos a través de fuentes y destinos centrados en B2B, lo que mejora la unificación y presentación de datos para casos de uso más diversos y flexibles.

## Resolución de identidad

Después de definir los esquemas y de introducir los datos según esos esquemas, Real-Time CDP B2B edition identifica los registros de origen que representan a personas y empresas del mundo real mediante un sistema potente y en tiempo real de resolución de identidades.

El sistema de resolución de identidades proporciona las siguientes funciones:

* Registros de personas B2B y B2C combinados
* Una jerarquía de cuentas de varios niveles
* Conexiones &quot;varios a varios&quot; y &quot;personas a cuenta&quot;
* Las identidades de personas y cuentas se resuelven en tiempo real

El sistema de resolución de identidades se ha ampliado para apoyar una clasificación más polifacética de las personas. El sistema permite identificar a las personas como líderes en oportunidades de negocio, así como clientes.

Experience Platform combina los registros de cuenta sincronizados por el CRM de origen y conectados a través de varias rutas dentro del sistema. El sistema reúne a las personas asociadas con oportunidades de negocio y a las registradas como clientes, pero también es capaz de preservar la distinción entre ellas como un atributo si son identificables.

Los identificadores coincidentes se utilizan para vincular y combinar registros de cuenta de varios sistemas. Las jerarquías de cuentas se conservan durante todo este proceso. Los diferenciadores se utilizan para examinar si una persona está asociada a una cuenta o no y proporcionar la capacidad de separarla de la cuenta si es necesario.

## Perfiles y segmentación

Una vez que Real-Time CDP B2B edition ha introducido datos y resuelto identidades relacionadas con personas, empresas, atributos y comportamientos, esos datos se utilizan para construir perfiles. Estos perfiles se pueden segmentar en audiencias explorables que luego se pueden activar en varios destinos.

Cuando se implementa correctamente, el sistema rastrea a las personas mediante identificadores principales únicos en lugar de atributos que pueden cambiar, como las direcciones de correo electrónico. Esto significa que cuando alguien cambia de trabajo, el sistema los sigue. La persona sigue siendo la misma entidad, pero en su lugar está vinculada a una nueva cuenta. Esta funcionalidad nativa ofrece un gran vector para la expansión en nuevas cuentas a medida que el sistema sigue a estas personas como individuos incluyendo todos sus atributos y comportamientos.

## Fuentes B2B

Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. El origen [!DNL Marketo] le permite transmitir datos B2B a Experience Platform y mantenerlos actualizados mediante aplicaciones conectadas a Experience Platform. Admite cualquier número de instancias de [!DNL Marketo] (lo que resulta beneficioso para grandes empresas con varias instancias) y extrae una sola organización en la que se combinan los datos.

>[!NOTE]
>
>El origen [!DNL Marketo] es **no** necesario para usar Real-Time CDP B2B edition.

Consulte las [fuentes en la documentación de Real-Time CDP B2B edition](./sources/b2b.md) para obtener más información sobre Marketo y la introducción de datos B2B en Experience Platform.

## Destinos B2B

Real-Time CDP B2B edition ofrece y admite destinos de Experience Platform como Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads y Google Ad Manager. El destino de Marketo Engage también transmite los datos de abono a segmentos desde Experience Platform y lo pone a disposición como listas en Marketo.

Consulte la descripción general del [Destino de Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) para obtener más información.

Para las empresas con más de un CRM, Real-Time CDP B2B edition proporciona la opción de configurar conectores de destino para instancias independientes de Marketo o CRM. Si es necesario, puede configurar los conectores de destino para cada instancia y enviar audiencias a cada una de las instancias de CRM de forma independiente.

## Pasos siguientes

Ahora que comprende mejor las ventajas que ofrece Real-Time CDP B2B edition para los especialistas en marketing y las diferencias entre esta aplicación y Real-Time CDP, puede aprender a aplicar estas funciones a su propia organización.

Para comprender cómo Real-Time CDP B2B edition puede beneficiar a su modelo de servicio empresa a empresa, consulte la siguiente documentación para ayudarle a empezar:

* [Ejemplo de caso de uso para Real-Time CDP B2B edition](./b2b-use-case.md)
* [Un tutorial completo para Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
* [Ingesta de datos](./sources/b2b.md)
* [Cómo acceder a los perfiles](./profile/profile-overview.md)
* [Esquemas en Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
* [Cómo crear audiencias](./segmentation/b2b.md)
* [Activación de audiencias en destinos](./destinations/b2b.md)
* [Definición y aplicación de políticas de gobernanza de datos](./privacy/data-governance-overview.md)
