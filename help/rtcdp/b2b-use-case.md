---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Ejemplo de caso de uso para Real-time Customer Data Platform B2B Edition
description: Este escenario de muestra proporciona un ejemplo para la configuración de la implementación de Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Use Cases, B2B
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 2%

---

# Ejemplo de caso de uso para Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition amplía las ofertas existentes de Real-Time CDP y Adobe Experience Platform para admitir flujos de trabajo y datos B2B. Este documento proporciona un ejemplo de uso que demuestra las ventajas adicionales que ofrece B2B Edition. Entre ellos se incluyen:

- Combine datos de personas y cuentas de diferentes fuentes de datos en silo para producir una vista completa que permita una mejor comprensión de los clientes y una segmentación más precisa. Consulte la documentación sobre [creación de relaciones de esquema XDM](./schemas/b2b.md) para su uso con diversas fuentes B2B para obtener más información.
- Segmente una audiencia en función de los atributos de entidades relacionadas. Esto incluye cuentas, oportunidades, campañas y listas de marketing. Los segmentos ya no se limitan únicamente a atributos de persona y eventos de experiencia. Consulte la [Documentación de segmentación B2B](./segmentation/b2b.md) para ver más ejemplos de creación de audiencias específicas de B2B.
- Admitir de forma nativa el caso de uso de una persona relacionada con varias cuentas.

## Caso de uso

Bodea, una empresa tecnológica, tiene un nuevo producto y quiere dirigirse simultáneamente a los clientes con un correo electrónico y una campaña publicitaria de LinkedIn. Con el fin de maximizar la eficacia de su campaña de marketing, Bodea también quiere dirigirse a las personas asociadas con esa cuenta existente que han gastado más de un millón de dólares en sus productos anteriormente, Y que han visitado la nueva página de producto en el último mes.

Sin embargo, Bodea tiene dos líneas de negocio diferentes. La primera línea de negocio de Bodea &quot;Línea 1&quot; crea software para la industria automotriz. Su segunda línea de negocio &quot;Línea 2&quot; vende impresoras 3D que crean piezas de automóviles. Como resultado de las dos líneas de negocio de Bodea, los datos de ingresos generados a partir de las cuentas de cliente de Bodea no están unificados en una sola vista.

Cada línea de negocio tiene su propio sistema de ventas: &quot;CRM 1&quot; y &quot;CRM 2&quot;. Ambos sistemas de ventas CRM están conectados a su propia plataforma de automatización de marketing &quot;Marketo 1&quot; y &quot;Marketo 2&quot;. Los datos de CRM 1 solo se sincronizan con Marketo 1 y los datos de CRM2 solo se sincronizan con Marketo 2. En última instancia, sus datos se mantienen en diferentes silos de información corporativa.

## Situación de los datos actuales

Puesto que ambas líneas del negocio de Bodea venden a la empresa Townsend, los datos del negocio de Townsend se registran como dos cuentas independientes en cada sistema de ventas.

En Marketo 1, Townsend se registra como Cuenta 1. Tiene dos personas relacionadas (p1@townsend.com y p2@townsend.com) y una oportunidad ganada a puerta cerrada de 200 000 $ (&quot;Oportunidad 1&quot;) en CRM 1. Esos datos se sincronizan desde CRM 1 a Marketo 1.

En Marketo 2, Townsend se registra como Cuenta 2. La cuenta 2 también tiene dos personas relacionadas (p2@townsend.com y p3@townsend.com) y una oportunidad ganada a puerta cerrada de 900 000 $ (&quot;Oportunidad 2&quot;) en CRM 2. Esos datos se sincronizan desde CRM 2 a Marketo 2.

Para fines de integración y control corporativo adicional, Bodea también tiene un sistema de gestión de datos maestros (MDM) donde mantiene un registro que indica que la cuenta 1 en Marketo 1 (y CRM 1) y la cuenta 2 en Marketo 2 (y CRM 2) son la misma compañía.

En el último mes, `p2@townsend.com` visitó la nueva página de producto y la visita web fue registrada por Marketo 1.

![diagrama de información de cuenta](./assets/account-info.png)

## El problema

La línea 1 acaba de lanzar un nuevo producto de software y desea mejorar su venta a la actual base de clientes de alto nivel de Bodea. Bodea lanza una campaña de marketing con ese público objetivo en mente.

