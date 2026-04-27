---
solution: Real-Time Customer Data Platform
title: Trabajo con clientes de MCP (Beta)
description: Obtenga información sobre cómo conectar Adobe Real-Time CDP a clientes MCP mediante el servidor MCP
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# Trabajo con clientes de MCP (Beta) {#rtcdp-mcp}

Puede utilizar la integración de MCP de Adobe Real-Time CDP para consultar audiencias, destinos y estado de activación mediante mensajes en lenguaje sencillo, sin escribir llamadas de API ni navegar por las pantallas de productos. Esta página explica cómo funciona la integración, qué puede hacer con ella y cómo empezar.

>[!AVAILABILITY]
>
>El servidor MCP de Real-Time CDP se distribuye como un **servidor de transporte HTTP remoto** que los usuarios instalan y configuran en las plataformas de aplicaciones y clientes MCP admitidos (por ejemplo, Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code). La autenticación se administra a través de un **flujo de inicio de sesión basado en explorador**: cuando el cliente se conecta por primera vez al servidor, abre el explorador predeterminado para que pueda iniciar sesión con las credenciales de Adobe y autorizar el acceso. Póngase en contacto con su representante de Adobe para acceder a este programa de Beta.

## Beta, seguridad y avisos legales {#mcp-notices}

**Aviso sobre la documentación de Beta:** Esta documentación cubre una función de Beta y no constituye documentación final. El contenido que se describe aquí está relacionado con una versión de Beta y está sujeto a cambios antes de su publicación general. Adobe no realiza ninguna declaración sobre la integridad o precisión de esta documentación.

Al usar Adobe Real-Time CDP MCP Server (Beta) (&quot;Beta&quot;), Usted reconoce por la presente que Beta se proporciona **&quot;tal cual&quot; sin garantía de ningún tipo**. Adobe no tiene obligación de mantener, corregir, actualizar, cambiar, modificar o apoyar de otro modo Beta. Se recomienda tener precaución y no confiar en modo alguno en el correcto funcionamiento o rendimiento de dichos Beta y/o materiales de acompañamiento. Beta se considera información confidencial de Adobe. Cualquier &quot;comentario&quot; (información sobre Beta, incluidos, entre otros, problemas o defectos que encuentre al utilizar Beta, sugerencias, mejoras y recomendaciones) proporcionado por usted a Adobe se asigna a Adobe, incluidos todos los derechos, el título y el interés en y para dichos comentarios.

>[!WARNING]
>
>El Modelo de Protocolo de Contexto (MCP) es un estándar de código abierto emergente y puede presentar riesgos de seguridad o fiabilidad. Las integraciones del servidor de Adobe MCP y la documentación relacionada se proporcionan &quot;tal cual&quot;, sin garantías de ningún tipo.
>
>La conexión de clientes o servidores MCP a productos de Adobe es una configuración seleccionada por el cliente. Los clientes son responsables de evaluar la seguridad y la idoneidad de cualquier integración de MCP. Adobe no se responsabiliza de los problemas que se deriven de una configuración incorrecta, un uso incorrecto del MCP, vulnerabilidades en implementaciones de terceros o acciones no deseadas realizadas a través de flujos de trabajo habilitados para MCP.
>
>Para reducir el riesgo, Adobe recomienda probar las integraciones en un entorno de zona protegida antes de usarlas de forma productiva y revisar y validar cuidadosamente todas las acciones y respuestas iniciadas por MCP antes de confirmarlas o depender de ellas.

## ¿Qué es el protocolo de contexto del modelo? {#mcp-overview}

Los equipos de marketing, datos y experiencia del cliente dependen cada vez más de las aplicaciones basadas en chat y las herramientas para desarrolladores, como Anthropic Claude, OpenAI ChatGPT, Cursor y Microsoft Copilot Studio, para optimizar su trabajo diario. Estas aplicaciones admiten el **Protocolo de contexto de modelo (MCP)**, un estándar abierto que permite a las aplicaciones exponer las herramientas back-end a modelos de lenguaje de gran tamaño (LLM) de manera uniforme.

