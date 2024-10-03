---
title: Uso Compartido De Paquetes Entre Organizaciones Mediante La Herramienta Sandbox
description: Aprenda a utilizar la herramienta de zona protegida en Adobe Experience Platform para compartir paquetes entre diferentes organizaciones.
badge: Beta
source-git-commit: 209aaaf0c2bfdb321f75257309980c7a48cb1eb4
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Uso compartido de paquetes entre organizaciones mediante la herramienta Sandbox

>[!NOTE]
>
>El uso compartido de paquetes entre organizaciones está actualmente en fase beta y solo está disponible para determinados clientes de la versión beta.

Mejore la precisión de la configuración en los entornos limitados y exporte e importe sin problemas las configuraciones de los entornos limitados entre distintas organizaciones con la función de herramientas de entornos limitados. Este documento explica cómo utilizar las herramientas de zona protegida en Adobe Experience Platform para compartir paquetes entre distintas organizaciones. Existen dos tipos de paquetes compartidos:

- **Paquete privado**

[Los paquetes privados](#private-packages) solo se pueden compartir con organizaciones que hayan aprobado la solicitud de uso compartido de la organización de origen a través de una lista de permitidos de inclusión.

- **Paquete público**

Hay [paquetes públicos](./sandbox-tooling.md/#export-and-import-an-entire-sandbox) disponibles para importar sin aprobación adicional. Estos paquetes se pueden compartir en el sitio web, el blog o la plataforma de un socio. La carga útil del paquete permite copiar y pegar paquetes de estos canales en la organización de destino.

## Paquetes privados {#private-packages}

>[!NOTE]
>
>Para iniciar y aprobar una solicitud de uso compartido y compartir paquetes entre organizaciones, necesitarás el permiso de control de acceso basado en roles **package-share**.

Utilice la función Herramienta de zona protegida para crear asociaciones, realizar un seguimiento de las estadísticas de solicitud de asociación, administrar las asociaciones existentes y compartir paquetes con organizaciones asociadas.

### Crear una solicitud de asociación de organización

Para crear una solicitud de asociación con una organización, vaya a la pestaña **[!UICONTROL Zonas protegidas]** **[!UICONTROL Organizaciones asociadas]**. A continuación, seleccione **[!UICONTROL Administrar organizaciones asociadas]**.

![Interfaz de usuario de zonas protegidas, con la ficha Organizaciones asociadas y Administrar organizaciones asociadas resaltadas.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

En el cuadro de diálogo [!UICONTROL Administración de socios de paquetes], escriba el identificador de organización en **[!UICONTROL Introducir identificador de organización]** y presione Intro. El identificador de organización se muestra en la sección **[!UICONTROL ID de organización seleccionados]** a continuación. Después de agregar los identificadores, selecciona **[!UICONTROL Confirmar]**.

>[!TIP]
>
>Se pueden introducir varios ID de organización a la vez mediante listas separadas por comas o introduciendo cada ID de organización seguido de &quot;entrar&quot;.

![Cuadro de diálogo de organizaciones asociadas al paquete con Introducir ID de organización, ID de organización seleccionados y Confirmar resaltado.](../images/ui/sandbox-tooling/private-enter-org-id.png)

La solicitud para compartir se ha enviado correctamente a la organización asociada y se le devolverá a la ficha [!UICONTROL Zonas protegidas] **[!UICONTROL Organizaciones asociadas]**, que muestra la **[!UICONTROL solicitud saliente]**.

![Ficha Organizaciones asociadas con la solicitud saliente resaltada.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autorizar una solicitud de asociación {#authorize-request}

Para autorizar una solicitud de asociación con una organización, vaya a la pestaña [!UICONTROL Zonas protegidas] **[!UICONTROL Organizaciones asociadas]**. A continuación, seleccione **[!UICONTROL Solicitud entrante]**.

![La interfaz de usuario de las zonas protegidas con la pestaña Organizaciones asociadas y la solicitud entrante resaltadas.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

El **[!UICONTROL estado]** actual de la solicitud, en este momento, es **Pendiente**. Para aprobar la solicitud, seleccione los puntos suspensivos (`...`) junto a la solicitud seleccionada y, a continuación, seleccione **[!UICONTROL Aprobar]** en el menú desplegable.

![Lista de solicitudes entrantes que muestra el menú desplegable con Aprobar resaltado.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

El cuadro de diálogo **[!UICONTROL Revisar solicitud de organización de socio]** muestra detalles sobre la solicitud de asociación de organización. Escriba un [!UICONTROL Motivo] para la aprobación y, a continuación, seleccione **[!UICONTROL Aprobar]**.

![Revisar el cuadro de diálogo de solicitud de organización asociada con el motivo y la aprobación resaltados.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Ha vuelto a la página [!UICONTROL Solicitud entrante] y el estado de la solicitud se ha actualizado a **[!UICONTROL Aprobada]**.

![Lista de solicitudes entrantes con el elemento Approved resaltado.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Utilice este flujo de trabajo/proceso para compartir paquetes entre su organización y la organización de origen.

### Uso compartido de paquetes con organizaciones asociadas {#share-package}

>[!NOTE]
>
>Solo se pueden compartir los paquetes con el estado **Publicado**.

Para compartir un paquete con una organización asociada aprobada, vaya a la pestaña [!UICONTROL Zonas protegidas] **[!UICONTROL Paquetes]**. A continuación, seleccione los puntos suspensivos (`...`) junto al paquete y, a continuación, seleccione **[!UICONTROL Compartir paquete]** en el menú desplegable.

![Lista de paquetes que muestra el menú desplegable con Compartir paquete resaltado.](../images/ui/sandbox-tooling/private-share-package.png)

En el cuadro de diálogo **[!UICONTROL Compartir paquete]**, seleccione el paquete que desea compartir en el menú desplegable **[!UICONTROL Compartir configuración]** y, a continuación, seleccione **[!UICONTROL Confirmar]**.

>[!TIP]
>
>Es posible seleccionar más de una organización. Las organizaciones seleccionadas aparecerán debajo del menú desplegable [!UICONTROL Compartir configuración].

![Cuadro de diálogo Compartir paquete con la configuración de Compartir y Confirmar resaltada.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

## Pasos siguientes {#next-steps}

Este documento muestra cómo utilizar la función de herramientas de espacio aislado para compartir paquetes entre diferentes organizaciones. Para obtener más información, consulte la [guía de herramientas de espacio aislado](../ui/sandbox-tooling.md).

Para obtener información sobre cómo realizar distintas operaciones con la API de espacio aislado, consulte la [guía para desarrolladores de espacios aislados](../api/getting-started.md). Para obtener información general de alto nivel sobre las zonas protegidas en Experience Platform, consulte la [documentación general](../home.md).