Dado que la información relevante de Townsend se registra como Cuenta 1 en Marketo 1 y Cuenta 2 en Marketo 2, el equipo de marketing de Bodea no puede utilizar de forma eficaz la información en silos.

Esto prohíbe al equipo de marketing de Bodea dirigir de manera eficiente los contactos comerciales específicos de estas empresas con esta nueva oportunidad.

Hasta la fecha, Townsend ha gastado más de un millón de dólares acumulados en productos de Bodea en todas sus cuentas. Sin embargo, un segmento creado con su sistema antiguo no incluiría a nadie de Townsend a menos que el total gastado dentro de un único sistema de ventas ascendiera a más de 1 millón de dólares. Esto se debe a que los datos de ingresos están en silos en cuentas bajo diferentes sistemas de ventas.

Dado que el gasto de Townsend se divide en diferentes sistemas de ventas y no suma individualmente más de un millón, el segmento no encontraría a nadie cualificado ni en Marketo 1 ni en Marketo 2.

### Solución del problema con Real-Time CDP B2B Edition

Con Real-Time CDP B2B Edition, el equipo de marketing de Bodea puede:

- Combine los datos de todos los orígenes diferentes (varias instancias de Marketo y CRM y la administración de datos maestros) en Real-Time CDP B2B Edition.

Con RT-CDP edición B2B, Bodea puede utilizar el conector de origen del Marketo Engage para introducir datos B2B de Marketo 1 y Marketo 2 en Experience Platform y mantener estos datos actualizados mediante aplicaciones conectadas a Platform. Consulte la [Conector de origen de Marketo](../sources/connectors/adobe-applications/marketo/marketo.md) para obtener más información.

Los datos B2B (Personas, Cuentas, Oportunidades y actividad ) de CRM1 se sincronizan con Marketo 1. Del mismo modo, todos los datos B2B de CRM 2 se sincronizan con Marketo 2. Se sincronizan con Adobe Experience Platform a través del conector de origen de Marketo. Sin embargo, si Bodea desea introducir datos adicionales de un CRM en Experience Platform, puede utilizar conectores de CRM existentes.

Por simplicidad y el propósito de este ejemplo, las personas están siendo identificadas por sus correos electrónicos. Los datos de cuentas combinadas para este ejemplo son los siguientes:

| Personas |
|---|
| p1@townsend.com |
| p2@townsend.com (que visitó la nueva página de producto el mes pasado) |
| p3@townsend.com |

| Oportunidades (ganadas de forma cerrada) |
|---|
| Oportunidad 1, 200.000 $ |
| Oportunidad 2, 900.000 $ |

- Cree segmentos únicos utilizando estos datos agregados para diversas iniciativas de marketing. En este ejemplo, el segmento encuentra todas las personas que:

   - Tener oportunidades asociadas (en TODAS las cuentas) que superen el valor de 1 millón de dólares
   - AND
   - Ha visitado la página de producto en el último mes

- Cree una audiencia que sea el destinatario más eficiente de la nueva campaña de marketing de Bodea. En este ejemplo, RT-CDP, edición B2B ayudará al experto en marketing a identificar `p2@townsend.com` como el destinatario correcto para esta campaña de marketing.

Bodea utiliza los destinos Marketo Engage y LinkedIn para ofrecer una solución integral de gestión de la experiencia del cliente (CXM) a su equipo de marketing. La audiencia creada en Experience Platform se inserta en el destino de Marketo donde aparece como una lista estática. A continuación, esta audiencia se añade automáticamente a una campaña de marketing de Marketo. Al mismo tiempo, la audiencia también puede enviarse a una campaña de marketing de LinkedIn mediante RT-CDP edición B2B.

## Pasos siguientes

Al leer este documento, se le han presentado los tipos de objetivos y problemas que se pueden resolver con Real-Time CDP B2B Edition.

Se recomienda la siguiente documentación para comprender mejor las funciones específicas de B2B:

- [Tutorial completo de Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
- [Fuentes en Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Esquemas en Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Ejemplos de segmentación B2B](./segmentation/b2b.md)
- [Resumen de perfiles de cuenta](./accounts/account-profile-overview.md)
- [Destinos en Real-time Customer Data Platform edición B2B](./destinations/b2b.md)
- [Configuración de un destino de audiencias coincidentes de LinkedIn](../destinations/catalog/social/linkedin.md)