Real-Time CDP ahora proporciona un servidor MCP que muestra las operaciones de audiencia, destino y activación directamente dentro de cualquier aplicación compatible con MCP. Con la integración de Real-Time CDP MCP, diferentes personas pueden colaborar en torno a los mismos datos de segmentación y activación, sin necesidad de escribir consultas contra las API de REST de Adobe Experience Platform ni navegar por varias pantallas de interfaz de usuario. Los clientes pueden describir su intención de manera conversacional y dejar que el LLM invoque las herramientas de MCP apropiadas.

## Funcionalidades clave {#mcp-capabilities}

El servidor MCP de Real-Time CDP le permite inspeccionar, resumir y solucionar problemas de audiencias y destinos directamente desde su asistente de IA. Todas las operaciones son **de solo lectura** — las superficies del servidor MCP recuperan las API como respuestas en lenguaje sencillo para que pueda:

* **Obtener visibilidad instantánea de la audiencia**: pregúntele sobre las definiciones de audiencia, el estado del ciclo vital y el área de nombres en lenguaje sencillo sin navegar por los menús ni extraer informes manualmente.
* **Estimar el tamaño de la audiencia antes de la activación**: previsualice los recuentos de miembros y los intervalos de confianza para una consulta de segmento de PQL o SDD antes de comprometerse a crear una audiencia.
* **Audite tu portafolio de activación**: revisa los destinos configurados, los flujos de datos que los alimentan y las conexiones de origen/destino detrás de cada flujo, sin analizar JSON ni saltar a través de las pantallas de productos.
* **Problemas de activación puntual al principio**: el destino de Surface falló o está en curso se ejecuta en el momento que usted lo solicita, para que su equipo pueda actuar con rapidez.
* **Colabore en torno a datos activos**: los especialistas en marketing, los ingenieros de datos y las partes interesadas pueden consultar los mismos datos de Real-Time CDP activos a través de su asistente de IA, lo que facilita la alineación, la decisión y la movilidad juntas.

## Herramientas disponibles {#mcp-tools}

La disponibilidad de las herramientas cambia rápidamente a medida que habilitamos nuevas herramientas. Póngase en contacto con su representante de Adobe para obtener una lista de las herramientas disponibles más recientes.

>[!NOTE]
>
>Todas las herramientas son **de solo lectura**. Las operaciones de escritura (creación, actualización o eliminación de audiencias, destinos o flujos de datos) no son compatibles con la versión actual de Beta.

## Casos de uso {#mcp-use-cases}

Los siguientes ejemplos muestran cómo interactuar con el servidor MCP [!DNL Adobe Real-Time CDP] mediante lenguaje natural:

| Objetivo | Mensaje de ejemplo |
| --- | --- |
| **Descubrimiento del catálogo de destino** | &quot;¿TikTok está disponible como destino en mi zona protegida?&quot; / &quot;¿Para qué tipos de destino ya tengo cuentas configuradas?&quot; |
| **Inventario de destino por tipo** | &quot;Enumerar todos mis destinos de Amazon S3&quot;. / &quot;¿Tengo algún destino de exportación de conjunto de datos configurado?&quot; |
| **Auditoría de configuración de destino** | &quot;¿En qué contenedor está escribiendo mi destino `Loyalty S3 Export`?&quot; / &quot;Mostrarme la ruta de acceso de destino y el formato de archivo para el flujo de datos [ID]&quot;. |
| **Estado de la cuenta** | &quot;¿Cuál de mis cuentas de destino tiene credenciales caducadas?&quot; / &quot;¿Hay alguna cuenta de Pinterest o Facebook en estado de error?&quot; |
| **Estado de activación — últimas 24 horas** | &quot;Enumerar todos los destinos con una ejecución fallida en las últimas 24 horas&quot;. / &quot;¿Mi destino de exportación de conjuntos de datos ha enviado datos en las últimas 24 horas?&quot; |
| **Historial de activación por destino** | &quot;¿Exportó algo `Weekly Loyalty Export` en los últimos 30 días?&quot; / &quot;Mostrarme el historial de ejecución completo del destino {NAME}.&quot; |
| **Análisis de errores** | &quot;¿Cuál es el motivo de error más común en mis destinos basados en archivos esta semana?&quot; / &quot;Agrupar ejecuciones fallidas recientes por tipo de error&quot;. |
| **Detección y filtrado de audiencias** | &quot;Enumerar cada audiencia basada en CSV en la zona protegida `marketing-prod`&quot;. / &quot;¿Qué audiencias tienen un ID de audiencia externa definido?&quot; |
| **Auditoría de tamaño de audiencia** | &quot;Mostrar todas las audiencias con tamaño 0&quot;. / &quot;¿Qué audiencias tienen más de 1000 perfiles?&quot; |
| **Auditoría de caducidad de audiencias** | &quot;¿Qué destinos tienen audiencias cuya fecha de finalización ya ha pasado?&quot; / &quot;Enumerar audiencias que caducarán en los próximos 7 días&quot;. |
| **Espacio de activación de audiencia** | &quot;¿Qué destinos tienen más de 10 audiencias activadas?&quot; / &quot;¿Qué audiencia se activa a la mayoría de los destinos?&quot; |
| **Filtro cruzado: activación de × de audiencia** | &quot;Mostrarme audiencias con un tamaño superior a 1000 que estén activadas en al menos 2 destinos&quot;. / &quot;Audiencias grandes que solo se activan en un único destino&quot;. |
| **Vista previa de pertenencia a audiencia** | &quot;Vista previa del tamaño de los miembros para la audiencia `High-Value Loyalty Members`.&quot; / &quot;Calcule el tamaño de esta consulta de PQL antes de guardarla: {EXPRESSION}&quot;. |

