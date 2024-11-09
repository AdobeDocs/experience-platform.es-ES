---
title: Guía de API de autorización del servicio de consultas
description: Aprenda a utilizar la API de autorización del servicio de consultas para aplicar restricciones IP basadas en la red para conexiones seguras a través de SQL. Utilice esta API para mejorar el control de acceso a los datos de Adobe Experience Platform.
role: Developer
source-git-commit: f673d0d71458fe87491318f06be59719e4c9d76c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# Guía de API de autorización del servicio de consultas

Utilice la API de autorización del servicio de consultas para aplicar restricciones basadas en IP. La aplicación de estas medidas garantiza que solo las redes y los equipos cliente aprobados puedan acceder a los datos a través de SQL en Adobe Experience Platform. Estos controles le ayudan a cumplir con los estrictos estándares de seguridad, a la vez que proporcionan supervisión y alertas de acceso en tiempo real.

Con esta API, puede configurar, aplicar y supervisar restricciones IP para acceder a datos a través de la interfaz SQL. Este documento proporciona información general de alto nivel sobre las funciones principales, las funciones de punto de conexión y las funciones futuras de la API.

## Características principales

Las siguientes funciones permiten definir restricciones de acceso basadas en IP, supervisar intentos de acceso y personalizar la configuración de seguridad de red para el servicio de consultas:

- **Definir controles de acceso a datos basados en la red**: especifique los intervalos de IP permitidos para el acceso al Servicio de consultas. Esta restricción se aplica específicamente a las conexiones a bases de datos SQL, incluidas las realizadas mediante herramientas de Business Intelligence (BI), clientes de base de datos o interfaces de programación como JDBC.
- **Habilitar alertas y supervisión exhaustivas**: todos los intentos de acceso, incluidas las conexiones denegadas, se registran y se envían a los [Registros de auditoría de Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) para su seguimiento en tiempo real. Utilice esta capacidad para supervisar los patrones de acceso y detectar posibles brechas de seguridad.
- **Configurar restricciones de IP flexibles**: especifique las IP permitidas en los formatos de bloque CIDR e IP individuales. Esta configuración se aplica por zona protegida, lo que le permite adaptar las restricciones de red a sus necesidades de seguridad específicas.

## Funciones de auditoría y supervisión

Para admitir las prácticas de acceso seguro a los datos, el servicio de consultas registra todas las IP de cliente que acceden o intentan acceder a AEP. Los eventos de auditoría, incluidas las conexiones denegadas, se envían a los registros de auditoría de Platform. Esto permite:

- **Supervisión en tiempo real**: haga un seguimiento de los patrones de acceso basados en IP para garantizar el cumplimiento.
- **Alerta de acceso no autorizado**: identifique y responda a los intentos de acceso de direcciones IP no autorizadas.

Para obtener más información sobre el registro de auditoría, consulte la [documentación del servicio de auditoría](https://experienceleague.adobe.com/docs/experience-platform/audit/audit-overview.html).

## Pasos siguientes

Empiece con la API de autorización del servicio de consultas revisando la [guía de introducción](./getting-started.md) para ver los pasos de configuración esenciales, incluidos los encabezados obligatorios y las convenciones de llamadas de API. A continuación, explore las guías específicas del extremo sobre [Acceso IP](./ip-access.md) y [Validación IP](./validate.md) para configurar y administrar el acceso de datos seguro.
