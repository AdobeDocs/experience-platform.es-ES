---
keywords: Experience Platform;inicio;temas populares;exportar;Exportar
solution: Experience Platform
title: Administración de trabajos de privacidad en la IU de Privacy Service
description: Aprenda a utilizar la interfaz de usuario de Privacy Service para coordinar y supervisar las solicitudes de privacidad en varias aplicaciones de Experience Cloud.
exl-id: aa8b9f19-3e47-4679-9679-51add1ca2ad9
source-git-commit: 9d05752f3db78d9d10fd91fd0d3fed924217199c
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 14%

---

# Administración de trabajos de privacidad en la IU de Privacy Service {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_description"
>title="Cumplimiento de las solicitudes de privacidad de los interesados"
>abstract="<h2>Descripción</h2><p>Adobe Experience Platform Privacy Service le permite crear y administrar solicitudes de privacidad en nombre de clientes que desean acceder a sus datos personales o eliminarlos de acuerdo con las regulaciones de privacidad.</p>"

Este documento proporciona los pasos para crear y administrar solicitudes de privacidad mediante [!DNL Privacy Service] interfaz de usuario.

>[!IMPORTANT]
>
>El Privacy Service solo está diseñado para solicitudes de derechos de los interesados y consumidores. No se admite ni permite ningún otro uso de Privacy Service para la limpieza o el mantenimiento de datos. El Adobe tiene la obligación legal de cumplirlos en el momento oportuno. Como tal, no se permiten las pruebas de carga en el Privacy Service, ya que es un entorno de solo producción y crea un registro de solicitudes de privacidad válidas innecesarias.
>
>Ahora se establece un límite diario de carga estricto para ayudar a evitar el abuso del servicio. Si se detecta que algún usuario abusa del sistema, se deshabilitará el acceso al servicio. Luego se celebrará una reunión posterior con ellos para abordar sus acciones y discutir el uso aceptable de Privacy Service.

## Examine la [!DNL Privacy Service] Panel de IU

El tablero de [!DNL Privacy Service] La interfaz de usuario proporciona dos widgets que le permiten ver el estado de sus trabajos de privacidad:[!UICONTROL Informe de estado]&quot; y &quot;[!UICONTROL Solicitudes de trabajo]&quot;. El panel también muestra la regulación seleccionada actual para los trabajos mostrados.

![Panel de IU](../images/user-guide/dashboard.png)

### Tipo de regulación

[!DNL Privacy Service] admite solicitudes de trabajo para varias normas de privacidad. En la tabla siguiente se enumeran las regulaciones admitidas y su etiqueta correspondiente tal como se representa en la interfaz de usuario:

| Etiqueta de IU | Regulación |
| --- | --- |
| [!UICONTROL APA_AUS] | Las [!DNL Australia Privacy Act (Privacy Act)] |
| [!UICONTROL CPA] | Las [!DNL Colorado Privacy Act] |
| [!UICONTROL CCPA] | Las [!DNL California Consumer Privacy Act] |
| [!UICONTROL CPRA_USA] | Las [!DNL California Consumer Privacy Rights Act (CPRA)] |
| [!UICONTROL CTDPA] | Las [!DNL Connecticut Data Privacy Act] |
| [!UICONTROL RGPD] | La política de la Unión Europea [!DNL General Data Protection Regulation] |
| [!UICONTROL HIPAA_AUS] | Las [!DNL Health Insurance Portability and Accountability Act] |
| [!UICONTROL LGPD_BRA] | El de Brasil [!DNL Lei Geral de Proteção de Dados] |
| [!UICONTROL NZPA_NZL] | Nueva Zelanda [!DNL Privacy Act] |
| [!UICONTROL PDPA_THA] | El de Tailandia [!DNL Personal Data Protection Act] |
| [!UICONTROL UCPA] | Las [!DNL Utah Consumer Privacy Act] |
| [!UICONTROL VCDPA_USA] | Las [!DNL Virginia Consumer Data Protection Act] |

{style="table-layout:auto"}

<!--Not released yet:
| [!UICONTROL PDPA_VNM] | Vietnam's [!DNL Personal Data Protection Decree] |
 -->

>[!NOTE]
>
>Consulte la información general sobre [normas de privacidad compatibles](../regulations/overview.md) para obtener más información sobre el contexto jurídico de cada reglamento.

Los trabajos de cada tipo de regulación se rastrean por separado. Para cambiar entre tipos de regulación, seleccione **[!UICONTROL Tipo de regulación]** y seleccione la regulación que desee en la lista.

![La consola Privacy Service con la lista desplegable Tipo de regulación.](../images/user-guide/regulation.png)

Al cambiar el tipo de regulación, el panel se actualiza para mostrar todas las operaciones, filtros, widgets y cuadros de diálogo de creación de trabajos que se aplican a la regulación seleccionada.

