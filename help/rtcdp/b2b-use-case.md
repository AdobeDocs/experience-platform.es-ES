---
keywords: RTCDP;CDP;Real-time Customer Data Platform;plataforma de datos de clientes en tiempo real;cdp en tiempo real;cdp;rtcdp
title: Ejemplo de caso de uso para Real-time Customer Data Platform B2B Edition
description: Este escenario de ejemplo proporciona un ejemplo para la configuración de la implementación de Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Ejemplo de caso de uso para Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition amplía las ofertas existentes de Real-Time CDP y Adobe Experience Platform para admitir datos y flujos de trabajo B2B. Este documento proporciona un ejemplo de caso de uso que demuestra los beneficios adicionales proporcionados por B2B Edition. Entre ellos se incluyen:

- Combine datos de personas y cuentas de diferentes fuentes de datos aisladas para producir una vista completa que permita comprender mejor a los clientes y realizar una segmentación más precisa. Consulte la documentación sobre [creación de relaciones de esquema XDM](./schemas/b2b.md) para uso con fuentes B2B variadas para obtener más información.
- Segmentar una audiencia según los atributos de entidades relacionadas. Esto incluye cuentas, oportunidades, campañas y listas de marketing. Los segmentos ya no están limitados únicamente a los atributos de persona y a los eventos de experiencia. Consulte la [Documentación de segmentación B2B](./segmentation/b2b.md) para obtener más ejemplos de creación de audiencias específicas de B2B.
- Compatibilidad nativa con el caso de uso de una persona relacionada con varias cuentas.

## Caso de uso

Bodea, una empresa tecnológica, tiene un nuevo producto y quiere dirigirse simultáneamente a los clientes mediante un correo electrónico y una campaña publicitaria de LinkedIn. Para maximizar la eficacia de su campaña de marketing, Bodea también quiere dirigirse a las personas asociadas con esa cuenta existente que han gastado más de un millón de dólares en sus productos anteriormente, Y han visitado la nueva página de producto en el último mes.

Sin embargo, Bodea tiene dos líneas de negocios diferentes. La primera línea de negocio de Bodea, &quot;Línea 1&quot;, crea software para la industria automotriz. Su segunda línea de negocio &quot;Línea 2&quot; vende impresoras 3D que crean piezas de automóvil. Como resultado de las dos líneas de negocio de Bodea, los datos de ingresos generados a partir de las cuentas de cliente de Bodea no están unificados en una sola vista.

Cada línea de negocio tiene su propio sistema de ventas: &quot;CRM 1&quot; y &quot;CRM 2&quot;. Ambos sistemas de ventas CRM están conectados a su propia plataforma de automatización de marketing &quot;Marketo 1&quot; y &quot;Marketo 2&quot;. Los datos de CRM 1 solo se sincronizan con Marketo 1 y los datos de CRM2 solo se sincronizan con Marketo 2. En última instancia, sus datos se mantienen en diferentes silos de información corporativa.

## Situación de los datos actuales

Como ambas líneas de negocio de Bodea venden a la empresa Townsend, el Townsend datos de negocio se registra como dos cuentas separadas en cada sistema de ventas.

En Marketo 1, Townsend se registra como Cuenta 1. Tiene dos personas relacionadas (p1@townsend.com y p2@townsend.com) y una oportunidad cerrada ganada de $200 k (&quot;Oportunidad 1&quot;) en CRM 1. Esos datos se sincronizan de CRM 1 a Marketo 1.

En Marketo 2, Townsend se registra como Cuenta 2. La cuenta 2 también tiene dos personas relacionadas (p2@townsend.com y p3@townsend.com) y una oportunidad ganada de 900.000 dólares (&quot;Oportunidad 2&quot;) en CRM 2. Esos datos se sincronizan de CRM 2 a Marketo 2.

Para fines de integración y control corporativo adicional, Bodea también tiene un sistema de gestión de datos maestro (MDM) donde mantiene un registro que indica que la cuenta 1 en Marketo 1 (y CRM 1) y la cuenta 2 en Marketo 2 (y CRM 2) son la misma empresa.

En el último mes, `p2@townsend.com` visitaron la nueva página del producto y Marketo 1 registró la visita web.

![diagrama de información de la cuenta](./assets/account-info.png)

## El problema

La línea 1 acaba de lanzar un nuevo producto de software y le gustaría venderlo a la base de clientes de primer nivel de Bodea. Bodea inicia una campaña de marketing teniendo en cuenta esa audiencia objetivo específica.

