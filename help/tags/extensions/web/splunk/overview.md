---
title: Información general sobre la extensión del fragmento
description: Obtenga información sobre la extensión Splunk para el reenvío de eventos en Adobe Experience Platform.
source-git-commit: e6f0bdcdb11630730834e353064abb960d3d0ea1
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Información general sobre la extensión de Splunk

[Fragmento](https://www.splunk.com) es una plataforma de observación que proporciona búsqueda, análisis y visualización para obtener información procesable sobre sus datos. El Splunk [reenvío de eventos](../../../ui/event-forwarding/overview.md) la extensión de aprovecha la variable [API de REST del recopilador de eventos HTTP de Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) para enviar eventos desde la red perimetral de Adobe Experience Platform a la [Colector de eventos HTTP de fragmento](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk utiliza tokens de portador como mecanismo de autenticación para comunicarse con la API del recopilador de eventos de Splunk.

## Casos de uso {#use-cases}

Los equipos de marketing pueden utilizar la extensión para los siguientes casos de uso:

| Caso de uso | Descripción |
| --- | --- |
| Análisis del comportamiento del cliente | Las organizaciones pueden capturar datos de eventos de interacción de clientes desde su sitio web y reenviar eventos relevantes a Splunk. Los equipos de marketing y análisis pueden realizar análisis subsiguientes dentro de la plataforma Splunk para comprender las interacciones y el comportamiento de los usuarios clave. La plataforma Splunk se puede utilizar para generar gráficos, tableros u otras visualizaciones que informen a las partes interesadas del negocio. |
| Búsqueda escalable en conjuntos de datos grandes | Las organizaciones pueden capturar entradas transaccionales o conversacionales como datos de evento del sitio web y reenviar eventos a Splunk. Los equipos de Analytics pueden aprovechar las capacidades de indexación escalables de Splunk para filtrar y procesar grandes conjuntos de datos con el fin de obtener perspectivas comerciales y tomar decisiones informadas. |

{style=&quot;table-layout:auto&quot;}

## Requisitos previos {#prerequisites}

Debe tener una cuenta de Splunk para utilizar esta extensión. Puede registrarse para una cuenta de Splunk en la [Página principal de Splunk](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> La extensión Splunk es compatible con las instancias de empresa Splunk Cloud y Splunk. Esta guía documenta la implementación mediante [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) como referencia. El proceso de configuración de [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) es similar, pero requiere una guía específica del administrador de Splunk Enterprise.

También debe tener los siguientes valores técnicos para configurar la extensión:

* Un [Token del recopilador de eventos](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Los tokens suelen tener formato UUIDv4 como el siguiente: `12345678-1234-1234-1234-1234567890AB`.
* La dirección y el puerto de la instancia de la plataforma Splunk para su organización. Una dirección de instancia de plataforma y un puerto suelen tener el siguiente formato: `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Los extremos de fragmento a los que se hace referencia en el reenvío de eventos solo deben utilizar puerto `443`. Actualmente, los puertos no estándar no son compatibles con las implementaciones de reenvío de eventos.

## Instalación de la extensión Splunk {#install}

Para instalar la extensión del recopilador de eventos de Splunk en la interfaz de usuario, vaya a **Reenvío de eventos** y seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez seleccionada o creada la propiedad deseada, vaya a **Extensiones** > **Catálogo**. Buscar &quot;[!DNL Splunk]&quot; y, a continuación, seleccione **[!DNL Install]** en la extensión de Splunk.

![Botón Instalar para la extensión Splunk que se está seleccionando en la interfaz de usuario](../../../images/extensions/splunk/install.png)

## Configurar la extensión Splunk {#configure_extension}

>[!IMPORTANT]
>
>Según las necesidades de implementación, es posible que tenga que crear un esquema, elementos de datos y un conjunto de datos antes de configurar la extensión. Revise todos los pasos de configuración antes de comenzar para determinar qué entidades debe configurar para su caso de uso.

Select **Extensiones** en el panel de navegación izquierdo. En **Installed**, seleccione **Configurar** en la extensión Splunk.

![Botón Configurar para la extensión Splunk que se está seleccionando en la interfaz de usuario](../../../images/extensions/splunk/configure.png)

Para **[!UICONTROL URL del recopilador de eventos HTTP]**, introduzca la dirección y el puerto de la instancia de la plataforma Splunk. En **[!UICONTROL Token de acceso]**, introduzca el [!DNL Event Collector Token] valor. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Opciones de configuración rellenadas en la interfaz de usuario](../../../images/extensions/splunk/input.png)

## Configuración de una regla de reenvío de eventos {#config_rule}

Comience a crear una nueva regla de reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al seleccionar las acciones para la regla, seleccione la variable [!UICONTROL Fragmento] y, a continuación, seleccione [!UICONTROL Crear evento] tipo de acción. Aparecen controles adicionales para configurar aún más el evento Splunk.

![Definir configuración de acción](../../../images/extensions/splunk/action-configurations.png)

El siguiente paso es asignar las propiedades del evento Splunk a los elementos de datos que haya creado anteriormente. A continuación se proporcionan las asignaciones opcionales compatibles basadas en los datos de evento de entrada que se pueden configurar. Consulte la [Documentación de Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) para obtener más información.

| Nombre del campo | Descripción |
| --- | --- |
| [!UICONTROL Evento ]<br><br>**(OBLIGATORIO)** | Indique cómo desea proporcionar los datos del evento. Los datos de evento se pueden asignar a la variable `event` dentro del objeto JSON en la solicitud HTTP, o puede ser texto sin procesar. La variable `event` se encuentra en el mismo nivel dentro del paquete de evento JSON que las claves de metadatos. Dentro de `event` llaves-valor clave, los datos pueden estar en cualquier forma que necesite (como una cadena, un número, otro objeto JSON, etc.). |
| [!UICONTROL Host] | El nombre de host del cliente desde el que se envían los datos. |
| [!UICONTROL Tipo de origen] | Tipo de origen que se asigna a los datos de evento. |
| [!UICONTROL Fuente] | El valor de origen que se asigna a los datos de evento. Por ejemplo, si está enviando datos desde una aplicación que está desarrollando, establezca esta clave en el nombre de la aplicación. |
| [!UICONTROL Índice] | Nombre del índice de los datos del evento. El índice que especifique aquí debe estar dentro de la lista de índices permitidos si el token tiene el parámetro de índices establecido. |
| [!UICONTROL Fecha] | La hora del evento. El formato de hora predeterminado es la hora UNIX (en formato `<sec>.<ms>`) y depende de la zona horaria local. Por ejemplo, `1433188255.500` indica 1433188255 segundos y 500 milisegundos después de epoch o lunes, 1 de junio de 2015, a las 7:50:55 PM GMT. |
| [!UICONTROL Campos] | Especifique un objeto JSON sin procesar o un conjunto de pares de clave-valor que contengan campos personalizados explícitos que se definirán en el momento del índice.  La variable `fields` key no se aplica a los datos sin procesar.<br><br>Solicitudes que contienen `fields` debe enviarse a `/collector/event` o no se indexarán. Para obtener más información, consulte la documentación de Splunk en [extracciones de campos indexados](http://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Validación de datos dentro de Splunk {#validate}

Después de crear y ejecutar la regla de reenvío de eventos, valide si el evento enviado a la API de Splunk se muestra como se espera en la interfaz de usuario de Splunk. Si la recopilación de eventos y la integración del Experience Platform se han realizado correctamente, verá eventos dentro de la consola de Splunk de esta manera:

![Los datos de evento que aparecen en la interfaz de usuario del Splunk durante la validación](../../../images/extensions/splunk/splunk-data.png)

## Pasos siguientes

Este documento trata sobre cómo instalar y configurar la extensión de reenvío de eventos Splunk en la interfaz de usuario. Para obtener más información sobre la recopilación de datos de eventos en Splunk, consulte la documentación oficial:

* [Configuración y uso del recopilador de eventos HTTP en el sitio web de Splunk ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Configuración de la autenticación con tokens](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Resolución de problemas del recopilador de eventos HTTP](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (también enumera un compendio de [posibles códigos de error](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
