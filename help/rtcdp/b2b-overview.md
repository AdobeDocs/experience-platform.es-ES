---
keywords: RTCDP;CDP;B2B Edition;Plataforma de datos del cliente en tiempo real;plataforma de datos del cliente en tiempo real;cdp en tiempo real;b2b;cdp;Customer AI
title: Información general de CDP B2B Edition en tiempo real
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Descripción general de la cuenta de la plataforma de datos del cliente en tiempo real B2B Edition
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: e54bd747a332e37920e24ce07602470f8ad74231
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 1%

---

# Información general sobre la plataforma de datos del cliente en tiempo real B2B Edition

>[!IMPORTANT]
>
>CDP B2B Edition en tiempo real está actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

El CDP B2B Edition en tiempo real, que se basa en la plataforma de datos del cliente en tiempo real (CDP en tiempo real), está diseñado para los especialistas en marketing que operan en un modelo de servicio de empresa a empresa. Agrupa datos de varias fuentes y los combina en una sola vista de personas y perfiles de cuenta. Estos datos unificados permiten a los especialistas en marketing dirigirse con precisión a audiencias específicas e interactuar con ellas en todos los canales disponibles.

Hay mejoras en una variedad de funcionalidades de Adobe Experience Platform que distinguen CDP B2B Edition en tiempo real de su contraparte B2C. Incluyen mejoras en el Modelo de datos de experiencia (XDM) para casos de uso B2B, actualizaciones para la resolución de identidades y la segmentación de perfiles, así como un conector y destino personalizado para [!DNL Marketo Engage]. El conector [!DNL Marketo] permite que las marcas B2B conecten sus datos de participación B2B líderes en el sector con información de comportamiento para nutrir posibles clientes y mejorar las operaciones de marketing basadas en cuentas.

Con CDP B2B Edition en tiempo real, puede:

* Combine los datos recopilados de varias fuentes en una sola vista para crear personas y perfiles de cuenta holísticos.
* Enriquezca, segmente y exporte todos sus datos de fuentes cruzadas desde un almacén centralizado de perfiles de cuenta unificados.
* Administre sus datos con herramientas de control de datos disponibles en cada paso del proceso de centralización para garantizar que sus datos se ajusten a las normativas legales y a las políticas del negocio.

Los detalles más completos sobre las mejoras realizadas para CDP B2B Edition en tiempo real se dividen en secciones a continuación.

## XDM

CDP B2B Edition en tiempo real proporciona varias nuevas clases de esquema XDM, grupos de campos y tipos de relación para capturar y estructurar sus datos específicamente para propósitos B2B. Consulte la descripción general de [XDM en la edición B2B de CDP en tiempo real](./schemas/b2b.md) para obtener un desglose de cada una de estas mejoras.

Mediante esquemas B2B preconfigurados, puede incorporar datos en una estructura estandarizada y procesable. Muchas de las nuevas clases de esquema se asignan casi directamente a las que se encuentran en los CRM principales, como [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] y otras fuentes de datos B2B. Con CDP B2B Edition en tiempo real, puede incorporar datos de fuentes B2B a Platform de manera directa y con resultados que sean fáciles de auditar.

Estas mejoras de XDM le permiten ingerir y activar mejor los datos a través de fuentes y destinos centrados en B2B, lo que mejora la unificación y presentación de datos para casos de uso más diversos y flexibles.

## Resolución de identidad

Después de definir los esquemas y de incorporar los datos de acuerdo con esos esquemas, CDP B2B Edition en tiempo real identifica los registros de origen que representan a personas y empresas del mundo real a través de un poderoso sistema de resolución de identidades en tiempo real.

El sistema de resolución de identidades ofrece las siguientes características:

* Registros combinados de personas B2B y B2C
* Una jerarquía de cuentas de varios niveles
* Conexiones &quot;varios a varios&quot;, entre personas y cuentas
* Las identidades de personas y cuentas se resuelven en tiempo real

El sistema de resolución de identidades se ha ampliado para apoyar una clasificación de personas más polifacética. El sistema permite identificar a las personas como posibles clientes en oportunidades comerciales, así como a clientes.