Como la información relevante del Townsend se registra como Cuenta 1 en Marketo 1 y Cuenta 2 en Marketo 2, el equipo de marketing de Bodea no puede utilizar la información aislada de forma eficiente.

Esto impide que el equipo de marketing de Bodea pueda dirigirse de manera eficiente a contactos comerciales específicos de estas empresas con esta nueva oportunidad.

Hasta la fecha, Townsend ha gastado más de un millón de dólares acumulativamente en productos de Bodea en todas sus cuentas. Sin embargo, un segmento creado con su antiguo sistema no incluiría a nadie de Townsend a menos que el total gastado en un único sistema de ventas ascendiera a más de 1 millón de dólares. Esto se debe a que los datos de ingresos se bloquean en cuentas bajo diferentes sistemas de ventas.

Dado que el gasto de Townsend está dividido entre distintos sistemas de ventas y no llega a más de un millón de personas de forma individual, el segmento no encontraría a nadie cualificado ni en Marketo 1 ni en Marketo 2.

### Cómo resuelve el problema Real-Time CDP B2B Edition

Con Real-Time CDP B2B Edition, el equipo de marketing de Bodea puede:

- Combine los datos de todas las fuentes diferentes (varias instancias de Marketo y CRM y la administración maestra de datos) en Real-Time CDP B2B Edition.

Con RT-CDP B2B Edition, Bodea puede utilizar el conector de origen del Marketo Engage para llevar los datos B2B de Marketo 1 y Marketo 2 al Experience Platform y mantener estos datos actualizados mediante aplicaciones conectadas a la plataforma. Consulte la [Conector de origen de Marketo](../sources/connectors/adobe-applications/marketo/marketo.md) documentación para obtener más información.

Los datos B2B (Personas, Cuentas, Oportunidades y Actividad ) de CRM1 se sincronizan con Marketo 1. Del mismo modo, todos los datos B2B de CRM 2 se sincronizan con Marketo 2. Se sincronizan con Adobe Experience Platform mediante el conector de origen de Marketo. Sin embargo, si Bodea desea introducir datos adicionales de un CRM en un Experience Platform, puede utilizar los conectores CRM existentes.

Por el bien de la simplicidad y el propósito de este ejemplo, las personas están siendo identificadas por sus correos electrónicos. Los datos de cuenta combinados para este ejemplo tienen el siguiente aspecto:

| Personas |
|---|
| p1@townsend.com |
| p2@townsend.com (que visitó la nueva página de productos en el último mes) |
| p3@townsend.com |

| Oportunidades (cerradas) |
|---|
| Oportunidad 1, $200 k |
| Oportunidad 2, $900 k |

- Cree segmentos únicos usando estos datos agregados para diversas iniciativas de marketing. En este ejemplo, el segmento encuentra todas las personas que:

   - Tener oportunidades asociadas (en todas las cuentas de ALL) superiores a 1 millón de dólares en valor
   - AND
   - Han visitado la página del producto en el último mes

- Cree una audiencia que sean los destinatarios más eficientes de la nueva campaña de marketing de Bodea. En este ejemplo, RT-CDP, B2B Edition ayudarán al especialista en marketing a identificar `p2@townsend.com` como el objetivo correcto para esta campaña de marketing.

Al utilizar los destinos de Marketo Engage y LinkedIn, Bodea cuenta con una solución integral de gestión de la experiencia del cliente (CXM) para su equipo de marketing. La audiencia creada en el Experience Platform se envía al destino de Marketo, donde aparece como una lista estática. A continuación, esta audiencia se agrega automáticamente a una campaña de marketing de Marketo. Simultáneamente, la audiencia también puede enviarse a una campaña de marketing de LinkedIn mediante RT-CDP B2B Edition.

## Pasos siguientes

Al leer este documento, ahora se ha introducido el tipo de objetivos y problemas que se pueden resolver con Real-Time CDP B2B Edition.

Se recomienda la siguiente documentación para comprender mejor las funciones específicas de B2B:

- [Tutorial completo de Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
- [Fuentes en Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Esquemas en Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Ejemplos de segmentación B2B](./segmentation/b2b.md)
- [Información general sobre perfiles de cuenta](./accounts/account-profile-overview.md)
- [Destinos en Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [Configurar un destino de Audiencias coincidentes de LinkedIn](../destinations/catalog/social/linkedin.md)
