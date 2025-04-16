---
title: Redireccionamiento fuera del sitio de visitantes no autenticados
description: Obtenga información sobre cómo redireccionar usuarios no autenticados mediante ECID
feature: Use Cases, Customer Acquisition
source-git-commit: 672b15b0c36efbf3b7d62ec616f254fffe3dbb81
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Retargeting no autenticado {#unauthenticated-retargeting}

A medida que las cookies de terceros pierden eficacia, las empresas están realizando la transición a soluciones sin cookies para lograr una participación y un redireccionamiento personalizados. La resegmentación fuera del sitio permite a las empresas llegar a usuarios con muchas intenciones en función de sus interacciones anteriores, sin depender de JavaScript del lado del cliente.

## Razones para considerar la retargeting de visitantes no autenticados {#why-use-case}

Al integrar Web SDK de Adobe Experience Platform y el reenvío de eventos del lado del servidor, puede optimizar el streaming de eventos y el reenvío de datos. Esto permite un retargeting sin problemas de usuarios no autenticados mediante ECID (Experience Cloud ID), lo que garantiza una participación coherente entre plataformas. Con esta solución, puede aumentar las oportunidades de conversión volviendo a dirigirse de forma eficaz a los usuarios no autenticados en función de sus interacciones anteriores.

## Requisitos previos y planificación {#prerequisites-and-planning}

Antes de continuar con la implementación de Web SDK y la configuración del reenvío de eventos, asegúrese de lo siguiente:

1. **Adobe con la configuración de Web SDK**: Adobe Web SDK debe implementarse para facilitar la recopilación de eventos y el reenvío de datos.

2. **Configuración de Adobe Experience Platform Edge Network**: Asegúrese de que Edge Network esté configurado para admitir el reenvío de eventos en tiempo real para el redireccionamiento fuera del sitio.

3. **Sincronización de ECID**: Asegúrese de que los ECID estén sincronizados en todas las plataformas para habilitar la coincidencia de audiencias sin problemas.

## Cómo lograr el retargeting fuera del sitio {#achieve-offsite-retargeting}

1. **Implementar Web SDK**: Implemente Adobe Web SDK en su sitio web para capturar datos de eventos en tiempo real, incluidas las interacciones de los usuarios, como vistas de páginas, clics y otros comportamientos.

2. **Habilitar el reenvío de eventos**: configure el reenvío de eventos en Platform para enviar los datos recopilados de los usuarios, lo que garantiza una transferencia de datos eficaz para la activación de audiencias.

3. **Configuración de la activación del lado del servidor**: utilice las capacidades del lado del servidor de Adobe para activar audiencias de retargeting basadas en ECID, lo que garantiza una segmentación de audiencia precisa en todas las plataformas.

4. **Crear audiencias con redireccionamiento**: Utilice las herramientas de segmentación de audiencia de Platform para definir audiencias centradas en función del comportamiento del usuario, como vistas, interacciones o carros de compras abandonados.

5. **Activar audiencias**: Una vez creadas las audiencias a las que se ha vuelto a dirigir, actívelas para ofrecer contenido personalizado; de este modo, se garantiza que los usuarios vuelvan a participar en función de sus interacciones anteriores con el sitio.

## Creación de una audiencia con el atributo calculado {#create-audience}

Para redirigirse de forma eficaz a los usuarios con intención alta, cree audiencias basadas en sus interacciones pasadas con el sitio web. Utilice Platform para segmentar usuarios mediante atributos calculados.

1. **Identificar comportamientos clave**: seleccione acciones del usuario para rastrear, como vistas de página o clics.

2. **Crear audiencias**: Use las herramientas de segmentación de audiencia para agrupar a los usuarios según sus comportamientos.

3. **Sincronizar ECID**: Asegúrese de que los ECID estén sincronizados entre plataformas para lograr una coincidencia de audiencia precisa.

## Activación de la audiencia {#activate-audience}

Una vez creada la audiencia, actívela en todas las plataformas para atraer a los usuarios.

1. **Revisar audiencias**: Asegúrese de que los segmentos de audiencia reflejen los comportamientos correctos.

2. **Crear reglas de activación**: establezca las condiciones para cuándo y cómo participan los usuarios en función de las acciones.

3. **Insertar en la plataforma**: Activar la audiencia.

4. **Supervisar rendimiento**: efectúe el seguimiento de rendimiento de audiencias y ajústelo según sea necesario.

## Configurar la extensión de retargeting fuera del sitio {#configure-extension}

### Implementación de Web SDK

Asegúrese de que Adobe Web SDK está correctamente integrado en el sitio web. Esta SDK permite recopilar datos de eventos en tiempo real, lo que resulta crucial para un resegmentado eficaz.

### Habilitar el reenvío de eventos

Configure un reenvío de eventos en Platform para enviar los datos de comportamiento del usuario recopilados a las plataformas de resegmentación. El reenvío de eventos garantiza que los datos se transmitan de forma eficaz, lo que permite a las empresas dirigirse a usuarios de alta intención sin depender de las cookies.

### Adjuntar a regla de retargeting

Asegúrese de que la extensión de retargeting fuera del sitio esté adjunta a una regla de evento válida en la recopilación de datos de Adobe Experience Platform. Normalmente, se debe crear una regla global para que se active cuando se realizan acciones clave, como `page load` o interacciones de usuario específicas.

Para obtener más información acerca de cómo configurar la extensión, lea la documentación de [Reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).

## Otros casos de uso {#other-use-cases}

Este documento proporciona información general sobre los casos de uso clave y las consideraciones técnicas para desarrollar y utilizar correctamente la configuración de SDK web y reenvío de eventos. Si sigue los procedimientos descritos y se asegura de que se cumplen los requisitos previos necesarios, puede mejorar significativamente sus capacidades de análisis y seguimiento de datos.

Puede explorar más casos de uso habilitados a través de la compatibilidad con datos de socios en Real-Time CDP:

- [Capte y adquiera nuevos clientes](./prospecting.md) mediante el uso de datos de socios.
- [Personalice experiencias en el sitio](./offsite-retargeting.md) con reconocimiento de visitantes ayudado por socios.
- [Complementar perfiles de origen](./supplement-first-party-profiles.md) con atributos proporcionados por el socio.