## Requisitos previos {#mcp-prerequisites}

Antes de conectar el servidor MCP de Real-Time CDP a su cliente MCP, asegúrese de lo siguiente:

* Tiene una licencia de Real-Time CDP activa.
* Tiene acceso a un cliente compatible que puede conectarse a un servidor MCP remoto o a una aplicación MCP personalizada, como Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code.
* Tiene el ID de organización y el nombre de la zona protegida que desea consultar.
* Tiene los permisos necesarios en Adobe Experience Platform para ver audiencias, destinos y entidades de servicios de flujo.

## Conexión del servidor MCP de Real-Time CDP {#mcp-connect}

>[!NOTE]
>
>Esta integración se realiza en Beta. Los menús del cliente, los requisitos del plan y los controles de administración pueden variar según la aplicación y la versión.

Antes de empezar, asegúrese de que dispone de lo siguiente:

* Dirección URL del extremo del servidor MCP: `Available to Beta customers through your Adobe representative`.
* Confirmación de que el usuario de Adobe tiene acceso a la organización de Experience Platform y a la zona protegida de destino.

El servidor MCP de Real-Time CDP es un **servidor HTTP MCP remoto**. En cada cliente, la configuración sigue el mismo patrón:

1. Añada la URL del servidor.
2. Guarde o habilite la conexión.
3. Complete el **inicio de sesión en Adobe basado en explorador** la primera vez que el cliente invoque una herramienta.
4. Proporcione a `imsOrgId` y a `sandboxName` con cada solicitud.

### Instalar en clientes basados en IU {#mcp-connect-ui}

#### Claude

Para `claude.ai` y Claude Desktop, agregue el servidor MCP de Real-Time CDP como **conector personalizado** mediante el extremo proporcionado por su representante de Adobe. En los planes de Claude individuales, agréguelo en **Personalizar > Conectores**. En los planes de equipo y empresa, es posible que un propietario tenga que agregarlo primero en **Configuración de la organización > Conectores**, después de lo cual cada usuario lo conecta en su propia configuración de Claude. Una vez configurado, habilite el conector en una conversación y complete el inicio de sesión del explorador Adobe la primera vez que lo use.

#### ChatGPT

En ChatGPT, agregue el servidor MCP de Real-Time CDP como **aplicación/conector personalizado** usando el punto de conexión proporcionado por su representante de Adobe. Según su plan de ChatGPT, esto puede requerir **modo de desarrollador** y la aprobación del administrador del espacio de trabajo. Una vez que la aplicación o el conector se hayan creado o habilitado, conéctelos desde **Configuración > Aplicaciones** o **Configuración > Aplicaciones y conectores** y, a continuación, autentifíquese mediante el inicio de sesión del explorador Adobe cuando se le solicite.

