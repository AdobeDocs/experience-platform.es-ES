---
title: Información general sobre la extensión Splunk
description: Obtenga información acerca de la extensión Splunk para el reenvío de eventos en Adobe Experience Platform.
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 1%

---

# Información general sobre la extensión Splunk

[Splunk](https://www.splunk.com) es una plataforma de observabilidad que proporciona búsqueda, análisis y visualización de perspectivas procesables en sus datos. El Splunk [reenvío de eventos](../../../ui/event-forwarding/overview.md) La extensión de aprovecha [API de REST del recopilador de eventos HTTP de Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) para enviar eventos desde Adobe Experience Platform Edge Network a [Recopilador de eventos HTTP de Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk utiliza tokens de portador como mecanismo de autenticación para comunicarse con la API del Recopilador de eventos de Splunk.

## Casos de uso {#use-cases}

Los equipos de marketing pueden utilizar la extensión para los siguientes casos de uso:

| Caso de uso | Descripción |
| --- | --- |
| Análisis del comportamiento del cliente | Las organizaciones pueden capturar datos de eventos de interacción de clientes desde su sitio web y reenviar eventos relevantes a Splunk. Los equipos de marketing y análisis pueden realizar análisis subsiguientes dentro de la plataforma Splunk para comprender las interacciones y el comportamiento clave del usuario. La plataforma Splunk se puede utilizar para generar gráficos, paneles u otras visualizaciones para informar a las partes interesadas empresariales. |
| Búsqueda escalable en conjuntos de datos grandes | Las organizaciones pueden capturar entradas transaccionales o conversacionales como datos de evento del sitio web y reenviar eventos a Splunk. Los equipos de Analytics pueden aprovechar las capacidades de indexación escalable de Splunk para filtrar y procesar grandes conjuntos de datos para obtener perspectivas comerciales y tomar decisiones informadas. |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Debe tener una cuenta de Splunk para utilizar esta extensión. Puede registrarse para obtener una cuenta de Splunk en la [Página principal de Splunk](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> La extensión de Splunk admite instancias empresariales de Splunk Cloud y Splunk. Esta guía documenta una implementación de mediante [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) como referencia. El proceso de configuración para [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) es similar, pero requiere orientación específica de su administrador de Splunk Enterprise.

También debe tener los siguientes valores técnicos para configurar la extensión:

* Un [Token de recopilador de eventos](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Los tokens suelen tener un formato UUIDv4 como el siguiente: `12345678-1234-1234-1234-1234567890AB`.
* La dirección y el puerto de la instancia de la plataforma Splunk para su organización. Una dirección y un puerto de instancia de plataforma suelen tener el siguiente formato: `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Los extremos de Splunk a los que se hace referencia en el reenvío de eventos solo deben utilizar el puerto `443`. Actualmente, los puertos no estándar no son compatibles con las implementaciones de reenvío de eventos.

## Instalación de la extensión de Splunk {#install}

Para instalar la extensión Splunk Event Collector en la interfaz de usuario de, vaya a **Reenvío de eventos** y seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, vaya a **Extensiones** > **Catálogo**. Buscar &quot;[!DNL Splunk]&quot;, y luego seleccione **[!DNL Install]** en la extensión de Splunk.

![Botón Instalar para la extensión Splunk que se está seleccionando en la IU](../../../images/extensions/server/splunk/install.png)

## Configuración de la extensión Splunk {#configure_extension}

>[!IMPORTANT]
>
>Según sus necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de empezar para determinar qué entidades debe configurar para su caso de uso.

Seleccionar **Extensiones** en el panel de navegación izquierdo. En **Instalado**, seleccione **Configurar** en la extensión Splunk.

![Botón Configurar para la extensión Splunk que se está seleccionando en la IU](../../../images/extensions/server/splunk/configure.png)

Para **[!UICONTROL URL del recopilador de eventos HTTP]**, introduzca la dirección y el puerto de la instancia de la plataforma Splunk. En **[!UICONTROL Token de acceso]**, introduzca su [!DNL Event Collector Token] valor. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Opciones de configuración rellenadas en la interfaz de usuario](../../../images/extensions/server/splunk/input.png)

## Configuración de una regla de reenvío de eventos {#config_rule}

Empezar a crear una nueva regla de reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione [!UICONTROL Splunk] extensión y, a continuación, seleccione la [!UICONTROL Crear evento] tipo de acción. Aparecen controles adicionales para configurar aún más el evento Splunk.

![Definir configuración de acción](../../../images/extensions/server/splunk/action-configurations.png)

El siguiente paso es asignar las propiedades del evento Splunk a los elementos de datos que haya creado anteriormente. A continuación se proporcionan las asignaciones opcionales admitidas basadas en los datos de evento de entrada que se pueden configurar. Consulte la [Documentación de Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) para obtener más información.

| Nombre del campo | Descripción |
| --- | --- |
| [!UICONTROL Evento ]<br><br>**(OBLIGATORIO)** | Indique cómo desea proporcionar los datos de evento. Los datos de evento se pueden asignar a `event` dentro del objeto JSON en la solicitud HTTP o puede ser texto sin procesar. El `event` La clave está en el mismo nivel dentro del paquete de eventos JSON que las claves de metadatos. Dentro de `event` llaves clave-valor, los datos pueden estar en cualquier formulario que necesite (como una cadena, un número, otro objeto JSON, etc.). |
| [!UICONTROL Host] | El nombre de host del cliente desde el que envía los datos. |
| [!UICONTROL Tipo de origen] | Tipo de origen que se asigna a los datos de evento. |
| [!UICONTROL Fuente] | Valor de origen que se asigna a los datos de evento. Por ejemplo, si está enviando datos desde una aplicación que está desarrollando, establezca esta clave en el nombre de la aplicación. |
| [!UICONTROL Índice] | Nombre del índice de los datos del evento. El índice que especifique aquí debe estar dentro de la lista de índices permitidos si el token tiene el parámetro indexes establecido. |
| [!UICONTROL Fecha] | La hora del evento. El formato de hora predeterminado es Tiempo UNIX (con el formato `<sec>.<ms>`) y depende de su zona horaria local. Por ejemplo, `1433188255.500` indica 1433188255 segundos y 500 milisegundos después de epoch o el lunes, 1 de junio de 2015, a las 7:50:17:00 GMT. |
| [!UICONTROL Campos] | Especifique un objeto JSON sin procesar o un conjunto de pares clave-valor que contengan campos personalizados explícitos que se definirán en el momento del índice.  El `fields` La clave no es aplicable a los datos sin procesar.<br><br>Solicitudes que contienen el `fields` La propiedad debe enviarse a `/collector/event` punto final o, de lo contrario, no se indexarán. Para obtener más información, consulte la documentación de Splunk sobre [extracciones de campo indexadas](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Validación de datos en Splunk {#validate}

Después de crear y ejecutar la regla de reenvío de eventos, valide si el evento enviado a la API de Splunk se muestra según lo esperado en la interfaz de usuario de Splunk. Si la recopilación de eventos y la integración del Experience Platform se realizaron correctamente, verá eventos dentro de la consola de Splunk de esta manera:

![Los datos de evento que aparecen en la IU de Splunk durante la validación](../../../images/extensions/server/splunk/splunk-data.png)

## Pasos siguientes

Este documento explica cómo instalar y configurar la extensión de reenvío de eventos Splunk en la interfaz de usuario. Para obtener más información sobre la recopilación de datos de eventos en Splunk, consulte la documentación oficial:

* [Configuración y uso del Recopilador de eventos HTTP en Splunk Web ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Configuración de la autenticación con tokens](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Solucionar problemas del recopilador de eventos HTTP](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (también enumera un compendio de [posibles códigos de error](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
