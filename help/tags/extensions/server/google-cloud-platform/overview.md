---
title: Extensión de reenvío de eventos de Google Cloud Platform
description: Esta extensión de reenvío de eventos de Adobe Experience Platform envía eventos de Adobe Experience Edge Network a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: d1a34a98efd24a20dc53544eeb0d79490aaf31e7
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# [!DNL Google Cloud Platform] extensión de reenvío de eventos

[[!DNL Google Cloud Platform]](https://cloud.google.com/) es una plataforma de computación en la nube que ofrece una amplia variedad de servicios, como computación distribuida, almacenamiento de bases de datos, entrega de contenido y servicios de integración de software como servicio (SaaS) para la administración de la relación con los clientes (CRM) y la planificación de recursos empresariales (ERP).

El [!DNL Google Cloud Platform] [reenvío de eventos](../../../ui/event-forwarding/overview.md) la extensión aprovecha [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) para enviar eventos desde Adobe Experience Platform Edge Network a [!DNL Google Cloud Platform] para un procesamiento posterior. Esta guía explica cómo instalar la extensión y utilizar sus funcionalidades en una regla de reenvío de eventos.

## Requisitos previos

Para utilizar esta extensión, debe tener un [!DNL Google Cloud Platform] cuenta con un existente [!DNL Cloud Pub/Sub] tema. Si no tiene un flujo de datos preexistente, consulte la [!DNL AWS] documentación sobre [crear un nuevo flujo de datos utilizando [!DNL AWS] Consola de administración](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

### Creación de un secreto y un elemento de datos

En primer lugar, cree un nuevo `Google OAuth 2` [secreto de reenvío de eventos](../../../ui/event-forwarding/secrets.md), que se utilizará para autenticar la conexión con su cuenta al tiempo que mantiene el valor seguro.

Siguiente, [creación de un elemento de datos](../../../ui/managing-resources/data-elements.md#create-a-data-element) uso del **[!UICONTROL Núcleo]** extensión y a **[!UICONTROL Secreto]** tipo de elemento de datos para hacer referencia a `Google OAuth 2` secreto que acaba de crear.

## Instalación y configuración de [!DNL Google Cloud Platform] extensión {#install}

Para instalar la extensión de, [crear una propiedad de reenvío de eventos](../../../ui/event-forwarding/overview.md#properties) o elija una propiedad existente para editar en su lugar.

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo. En el **[!UICONTROL Catálogo]** pestaña, seleccione **[!UICONTROL Instalar]** en la tarjeta de [!DNL Google Cloud Platform] extensión.

![El catálogo [!DNL Google Cloud Platform] instalación de resalte de extensión.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

En la pantalla de configuración de, introduzca el secreto del elemento de datos que creó anteriormente en la **[!UICONTROL Token de acceso]** field. El secreto del elemento de datos contendrá su [!DNL Google Cloud Platform] Token de OAuth 2. Seleccione **[!UICONTROL Guardar]** cuando haya terminado.

![El [!DNL Google Cloud Platform] página de configuración de la extensión.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Crear un [!DNL Send Data to Cloud Pub/Sub] regla {#tracking-rule}

Una vez instalada la extensión de, cree un nuevo reenvío de eventos [regla](../../../ui/managing-resources/rules.md) y configure sus condiciones como desee. Al configurar las acciones de la regla, seleccione **[!UICONTROL Google Cloud Platform]** extensión y seleccione **[!UICONTROL Enviar datos a Cloud Pub/Sub]** para el tipo de acción.

![La vista de configuración de acción para [!UICONTROL Google Cloud Platform], con la acción resaltada y [!UICONTROL Enviar datos a Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrada | Descripción |
| --- | --- |
| [!UICONTROL Tema] | Tema que recibirá los eventos del reenvío de eventos. El valor debe tener el formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Datos] | Este campo contiene los datos que se van a reenviar a [!DNL Cloud Pub/Sub] tema en formato JSON.<br><br>En el **[!UICONTROL Raw]** , puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono de elemento de datos (![Icono de conjunto de datos](../../../images/extensions/server/aws/data-element-icon.png)) para seleccionar de una lista de elementos de datos existentes para representar los datos.<br><br>También puede utilizar la variable **[!UICONTROL Editor de pares de clave-valor JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |
| [!UICONTROL Atributos] | Este campo contiene el objeto JSON con atributos adicionales que se envían junto con el mensaje.<br><br>En el **[!UICONTROL Raw]** , puede pegar el objeto JSON directamente en el campo de texto proporcionado o puede seleccionar el icono de elemento de datos (![Icono de conjunto de datos](../../../images/extensions/server/aws/data-element-icon.png)) para seleccionar de una lista de elementos de datos existentes para representar los datos.<br><br>También puede utilizar la variable **[!UICONTROL Editor de pares de clave-valor JSON]** para agregar manualmente cada par clave-valor a través de un editor de interfaz de usuario. Cada valor se puede representar mediante una entrada sin procesar o se puede seleccionar un elemento de datos en su lugar. |

{style="table-layout:auto"}

## Pasos siguientes

Esta guía explica cómo enviar datos a [!DNL Cloud Pub/Sub] uso del [!DNL Google Cloud Platform] extensión de reenvío de eventos. Para obtener más información sobre las funcionalidades de reenvío de eventos en Experience Platform, consulte la [resumen del reenvío de eventos](../../../ui/event-forwarding/overview.md).