#### Cursor

En Cursor, agregue el servidor MCP de Real-Time CDP como servidor MCP remoto mediante el punto final proporcionado por su representante de Adobe. Abra **Configuración > MCP**, agregue un servidor nuevo y pegue la dirección URL del extremo. Una vez agregado, habilite el servidor para su área de trabajo seleccionando **connect** para autenticarse mediante el explorador.

#### Otros clientes basados en IU

Para clientes como código VS u otras aplicaciones de escritorio y web con compatibilidad con MCP remoto, agregue el servidor MCP de Real-Time CDP como un servidor HTTP **remoto** usando el extremo proporcionado por su representante de Adobe. Si el cliente admite encabezados opcionales o tokens de portador, déjelos vacíos a menos que Adobe indique específicamente lo contrario; la autenticación se administra mediante el flujo de inicio de sesión de Adobe basado en el explorador la primera vez que se utiliza.

### Instalar en clientes técnicos {#mcp-connect-technical}

#### Código Claude

Añada el servidor desde el terminal:

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

A continuación, inicie Claude Code y ejecute:

```text
/mcp
```

Seleccione el servidor `rtcdp` y complete el flujo de inicio de sesión de Adobe en su explorador. Si ya agregó el servidor en `claude.ai`, también puede aparecer automáticamente en el código de la cláusula cuando ambos usen la misma cuenta.

#### Códice

Añada el servidor desde el terminal:

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

Autentique el servidor:

```bash
codex mcp login rtcdp
```

Compruebe la configuración:

```bash
codex mcp list
```

También puede agregar el servidor directamente a `~/.codex/config.toml`:

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### Parámetros de solicitud requeridos {#mcp-connect-params}

Cada llamada a la herramienta requiere dos parámetros que amplían el ámbito de la solicitud:

* `imsOrgId`: su ID de organización, asignado al encabezado `x-gw-ims-org-id` en las llamadas a la API de Experience Platform descendentes.
* `sandboxName`: el nombre de la zona protegida de Experience Platform, asignado al encabezado `x-sandbox-name`.

## Limitaciones conocidas (Beta) {#mcp-limitations}

Las siguientes limitaciones se aplican a la versión actual de Beta del servidor MCP [!DNL Adobe Real-Time CDP]:

| Limitación | Descripción | Solución alternativa |
| --- | --- | --- |
| **Superficie de solo lectura** | El servidor MCP solo expone las API de recuperación. No puede crear, actualizar, activar ni eliminar audiencias, destinos o flujos de datos. | Utilice la interfaz de usuario de Real-Time CDP o las API de REST de AEP para operaciones de escritura. |
| **Sin métricas de participación o envío** | El servidor MCP no devuelve estadísticas de envío descendente, participación o métricas de conversión desde las plataformas de destino. | Utilice los propios informes de la plataforma de destino, Customer Journey Analytics MCP o Adobe Analytics MCP para los datos de participación y conversión. |
| **La consulta de segmentos debe crearse externamente** | `Preview Audience Membership` requiere una expresión PQL o SDD válida como entrada; el servidor MCP no crea la consulta automáticamente. | Cree la expresión PQL/SDD en la interfaz de usuario del Generador de segmentos o a través de la API del servicio de segmentación y péguela en el símbolo del sistema de MCP. |
| **Paginación mediante tokens de continuación** | Las herramientas de lista devuelven resultados paginados. La enumeración completa en zonas protegidas muy grandes requiere encadenar `continuationToken` llamadas. | Reduzca las consultas mediante filtros (nombre, estado, especificación de conexión, intervalo de tiempo) en lugar de enumerar la lista completa. |
| **El filtrado de la ejecución de activación solo se basa en el tiempo** | `Inspect Activation Runs` admite el filtrado por estado y marca de tiempo de finalización (epoch ms UTC), pero no por tipo de error o plataforma de destino directamente. | Filtre primero por `flowId` (obtenido de `List Configured Destinations`) para que el ámbito se ejecute en un destino específico. |
| **Se requiere la configuración de región** | Las llamadas a la herramienta fallarán con HTTP 403 &quot;Falta la región del usuario&quot; si la puerta de enlace MCP no está configurada para la región del usuario. | Póngase en contacto con su representante de Adobe para confirmar que la puerta de enlace está configurada para su región antes de usarla por primera vez. |