Platform fusiona los registros de cuenta sincronizados por el CRM de origen y conectados mediante varias rutas dentro del sistema. El sistema reúne a las personas asociadas con oportunidades comerciales y a las registradas como clientes, pero también puede preservar la distinción entre ellas como atributo si son identificables.

Los identificadores coincidentes se utilizan para vincular y combinar registros de cuenta de varios sistemas. Las jerarquías de cuentas se conservan a lo largo de este proceso. Los diferenciadores se utilizan para comprobar si una persona está asociada a una cuenta o no, y para proporcionar la capacidad de separarla de la cuenta si es necesario.

## Perfiles y segmentación

Una vez que CDP B2B Edition en tiempo real ha introducido datos y resuelto identidades relacionadas con personas, empresas, atributos y comportamientos, esos datos se utilizan para construir perfiles. Estos perfiles se pueden segmentar en audiencias explorables que luego se pueden activar en varios destinos.

Cuando se implementa correctamente, el sistema realiza el seguimiento de las personas que utilizan identificadores principales únicos en lugar de atributos que pueden cambiar, como las direcciones de correo electrónico. Esto significa que cuando alguien cambia de trabajo, el sistema sigue su ejemplo. La persona sigue siendo la misma entidad, pero en su lugar están vinculadas a una nueva cuenta. Esta funcionalidad nativa ofrece un bueno vector para la expansión a nuevas cuentas, ya que el sistema sigue a estas personas como individuos, incluidos todos sus atributos y comportamientos.

## Fuentes B2B

Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. La fuente [!DNL Marketo] permite transmitir datos B2B a Platform y mantener estos datos actualizados mediante aplicaciones conectadas a la plataforma. Admite cualquier número de instancias de [!DNL Marketo] (lo que resulta beneficioso para grandes empresas con varias instancias) y se incorpora a una única organización de IMS en la que se combinan los datos.

>[!NOTE]
>
>La fuente [!DNL Marketo] es **no** necesaria para utilizar CDP B2B Edition en tiempo real.

Consulte las fuentes en la documentación de CDP B2B Edition en tiempo real para obtener más información sobre Marketo y la introducción de datos B2B en Platform.

<!-- PLACEHOLDER [sources in Real-time CDP B2B Edition](./sources/b2b) -->

## Destinos B2B

Todos los destinos de Experience Platform como [!DNL Google], [!DNL Linkedin] o [!DNL Facebook] están disponibles y son totalmente compatibles con CDP B2B Edition en tiempo real. También hay un destino [!DNL Marketo Engage] que transmite datos desde [!DNL Marketo] o desde Platform y lo hace disponible como audiencias.

El destino [!DNL Marketo] proporciona una manera rápida y sencilla de extraer información del Experience Platform a [!DNL Marketo]. El destino permite a los especialistas en marketing insertar segmentos creados en Adobe Experience Platform en [!DNL Marketo]. En [!DNL Marketo], estas audiencias están disponibles como listas estáticas.

Para empresas con más de un CRM, CDP B2B Edition en tiempo real proporciona la opción de configurar conectores de destino para separar instancias de [!DNL Marketo] o CRM. Si es necesario, puede configurar los conectores de destino para cada instancia y enviar audiencias a cada una de las instancias de CRM de forma independiente.

## Pasos siguientes

Ahora que comprende mejor los beneficios para los especialistas en marketing que ofrece CDP B2B Edition en tiempo real, y las diferencias entre ella y CDP en tiempo real, puede aprender a aplicar estas funciones a su propia organización IMS.

<!-- PLACEHOLDER [example use case for Real-time CDP B2B Edition]() -->

Para comprender cómo CDP B2B Edition en tiempo real puede beneficiar a su modelo de servicio de empresa a empresa, consulte el ejemplo de uso para CDP B2B Edition en tiempo real. También puede consultar la documentación de [esquemas en la plataforma de datos del cliente en tiempo real B2B Edition](./schemas/b2b.md) para obtener instrucciones más específicas sobre la creación de esquemas y la definición de relaciones para entidades de datos B2B esenciales.
