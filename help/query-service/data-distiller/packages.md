---
title: Paquetes de servicio de consulta
description: El siguiente documento describe los paquetes de funcionalidades y productos disponibles para el servicio de consulta y destaca las diferencias entre las consultas ad hoc y las consultas por lotes.
source-git-commit: 2db842c46d7075d77d3fd15c0db2b58b59e4140b
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# Paquetes de servicio de consulta

Este documento describe los diferentes tipos de paquetes y capacidades de ejecución de consultas disponibles en el servicio de consultas.

El servicio de consulta de Adobe Experience Platform se puede dividir en dos funciones en función de los patrones de consulta que se pueden ejecutar:

- **Consultas ad hoc** son consultas SQL que se utilizan para explorar conjuntos de datos ingestados para verificación, validación, experimentación, etc. Estas consultas no vuelven a escribir datos en el lago de datos de Platform.
- **Consultas por lotes** son consultas SQL utilizadas para realizar el procesamiento posterior a la ingesta de conjuntos de datos ingestados. Estas consultas limpian, moldean, manipulan y enriquecen datos, cuyos resultados se vuelven a escribir en el lago de datos de Platform. Estas consultas se pueden programar, administrar y monitorizar como trabajos por lotes.

Las funcionalidades del servicio de consulta están empaquetadas con los siguientes productos y complementos:

- **Aplicaciones basadas en plataformas** (Real-time Customer Data Platform, Customer Journey Analytics y Adobe Journey Optimizer): El acceso al servicio de consulta para ejecutar consultas ad hoc se proporciona desde el principio con cada variación y nivel de aplicaciones basadas en Platform.
- **[!DNL Data Distiller]** (paquete de complementos que se puede adquirir con Adobe Real-Time CDP, Customer Journey Analytics y Adobe Journey Optimizer): El acceso al servicio de consultas para ejecutar consultas por lotes se proporciona con [!DNL Data Distiller].

La siguiente tabla describe las autorizaciones clave del servicio de consulta en función de cómo están empaquetadas:

| Derecho de servicio de consulta | Empaquetado con aplicaciones basadas en plataforma | Empaquetado con [!DNL Data Distiller] |
|---|---|---|
| Patrón de consulta admitido | Solo consulta ad hoc | Consulta por lotes |
| Caso de uso admitido | <ul><li>&#x200B; de exploración</li><li>&#x200B; de detección de datos</li><li>Validación de datos</li><li>Experimento</li></ul> | <ul><li>Limpieza</li><li>Forma</li><li>Manipulación</li><li>Enriquecimiento</li></ul> |
| Semántica compatible | <ul><li>Consultas SELECT</li></ul> | <ul><li>Consultas de CTAS e ITAS</li></ul> |
| Tiempo máximo de ejecución | 10 minutos | 24 horas |
| Métrica de licencias | **Consulta de la concurrencia del usuario**: <ul><li>1 usuario simultáneo (CDP en tiempo real, Adobe Journey Optimizer) &#x200B;</li><li>5 usuarios simultáneos (Customer Journey Analytics) &#x200B;</li></ul> **Conversión de consulta**: <ul><li>1 consulta en ejecución simultánea (todas las aplicaciones) &#x200B;</li></ul> **Otros usuarios de consultas ad hoc incluyen complementos** se puede adquirir para aumentar los derechos de consulta ad hoc autorizados de los clientes. <ul><li>+5 usuarios simultáneos adicionales por paquete</li><li>+1 consulta de ejecución concurrente adicional por paquete</li></ul> | **Horario de cómputo**: <ul><li>Variable (según los derechos de aplicación del cliente)</li></ul> **Horario de cómputo** es una medida del tiempo que tarda el motor de Query Service en leer, procesar y escribir datos de nuevo en el lago de datos cuando se ejecuta una consulta por lotes. |
| Interfaz de ejecución de consultas | <ul><li>Interfaz de usuario del servicio de consulta</li><li>Interfaz de usuario de cliente de terceros</li><li>[!DNL PostgresSQL] interfaz de usuario del cliente</li></ul> | <ul><li>Interfaz de usuario de consulta </li><li>Interfaz de usuario de cliente de terceros</li><li>[!DNL PostgresSQL] interfaz de usuario del cliente</li><li>API de REST</li></ul> |
| Resultados De Consulta Devueltos Mediante | Interfaz de usuario del cliente | Conjunto de datos derivado almacenado en el lago de datos |
| Límite de resultados | <ul><li>Interfaz de usuario de consulta: 100 filas</li><li>Cliente de terceros: 50.000</li><li>[!DNL PostgresSQL] cliente - 50.000</li></ul> | <ul><li>Interfaz de usuario de consulta (sin límite superior de filas)</li><li>Clientes de terceros (sin límite superior de filas)</li><li>[!DNL PostgresSQL] cliente (sin límite superior de filas)</li><li>API de REST (sin límite superior de filas)</li></ul> |
| Leer la capacidad del conjunto de datos | Sí | Sí |
| Capacidad de escritura de conjunto de datos | No | Sí |
| Capacidad de programación | No | Sí |
| Monitorización de la capacidad | Sí | Sí |
| Capacidad de configuración de alertas de consulta | No | Sí |

{style=&quot;table-layout:auto&quot;}

## Control de acceso

El control de acceso para el Experience Platform se administra a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com/) donde los perfiles de producto vinculan a los usuarios con permisos y entornos limitados. Consulte la [información general sobre el control de acceso](../../access-control/home.md) para obtener más información.

Para utilizar el servicio de consulta, la variable [!DNL Manage Queries] el permiso debe estar habilitado en admin console. Este permiso permite a los usuarios ejecutar consultas ad hoc y por lotes. Instrucciones detalladas para solicitar acceso al perfil del producto [!DNL Manage Queries] se han descrito en [administrar permisos para un perfil de producto](../../access-control/ui/permissions.md) y [administrar usuarios para un perfil de producto](../../access-control/ui/users.md) documentos.

Después de comprar el [!DNL Data Distiller] complemento, la variable [!DNL Write Dataset] debe concederse el permiso. Este permiso permite [!DNL Data Distiller] usuarios para ejecutar consultas por lotes.

En la tabla siguiente se describen los efectos del [!DNL Manage Queries] permiso:

| Permiso | Función |
|---|---|
| [!DNL Manage Queries] (sin permiso de escritura de datos) | Proporciona acceso para ejecutar consultas ad hoc |
| [!DNL Manage Queries] (con permiso de escritura de datos) | Proporciona acceso para ejecutar consultas por lotes |

{style=&quot;table-layout:auto&quot;}

## Compatibilidad con Sandbox

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform. Cada instancia de Platform admite varias producciones y entornos limitados que no sean de producción, cada uno de los cuales mantiene su propia biblioteca de recursos de Platform. Los entornos limitados que no son de producción permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre los entornos limitados, consulte la [información general sobre los entornos limitados](../../sandboxes/home.md). Todas las autorizaciones del servicio de consulta se comparten entre todos los entornos limitados

## Pasos siguientes

Al leer este documento, debería tener una mejor comprensión de los diferentes tipos de paquetes y capacidades de ejecución de consultas disponibles en el servicio de consultas. Para obtener más información sobre el servicio de consulta, como los casos de uso conocidos del sector, lea la [documentación de caso de uso](../use-cases/abandoned-browse.md). Para obtener información más general, consulte la [Información general del servicio de consultas](../home.md).