![Panel actualizado](../images/user-guide/dashboard-update.png)

### Informe de estado

El gráfico de la izquierda del widget Informe de estado rastrea los trabajos enviados con cualquier trabajo que pueda haber informado con errores. El gráfico de la derecha rastrea los trabajos que se acercan al final del período de cumplimiento de 30 días.

Seleccione uno de los dos botones de alternancia situados encima del gráfico para mostrar u ocultar sus métricas respectivas.

![](../images/user-guide/hide-errors.png)

Para ver el número exacto de trabajos asociados a cualquier punto de datos en los gráficos, pase el ratón sobre el punto de datos en cuestión.

![Puntos de datos al pasar el ratón](../images/user-guide/mouse-over.png)

Para ver más detalles sobre un punto de datos determinado, seleccione el punto de datos en cuestión para mostrar los trabajos asociados en el widget Solicitudes de trabajo. Tome nota del filtro que se aplica justo encima de la lista de trabajos.

![Filtro aplicado desde el widget](../images/user-guide/apply-filter.png)

>[!NOTE]
>
>Cuando se ha aplicado un filtro al widget Solicitudes de trabajo, puede eliminar el filtro seleccionando la variable **X** en la píldora de filtro. Las solicitudes de trabajo vuelven a la lista de seguimiento predeterminada.

### Solicitudes de trabajo

El widget Solicitudes de trabajo enumera todas las solicitudes de trabajo disponibles en su organización, incluidos detalles como el tipo de solicitud, el estado actual, la fecha de vencimiento y el correo electrónico del solicitante.

>[!NOTE]
>
>Los datos de los trabajos creados anteriormente solo son accesibles durante 30 días después de la fecha de finalización.

Puede filtrar la lista escribiendo palabras clave en la barra de búsqueda debajo del título de las solicitudes de trabajo. La lista se filtra automáticamente a medida que escribe y muestra solicitudes que contienen valores que coinciden con los términos de búsqueda. También puede utilizar la variable **[!UICONTROL Solicitado el]** menú desplegable para seleccionar un intervalo de tiempo para los trabajos de la lista.

![Opciones de búsqueda de solicitud de trabajo](../images/user-guide/job-search.png)

Para ver los detalles de una solicitud de trabajo determinada, seleccione el ID de trabajo de la solicitud en la lista para abrir **[!UICONTROL Detalles del trabajo]** página.

![Detalles del trabajo de IU RGPD](../images/user-guide/job-details.png)

Este cuadro de diálogo contiene información de estado sobre cada [!DNL Experience Cloud] y su estado actual en relación con el trabajo general. Como cada trabajo de privacidad es asincrónico, la página muestra la última fecha y hora de comunicación (GMT) de cada solución, ya que algunos requieren más tiempo que otros para procesar la solicitud.

Si una solución ha proporcionado datos adicionales, se pueden ver en este cuadro de diálogo. Puede ver estos datos seleccionando filas de producto individuales.

Para descargar todos los datos de trabajo como archivo CSV, seleccione **[!UICONTROL Exportar a CSV]** en la parte superior derecha del cuadro de diálogo.

## Crear una nueva solicitud de trabajo de privacidad {#create-a-new-privacy-job-request}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_requests_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html?lang=es#logging-in-from-experience-platform">Solicitudes</a> en la navegación izquierda para abrir la lU de privacidad y, a continuación, <b>Crear solicitud</b>.</li><li>Desde aquí puede utilizar el generador de solicitudes o cargar un archivo JSON de interesados.</li><li>Si utiliza el generador de solicitudes, seleccione el tipo de trabajo (acceso o eliminación) y, a continuación, elija el tipo de identidad que va a proporcionar (correo electrónico, ECID o AAID), o introduzca un área de nombres de identidad personalizada. Introduzca los valores de identidad adecuados para los clientes y seleccione <b>Crear</b> cuando termine.</li><li>Si carga un archivo JSON, seleccione la flecha situada junto a Crear solicitud. En la lista de opciones, seleccione <b>Cargar JSON</b> y suba el archivo. Si no tiene un archivo JSON que cargar, seleccione <b>Descargar Adobe-GDPR-Request.json</b> para obtener una plantilla que puede rellenar. Cargue el JSON y seleccione <b>Crear</b> cuando termine.</li><li>Para obtener más ayuda sobre esta función, consulte la sección <a href="https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/user-guide.html?lang=es">Guía del usuario de Privacy Service</a> en Experience League.</li></ul>"

>[!NOTE]
>
>Para crear una solicitud de trabajo de privacidad, debe proporcionar información de identidad para los clientes específicos a los que se va a acceder o eliminar dichos datos. Revise el documento en [datos de identidad para solicitudes de privacidad](../identity-data.md) antes de continuar con esta sección.