## Preguntas frecuentes {#mcp-faq}

+++¿Qué clientes MCP son compatibles?

El servidor MCP de Real-Time CDP funciona con clientes compatibles que pueden conectarse a servidores MCP remotos o aplicaciones MCP personalizadas, como Claude, ChatGPT, Claude Code, Codex, Cursor y VS Code. El flujo de instalación depende del cliente: los clientes basados en la interfaz de usuario suelen agregar el servidor desde la configuración, mientras que los clientes técnicos como Claude Code y Codex pueden agregarlo desde la línea de comandos o los archivos de configuración.
+++

+++¿Cómo funciona la autenticación?

La autenticación se administra mediante un **inicio de sesión basado en explorador**. Cuando el cliente de MCP invoca una herramienta por primera vez, abre el explorador predeterminado a una página de inicio de sesión de Adobe. Después de autenticar y autorizar al cliente, se establece la sesión y las llamadas de herramienta posteriores lo vuelven a utilizar. No es necesario almacenar claves API ni credenciales de larga duración en la configuración del cliente.
+++

+++¿A qué objetos de Real-Time CDP puedo acceder a través de MCP?

Puede acceder a audiencias, tipos de destino, cuentas de destino configuradas, flujos de datos de destino, conexiones de origen y destino e historial de ejecución de activación. Las operaciones son de solo lectura (recuperar API); las operaciones de escritura no son compatibles con la versión actual.
+++

+++¿Necesito acceso de desarrollador para utilizar el servidor MCP de Real-Time CDP?

No. El servidor MCP está diseñado tanto para personalidades técnicas como de marketing. Los especialistas en marketing pueden interactuar con él mediante peticiones de datos en lenguaje natural en cualquier cliente de MCP admitido, mientras que los ingenieros de datos y los desarrolladores pueden utilizarlo en herramientas para desarrolladores compatibles con MCP.
+++

+++¿Se envían mis datos al proveedor del cliente de MCP?

Cuando envía una solicitud, el cliente MCP puede enviar contexto relevante (incluidos los datos de Real-Time CDP devueltos por el servidor MCP) a su modelo para su procesamiento. Revise las políticas de privacidad y administración de datos de su proveedor de cliente MCP antes de conectarse a los datos de producción.
+++

+++¿Qué permisos necesito en Real-Time CDP?

Necesita al menos **permisos de visualización** para los objetos que desea consultar: audiencias, destinos y entidades de servicio de flujo. No se requieren permisos de escritura porque el servidor MCP solo realiza operaciones de lectura. Póngase en contacto con el administrador de [!DNL Adobe Experience Platform] si no está seguro del nivel de acceso actual.
+++

+++¿Puedo utilizar el servidor MCP en entornos de espacio aislado?

Sí. Cada llamada a la herramienta requiere un parámetro `sandboxName`, por lo que el servidor MCP siempre respeta la configuración de la zona protegida [!DNL Adobe Experience Platform]. Puede consultar cualquier zona protegida a la que tenga acceso especificando su nombre en la solicitud.
+++

+++¿Cuál es la diferencia entre Previsualizar pertenencia a audiencia y Buscar audiencias existentes?

`Search Existing Audiences` devuelve audiencias que ya se han creado y guardado en su zona protegida. `Preview Audience Membership` toma una expresión de segmento PQL o SDD sin procesar y devuelve una estimación de tamaño para ella, lo cual resulta útil para cambiar el tamaño de una consulta *antes de* guardarla como audiencia.
+++

+++¿Puedo consultar audiencias de cuenta y de perfil?

Sí. Tanto `Search Existing Audiences` como `Preview Audience Membership` admiten un parámetro de tipo de entidad. Las audiencias de perfil se pueden expresar en PQL o SDD; las audiencias de cuenta siempre utilizan sintaxis SDD (relacional).
+++
