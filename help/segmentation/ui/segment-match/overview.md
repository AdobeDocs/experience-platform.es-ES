---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Coincidencia de segmentos;coincidencia de segmentos
solution: Experience Platform
title: Resumen de coincidencia de segmentos
description: La coincidencia de segmentos es un servicio de uso compartido de segmentos en Adobe Experience Platform que permite a dos o más usuarios de Platform intercambiar datos de segmentos de una manera segura, controlada y compatible con la privacidad.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: b82bbdf7957e5a8d331d61f02293efdaf878971c
workflow-type: tm+mt
source-wordcount: '1968'
ht-degree: 2%

---

# Información general de [!DNL Segment Match]

La coincidencia de segmentos de Adobe Experience Platform es un servicio de uso compartido de segmentos que permite a dos o más usuarios de Platform intercambiar datos de segmentos de una manera segura, controlada y compatible con la privacidad. [!DNL Segment Match] utiliza estándares de privacidad de Platform e identificadores personales como correos electrónicos con hash, números de teléfono con hash e identificadores de dispositivo como IDFA y GAID.

Con [!DNL Segment Match] puede:

* Administrar el proceso de superposición de identidades.
* Ver estimaciones previas al uso compartido.
* Aplique etiquetas de uso de datos para controlar si los datos se pueden compartir con los socios.
* Mantenga la administración del ciclo vital de la audiencia compartida después de publicar una fuente y continúe con un intercambio dinámico de datos mediante la capacidad de agregar, eliminar y dejar de compartir.

[!DNL Segment Match] utiliza un proceso de superposición de identidad para garantizar que el uso compartido de segmentos se realice de forma segura y centrada en la privacidad. Un **identidad superpuesta** es una identidad que coincide tanto con el segmento de como con el segmento de su socio seleccionado. Antes de compartir un segmento entre un remitente y un destinatario, el proceso de superposición de identidades comprueba si hay superposición en las áreas de nombres y comprueba el consentimiento entre el remitente y los destinatarios. Ambas comprobaciones de superposición deben pasar para que se comparta un segmento.

Las secciones siguientes proporcionan más información sobre [!DNL Segment Match], incluidos detalles sobre la configuración y su flujo de trabajo completo.

## Configuración

En las siguientes secciones se describe cómo configurar [!DNL Segment Match]:

### Configurar datos de identidad y áreas de nombres {#namespaces}

El primer paso para empezar a usar [!DNL Segment Match] es para asegurarse de que está introduciendo datos en las áreas de nombres de identidad admitidas.

Las áreas de nombres de identidad son un componente de [Servicio de identidad de Adobe Experience Platform](../../../identity-service/home.md). Cada identidad del cliente contiene un área de nombres asociada que indica el contexto de la identidad. Por ejemplo, un área de nombres puede distinguir el valor &quot;name&quot;<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID numérico de CRM.

Una identidad completa incluye un valor de ID y un área de nombres. Al hacer coincidir datos de registro en fragmentos de perfil (como cuando [!DNL Real-Time Customer Profile] combina datos de perfil), tanto el valor de identidad como el área de nombres deben coincidir.

En el contexto de [!DNL Segment Match], las áreas de nombres se utilizan en el proceso de superposición al compartir datos.

La lista de áreas de nombres admitidas es la siguiente:

| Área de nombres | Descripción |
| --------- | ----------- |
| Correos electrónicos (SHA256, en minúsculas) | Un área de nombres para las direcciones de correo electrónico con hash previo. Los valores proporcionados en este área de nombres se convierten a minúsculas antes de crear valores hash con SHA256. Los espacios iniciales y finales deben recortarse antes de normalizar una dirección de correo electrónico. Esta configuración no se puede cambiar de forma retroactiva. Platform ofrece dos métodos para admitir el hashing en la recopilación de datos, a través de [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) y mediante [preparación de datos](../../../data-prep/functions.md#hashing). |
| Teléfono (SHA256_E.164) | Un espacio de nombres que representa los números de teléfono sin procesar que deben tener un cifrado hash con los formatos SHA256 y E.164. |
| ECID | Un área de nombres que representa un valor de ID de Experience Cloud (ECID). Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte la [Información general de ECID](../../../identity-service/features/ecid.md) para obtener más información. |
| Apple IDFA (ID para anunciantes) | Área de nombres que representa el Apple ID para anunciantes. Consulte el siguiente documento sobre [anuncios basados en intereses](https://support.apple.com/en-us/HT202074) para obtener más información. |
| ID de anuncio de Google | Un área de nombres que representa un ID de publicidad de Google. Consulte el siguiente documento sobre [ID de publicidad de Google](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obtener más información. |

### Configuración del consentimiento

Debe proporcionar una configuración de consentimiento y establecer su valor predeterminado en `opt-in` o `opt-out` para una comprobación de consentimiento.

La comprobación de consentimiento de inclusión y exclusión determina si puede operar con el consentimiento para compartir datos de usuario de forma predeterminada. Si la configuración de consentimiento predeterminada está establecida en `opt-out`A continuación, los datos de usuario se pueden compartir, a menos que un usuario se excluya explícitamente. Si el valor predeterminado es `opt-in`Por lo tanto, los datos de usuario no se pueden compartir, a menos que un usuario se adhiera explícitamente.

La configuración de consentimiento predeterminada para [!DNL Segment Match] se establece en `opt-out`. Para aplicar un modelo de inclusión a sus datos, envíe una solicitud por correo electrónico al equipo de la cuenta de Adobe.

Para obtener más información sobre `share` se utiliza para establecer el valor del consentimiento de uso compartido de datos, consulte la siguiente documentación sobre [grupo de campos privacidad y consentimientos](../../../xdm/field-groups/profile/consents.md). Para obtener información sobre el grupo de campos específico utilizado para recopilar el consentimiento del consumidor para la recopilación y el uso de datos relacionados con la privacidad, la personalización y las preferencias de marketing, consulte lo siguiente [Ejemplo de consentimiento para las preferencias de privacidad, personalización y marketing de GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configuración de etiquetas de uso de datos

El último requisito previo que debe establecer es configurar una nueva etiqueta de uso de datos para evitar el uso compartido de datos. Mediante las etiquetas de uso de datos, puede administrar qué datos se pueden compartir a través de [!DNL Segment Match].

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas alientan el etiquetado de datos en cuanto se incorporan en Experience Platform o en cuanto los datos están disponibles para su uso en Platform.

[!DNL Segment Match] utiliza la etiqueta C11, una etiqueta de contrato específica de [!DNL Segment Match] que puede agregar manualmente a cualquier conjunto de datos o atributo para asegurarse de que se excluyen del [!DNL Segment Match] proceso de uso compartido de socios. La etiqueta C11 indica datos que no deben utilizarse en [!DNL Segment Match] procesos. Después de determinar de qué conjuntos de datos o campos desea excluir [!DNL Segment Match] y agregó la etiqueta C11 en consecuencia, la etiqueta se aplica automáticamente por el [!DNL Segment Match] flujo de trabajo. [!DNL Segment Match] activa automáticamente la [!UICONTROL Restringir el uso compartido de datos] política básica. Para obtener instrucciones específicas sobre cómo aplicar etiquetas de uso de datos a conjuntos de datos, consulte el tutorial sobre [administración de etiquetas de uso de datos en la IU](../../../data-governance/labels/user-guide.md).

Para obtener una lista de las etiquetas de uso de datos y sus definiciones, consulte la [glosario de etiquetas de uso de datos](../../../data-governance/labels/reference.md). Para obtener información sobre las políticas de uso de datos, consulte la [información general sobre políticas de uso de datos](../../../data-governance/policies/overview.md).

### Comprensión [!DNL Segment Match] permissions

Existen dos permisos asociados a [!DNL Segment Match]:

| Permiso | Descripción |
| --- | --- |
| Administrar conexiones de Audience Share | Este permiso le permite completar el proceso de identificación entre socios, que conecta dos organizaciones para habilitar [!DNL Segment Match] flujos. |
| Administrar recursos compartidos de audiencia | Este permiso le permite crear, editar y publicar fuentes (el paquete de datos utilizado para [!DNL Segment Match]) con socios activos (socios conectados por el usuario administrador con **[!UICONTROL Conexiones de Audience Share]** access). |

Consulte la [información general de control de acceso](../../../access-control/home.md) para obtener más información sobre el control de acceso y los permisos.

## [!DNL Segment Match] flujo de trabajo de extremo a extremo

Una vez configurados los datos de identidad y las áreas de nombres, la configuración de consentimiento y la etiqueta de uso de datos, puede empezar a trabajar con [!DNL Segment Match] y sus características.

### Administrar socio

En la IU de Platform, seleccione **[!UICONTROL Segmentos]** en la barra de navegación izquierda y, a continuación, seleccione **[!UICONTROL Fuentes]** desde el encabezado superior.

![segments-feed.png](./images/segments-feed.png)

El [!UICONTROL Fuentes] Esta página contiene una lista de las fuentes recibidas de los socios, así como las fuentes que ha compartido. Para ver una lista de socios existentes o establecer una conexión con un socio nuevo, seleccione **[!UICONTROL Administrar socios]**.

![manage-partners.png](./images/manage-partners.png)

Una conexión entre dos socios es un &quot;protocolo de enlace bidireccional&quot; que actúa como un método de autoservicio para que los usuarios conecten sus organizaciones de Platform a nivel de zona protegida. La conexión es necesaria para informar a Platform de que se ha establecido un acuerdo y de que Platform puede facilitar el uso compartido de servicios entre usted y sus socios.

>[!NOTE]
>
>El &quot;apretón de manos bidireccional&quot; entre usted y su pareja es estrictamente una conexión. No se intercambian datos durante este proceso.

Puede ver una lista de conexiones con socios existentes en la interfaz principal de [!UICONTROL Administrar socios] pantalla. En el carril derecho se encuentra el [!UICONTROL Compartir configuración] , que le ofrece la opción de generar un nuevo [!UICONTROL identificador de conexión] así como un cuadro de entrada en el que puede introducir el nombre de un socio [!UICONTROL identificador de conexión].

![set-connection.png](./images/establish-connection.png)

Para crear un nuevo [!UICONTROL identificador de conexión], seleccione **[!UICONTROL Regenerar]** bajo [!UICONTROL Compartir configuración] y, a continuación, seleccione el icono de copiar junto al ID recién generado.

![share-setting.png](./images/share-setting.png)

Para conectar un socio con su [!UICONTROL identificador de conexión], introduzca su valor de ID único en el cuadro de entrada de [!UICONTROL Conectar socio] y luego seleccione **[!UICONTROL Solicitud]**.

![connect-partner.png](./images/connect-partner.png)

### Crear fuente   {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Casos de uso de marketing restringidos"
>abstract="Los casos de uso de marketing restringidos ayudan a proporcionar orientación a sus socios para garantizar que los segmentos compartidos se utilizan correctamente según las restricciones de gobernanza de datos."
>text="Learn more in documentation"

A **fuente** es una agrupación de datos (segmentos), las reglas para exponer o utilizar esos datos y las configuraciones que determinan cómo se comparan los datos con los datos de sus socios. Una fuente se puede administrar de forma independiente y se puede intercambiar con otros usuarios de Platform mediante [!DNL Segment Match].

Para crear una fuente nueva, seleccione **[!UICONTROL Crear fuente]** desde el [!UICONTROL Fuentes] panel.

![create-feed.png](./images/create-feed.png)

La configuración básica de una fuente incluye un nombre, una descripción y configuraciones con respecto a los casos de uso de marketing y la configuración de identidad. Proporcione un nombre y una descripción para la fuente y, a continuación, aplique los casos de uso de marketing de los que desea que se excluyan los datos. Puede seleccionar más de un caso de uso en una lista que incluya:

* [!UICONTROL Analytics]
* [!UICONTROL Combinar con PII]
* [!UICONTROL Segmentación entre sitios]
* [!UICONTROL Ciencia de datos]
* [!UICONTROL Segmentación por correo electrónico]
* [!UICONTROL Exportar a terceros]
* [!UICONTROL Publicidad in situ]
* [!UICONTROL Personalización in situ]
* [!UICONTROL Coincidencia de segmentos]
* [!UICONTROL Personalización de identidad única]

Finalmente, seleccione las áreas de nombres de identidad adecuadas para la fuente. Para obtener información sobre las áreas de nombres específicas admitidas por [!DNL Segment Match], consulte la [datos de identidad y tabla de áreas de nombres](#namespaces). Cuando haya terminado, seleccione **[!UICONTROL Siguiente]**.

![audience-sharing.png](./images/audience-sharing.png)

Una vez que haya establecido la configuración de la fuente, seleccione los segmentos que desee compartir en la lista de segmentos de origen. Puede seleccionar más de un segmento de la lista y puede utilizar el carril derecho para administrar la lista de segmentos seleccionados. Una vez finalizado, seleccione **[!UICONTROL Siguiente]**.

![select-segments.png](./images/select-segments.png)

El [!UICONTROL Compartir] , que le proporciona una interfaz para seleccionar los socios con los que desea compartir la fuente. Durante este paso, también puede ver el informe de estimaciones de superposición previo al uso compartido y el número de identidades superpuestas por área de nombres entre usted y su socio, el número de identidades superpuestas que tienen consentimiento para compartir datos.

Seleccionar **[!UICONTROL Analizar por segmento]** para ver el informe de estimaciones.

![analyze.png](./images/analyze.png)

El informe de estimaciones de superposición le permite administrar las comprobaciones de superposición y consentimiento por socio y por segmento antes de compartir la fuente.

| Métricas | Descripción |
| ------- | ----------- |
| Identidades estimadas con consentimiento | Número total de identidades superpuestas que cumplen los requisitos de consentimiento configurados para su organización. |
| Identidades superpuestas estimadas | El número de identidades que cumplen los requisitos para el segmento seleccionado y que también coinciden con el socio seleccionado. Estas identidades se muestran por área de nombres y no representan identidades de perfil individuales. Las estimaciones de superposición se basan en bocetos de perfil. |

Cuando haya terminado, seleccione **[!UICONTROL Cerrar]**.

![overlap-report.png](./images/overlap-report.png)

Una vez que haya seleccionado sus socios y haya visto el informe de estimaciones de superposición, seleccione **[!UICONTROL Siguiente]** para continuar.

![share.png](./images/share.png)

El [!UICONTROL Revisar] Este paso aparece, lo que le permite revisar la nueva fuente antes de compartirla y publicarla. Este paso incluye detalles sobre la configuración de identidad que aplicó, así como información sobre los casos de uso de marketing, los segmentos y los socios que seleccionó.

Seleccionar **[!UICONTROL Finalizar]** para continuar.

![review.png](./images/review.png)

### Actualizar fuente

Para añadir o quitar segmentos, seleccione **[!UICONTROL Crear fuente]** desde el [!UICONTROL Fuentes] y, a continuación, seleccione **[!UICONTROL Fuente existente]**. En la lista de fuentes existentes que aparece, seleccione la fuente que desee actualizar y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![feed-list](./images/feed-list.png)

Aparecerá la lista de segmentos. Desde aquí, puede añadir nuevos segmentos a la fuente y puede utilizar el carril derecho para eliminar los segmentos que ya no necesite. Cuando haya terminado de administrar los segmentos en la fuente, seleccione **[!UICONTROL Siguiente]** y luego siga los pasos descritos anteriormente para completar la fuente actualizada.

![actualización del estado](./images/update.png)

>[!NOTE]
>
>Al añadir o eliminar un segmento de una fuente compartida, el socio receptor debe confirmar el cambio volviendo a activar la variable [!DNL Profile] alternar en la lista de fuentes recibidas.

### Aceptar una fuente entrante

Para ver una fuente entrante, seleccione **[!UICONTROL Recibido]** desde el encabezado del [!UICONTROL Fuentes] y, a continuación, seleccione la fuente que desee ver en la lista. Para aceptar la fuente, seleccione **[!UICONTROL Habilitar para el perfil]** y espere unos momentos para que el estado se actualice desde [!UICONTROL Pendiente] hasta [!UICONTROL Habilitado].

![received.png](./images/received.png)

Una vez que acepte una fuente compartida, puede empezar a utilizar los datos compartidos para generar nuevos segmentos.

## Pasos siguientes

Al leer este documento, ha adquirido una comprensión de [!DNL Segment Match], sus capacidades y su flujo de trabajo completo. Consulte los siguientes documentos para obtener más información acerca de otros servicios de Platform:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [Información general de [!DNL Real-Time Customer Profile]](../../../profile/home.md)