El [!DNL Privacy Service] La interfaz de usuario proporciona dos métodos para crear nuevas solicitudes de trabajo:

* [Uso del Generador de solicitudes](#request-builder)
* [Cargar un archivo JSON](#json)

Los pasos para utilizar cada uno de estos métodos se describen en las secciones siguientes.

### Uso del Generador de solicitudes {#request-builder}

Con el Generador de solicitudes, puede crear manualmente una nueva solicitud de trabajo de privacidad en la interfaz de usuario. El Generador de solicitudes se utiliza mejor para conjuntos de solicitudes más simples y pequeños, ya que el Generador de solicitudes limita las solicitudes a tener solo tipo de ID por usuario. Para solicitudes más complicadas, puede ser mejor [cargar un archivo JSON](#json) en su lugar.

Para empezar a usar el Generador de solicitudes, seleccione **[!UICONTROL Crear solicitud]** debajo del widget Informe de estado, en el lado derecho de la pantalla.

![Seleccione Crear solicitud](../images/user-guide/create-request.png)

El **[!UICONTROL Crear solicitud]** se abre el cuadro de diálogo, que muestra las opciones disponibles para enviar una solicitud de trabajo de privacidad para el tipo de regulación seleccionado actualmente.

<img src="../images/user-guide/request-builder.png" width="500" /><br/>

Seleccione el **[!UICONTROL Tipo de trabajo]** de la solicitud (&quot;Eliminar&quot; o &quot;Acceder&quot;) y uno o más productos disponibles de la lista.

<img src="../images/user-guide/type-and-products.png" width="500" /><br/>

En **[!UICONTROL Tipo de área de nombres]**, seleccione el tipo de área de nombres adecuado para los ID de cliente que se envían a [!DNL Privacy Service].

<img src="../images/user-guide/namespace-type.png" width="500" /><br/>

Cuando utilice el tipo de área de nombres estándar, seleccione un área de nombres en el menú desplegable (correo electrónico, ECID o AAID) y, a continuación, escriba los valores de ID en el cuadro de texto de la derecha, pulsando **\&lt;enter>** para que cada ID lo añada a la lista.

<img src="../images/user-guide/standard-namespace.png" width="500" /><br/>

Cuando utilice el tipo de área de nombres personalizada, debe escribir manualmente el área de nombres antes de proporcionar los valores de ID siguientes.

<img src="../images/user-guide/custom-namespace.png" width="500" /><br/>

Cuando termine, seleccione **[!UICONTROL Crear]**.

<img src="../images/user-guide/request-builder-create.png" width="500" /><br/>

El cuadro de diálogo desaparece y los nuevos trabajos (o trabajos) se enumeran en el widget Solicitudes de trabajo junto con su estado de procesamiento actual.

### Cargar un archivo JSON {#json}

Al crear solicitudes más complejas, como las que utilizan varios tipos de ID para cada interesado que se procesa, puede crear una solicitud cargando un archivo JSON.

Seleccione la flecha situada junto a **[!UICONTROL Crear solicitud]**, debajo del widget Informe de estado en el lado derecho de la pantalla. En la lista de opciones que aparece, seleccione **[!UICONTROL Cargar JSON]**.

![Opciones de creación de solicitudes](../images/user-guide/create-options.png)

El **[!UICONTROL Cargar JSON]** , que proporciona una ventana para que arrastre y suelte el archivo JSON en.

<img src="../images/user-guide/upload-json.png" width="500" /><br/>

Si no tiene un archivo JSON para cargar, seleccione **[!UICONTROL Descargar Adobe-RGPD-Request.json]** para descargar una plantilla que puede rellenar según los valores que haya recopilado de sus interesados.


<img src="../images/user-guide/privacy-template.png" width="500" /><br/>


Busque el archivo JSON en el equipo y arrástrelo a la ventana de diálogo. Si la carga se realiza correctamente, el nombre del archivo aparecerá en el cuadro de diálogo. Puede continuar agregando más archivos JSON según sea necesario arrastrándolos y soltándolos en el cuadro de diálogo.

Cuando termine, seleccione **[!UICONTROL Crear]**. El cuadro de diálogo desaparece y los nuevos trabajos (o trabajos) se enumeran en el widget Solicitudes de trabajo junto con su estado de procesamiento actual.

### Pasos siguientes

Al leer este documento, ha aprendido a utilizar el [!DNL Privacy Service] IU para crear un trabajo de privacidad, ver los detalles de un trabajo y supervisar su estado de procesamiento, y descargar los resultados una vez que se haya completado.

Para obtener información sobre los pasos para realizar estas operaciones mediante programación usando [!DNL Privacy Service] API, consulte la [Guía de API](../api/overview.md).
