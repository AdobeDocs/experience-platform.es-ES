---
keywords: Experience Platform; servicio de consultas; control de acceso IP; autorización; API; introducción
title: Guía de API de autorización del servicio de consultas
description: Obtenga información sobre cómo empezar a aplicar restricciones de autorización y de intervalo de IP para el acceso seguro a datos en el servicio de consultas de Adobe Experience Platform.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 6%

---

# Guía de API de autorización del servicio de consultas

>[!AVAILABILITY]
>
>Esta funcionalidad está disponible para los clientes que han adquirido el complemento Data Distiller. Para obtener más información, contacte con su representante de Adobe.

La API de autorización del servicio de consultas proporciona a las organizaciones un control más estricto sobre el acceso a los datos a través de la interfaz SQL en Adobe Experience Platform. Puede utilizar esta API para definir restricciones de IP, limitar el acceso a datos a redes específicas y mejorar la monitorización de la seguridad.

Esta guía describe cómo configurar las credenciales de autorización y los permisos necesarios para realizar llamadas a la API de autorización del servicio de consultas.

## Introducción {#getting-started}

Las secciones siguientes proporcionan información sobre la preparación de los valores de autorización necesarios y la realización de las primeras solicitudes a la API de autorización del servicio de consultas.

### Permisos necesarios {#required-permissions}

Para habilitar las restricciones de acceso a datos seguros en Query Service, necesita el permiso **[!UICONTROL Administrar Lista de permitidos]**. Este permiso permite a las organizaciones definir intervalos de IP específicos (en formato IPv4 o IPv6) autorizados para acceder a los datos en Platform a través de la interfaz SQL. El acceso se administra en el nivel de zona protegida, donde los usuarios pueden configurar una lista de direcciones IP aprobadas o bloques CIDR que restrinjan el acceso solo a redes permitidas.

>[!NOTE]
>
>Los administradores del sistema pueden configurar permisos de usuario desde el Adobe [Admin Console](https://adminconsole.adobe.com/). Para obtener más información, consulte la [Guía del usuario de Admin Console](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

Las siguientes funcionalidades están disponibles con el permiso **[!UICONTROL Administrar Lista de permitidos]**:

- **Definir intervalos de IP permitidos**: solo las direcciones IP o los bloques CIDR de estos intervalos definidos pueden acceder a los datos en Platform mediante SQL a través del servicio de consultas.
- **Aplicar comprobaciones de intervalo de IP**: se deniegan las conexiones desde direcciones IP que no están dentro de los intervalos permitidos.
- **Funciones de auditoría y alertas**: todos los intentos de acceso, incluidas las conexiones denegadas, se registran como eventos de auditoría. Estos eventos están disponibles en los [Registros de auditoría de Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md), lo que permite supervisar las posibles violaciones de seguridad.

### Recopilación de valores para los encabezados obligatorios {#gather-values-for-required-headers}

Para realizar llamadas a la API de autorización del servicio de consultas, debe completar el [tutorial de autenticación de la API de plataforma](../../landing/api-authentication.md), que proporciona valores para los encabezados necesarios en las llamadas a la API. Incluya los siguientes encabezados en cada solicitud:

- **Autorización**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Para obtener más información sobre las zonas protegidas, consulte la [documentación general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) también requieren este encabezado:

- **Tipo de contenido**: `application/json`

### Pasos siguientes

Con los permisos y valores de encabezado requeridos recopilados, está listo para empezar a configurar restricciones de IP para el servicio de consulta. Continúe con la documentación del extremo para ver ejemplos detallados de operaciones de CRUD, que incluyen:

- Formato de API y pares de solicitud/respuesta de ejemplo.
- Encabezados, cargas útiles y códigos de respuesta para cada operación.

Cada ejemplo de llamada a la API muestra cómo dar formato a las solicitudes e interpretar las respuestas, lo que le ayuda a aplicar el acceso seguro a los datos en el servicio de consultas.

Para obtener instrucciones específicas sobre cómo configurar y validar restricciones IP, consulte la [documentación del extremo de acceso IP](./ip-access.md) y la [documentación del extremo de validación IP](./validate.md).
