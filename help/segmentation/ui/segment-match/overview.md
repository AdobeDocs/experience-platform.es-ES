---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Coincidencia de segmentos;coincidencia de segmentos
solution: Experience Platform
title: Resumen de coincidencia de segmentos
description: La coincidencia de segmentos es un servicio de uso compartido de segmentos en Adobe Experience Platform que permite a dos o más usuarios de Experience Platform intercambiar datos de segmentos de una manera segura, controlada y compatible con la privacidad.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: aa56c6bec3544c922521cc611036fd2989feb8b3
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 3%

---

# Información general de [!DNL Segment Match]

>[!IMPORTANT]
>
>Adobe introdujo [!DNL Segment Match] en 2021 para que los clientes colaboraran e intercambiaran audiencias. A principios de 2025, Adobe introdujo [Real-Time CDP Collaboration](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/home), el enfoque a largo plazo para cumplir con este caso de uso.
>
>* Para clientes de Estados Unidos, Canadá, Australia y Nueva Zelanda: Adobe recomienda a los clientes de Real-Time CDP Prime y Ultimate realizar la transición de los casos de uso de colaboración de datos de [!DNL Segment Match] a Real-Time CDP Collaboration. Consulta la [documentación](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/home) y la [guía de inicio rápido](https://experienceleague.adobe.com/es/docs/real-time-cdp-collaboration/using/quick-start-guide) para Real-Time CDP Collaboration y ponte en contacto con el equipo de tu cuenta de Adobe para obtener más información.
>* Para clientes de todas las demás regiones geográficas: [!DNL Segment Match] es la opción recomendada hasta que Real-Time CDP Collaboration se publique en esas regiones geográficas en 2026.

La coincidencia de segmentos de Adobe Experience Platform es un servicio de uso compartido de segmentos que permite a dos o más usuarios de Experience Platform intercambiar datos de segmentos de una manera segura, controlada y compatible con la privacidad. [!DNL Segment Match] usa estándares de privacidad de Experience Platform e identificadores personales como correos electrónicos con hash, números de teléfono con hash e identificadores de dispositivo como IDFA y GAID.

Con [!DNL Segment Match] puede:

* Administrar el proceso de superposición de identidades.
* Ver estimaciones previas al uso compartido.
* Aplique etiquetas de uso de datos para controlar si los datos se pueden compartir con los socios.
* Mantenga la administración del ciclo vital de la audiencia compartida después de publicar una fuente y continúe con un intercambio dinámico de datos mediante la capacidad de agregar, eliminar y dejar de compartir.

[!DNL Segment Match] utiliza un proceso de superposición de identidades para garantizar que el uso compartido de segmentos se realice de una manera segura y centrada en la privacidad. Una **identidad superpuesta** es una identidad que coincide tanto en el segmento como en el segmento de su socio seleccionado. Antes de compartir un segmento entre un remitente y un destinatario, el proceso de superposición de identidades comprueba si hay superposición en las áreas de nombres y comprueba el consentimiento entre el remitente y los destinatarios. Ambas comprobaciones de superposición deben pasar para que se comparta un segmento.

Las secciones siguientes proporcionan más información sobre [!DNL Segment Match], incluidos detalles sobre la configuración y su flujo de trabajo de extremo a extremo.

## Configuración

Las siguientes secciones describen cómo configurar [!DNL Segment Match]:

### Configurar datos de identidad y áreas de nombres {#namespaces}

El primer paso para comenzar con [!DNL Segment Match] es asegurarse de que está ingiriendo datos con las áreas de nombres de identidad admitidas.

Las áreas de nombres de identidad son un componente de [Adobe Experience Platform Identity Service](../../../identity-service/home.md). Cada identidad del cliente contiene un área de nombres asociada que indica el contexto de la identidad. Por ejemplo, un área de nombres puede distinguir un valor de &quot;name<span>@email.com&quot; como dirección de correo electrónico o &quot;443522&quot; como ID numérico de CRM.

Una identidad completa incluye un valor de ID y un área de nombres. Al hacer coincidir los datos de los registros en los fragmentos de perfil (como cuando [!DNL Real-Time Customer Profile] combina datos de perfil), tanto el valor de identidad como el área de nombres deben coincidir.

En el contexto de [!DNL Segment Match], las áreas de nombres se utilizan en el proceso de superposición al compartir datos.

La lista de áreas de nombres admitidas es la siguiente:

| Área de nombres | Descripción |
| --------- | ----------- |
| Correos electrónicos (SHA256, en minúsculas) | Un área de nombres para las direcciones de correo electrónico con hash previo. Los valores proporcionados en este área de nombres se convierten a minúsculas antes de crear valores hash con SHA256. Los espacios iniciales y finales deben recortarse antes de normalizar una dirección de correo electrónico. Esta configuración no se puede cambiar de forma retroactiva. Experience Platform ofrece dos métodos para admitir la función hash en la recopilación de datos, a través de [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=es#hashing-support) y a través de la [preparación de datos](../../../data-prep/functions.md#hashing). |
| Teléfono (SHA256_E.164) | Un espacio de nombres que representa los números de teléfono sin procesar que deben llevar un hash con los formatos SHA256 y E.164. |
| ECID | Un área de nombres que representa un valor de Experience Cloud ID (ECID). Este área de nombres también se puede mencionar mediante los siguientes alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulte la [descripción general de ECID](../../../identity-service/features/ecid.md) para obtener más información. |
| Apple IDFA (ID para anunciantes) | Área de nombres que representa el Apple ID para anunciantes. Consulte el siguiente documento sobre [anuncios basados en intereses](https://support.apple.com/en-us/HT202074) para obtener más información. |
| ID de Google Ad | Un área de nombres que representa un Google Advertising ID. Consulte el siguiente documento sobre [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) para obtener más información. |

### Configuración del consentimiento

Debe proporcionar una configuración de consentimiento y establecer su valor predeterminado en `opt-in` o `opt-out` para una comprobación de consentimiento.

La comprobación de consentimiento de inclusión y exclusión determina si puede operar con el consentimiento para compartir datos de usuario de forma predeterminada. Si la configuración de consentimiento predeterminada se establece en `opt-out`, los datos de usuario se pueden compartir, a menos que un usuario se excluya explícitamente. Si el valor predeterminado es `opt-in`, los datos de usuario no se podrán compartir, a menos que un usuario se incluya explícitamente.

La configuración de consentimiento predeterminada para [!DNL Segment Match] está establecida en `opt-out`. Para aplicar un modelo de inclusión a sus datos, envíe una solicitud por correo electrónico al equipo de la cuenta de Adobe.

Para obtener más información sobre el atributo `share` utilizado para establecer el valor del consentimiento para compartir datos, consulte la siguiente documentación sobre [grupo de campos de privacidad y consentimientos](../../../xdm/field-groups/profile/consents.md). Para obtener información sobre el grupo de campos específico que se usa para recopilar el consentimiento del consumidor para recopilar y usar datos relacionados con la privacidad, la personalización y las preferencias de marketing, consulte el siguiente [Ejemplo de consentimiento para preferencias de privacidad, Personalization y marketing en GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configuración de etiquetas de uso de datos

El último requisito previo que debe establecer es configurar una nueva etiqueta de uso de datos para evitar el uso compartido de datos. Mediante las etiquetas de uso de datos, puede administrar qué datos se pueden compartir a través de [!DNL Segment Match].

Las etiquetas de uso de datos le permiten categorizar conjuntos de datos y campos según las políticas de uso que se aplican a esos datos. Las etiquetas se pueden aplicar en cualquier momento, lo que proporciona flexibilidad en la forma en que se decide administrar los datos. Las prácticas recomendadas recomiendan el etiquetado de los datos en cuanto se incorporan a Experience Platform o en cuanto los datos están disponibles para su uso en Experience Platform.

[!DNL Segment Match] utiliza la etiqueta C11, una etiqueta de contrato específica de [!DNL Segment Match] que puede agregar manualmente a cualquier conjunto de datos o atributo para asegurarse de que se excluyen del proceso de uso compartido de socios de [!DNL Segment Match]. La etiqueta C11 indica datos que no deben usarse en [!DNL Segment Match] procesos. Después de determinar qué conjuntos de datos o campos desea excluir de [!DNL Segment Match] y agregar la etiqueta C11 en consecuencia, el flujo de trabajo [!DNL Segment Match] aplica automáticamente la etiqueta. [!DNL Segment Match] habilita automáticamente la directiva principal [!UICONTROL Restrict data sharing]. Para obtener instrucciones específicas sobre cómo aplicar etiquetas de uso de datos a los conjuntos de datos, consulte el tutorial sobre [administración de etiquetas de uso de datos en la interfaz de usuario](../../../data-governance/labels/user-guide.md).

Para obtener una lista de las etiquetas de uso de datos y sus definiciones, consulte el [glosario de etiquetas de uso de datos](../../../data-governance/labels/reference.md). Para obtener información acerca de las directivas de uso de datos, consulte la [descripción general de las directivas de uso de datos](../../../data-governance/policies/overview.md).

### Comprender los permisos de [!DNL Segment Match]

Hay dos permisos asociados con [!DNL Segment Match]:

| Permiso | Descripción |
| --- | --- |
| Administrar conexiones de Audience Share | Este permiso le permite completar el proceso de identificación del socio, que conecta dos organizaciones para habilitar [!DNL Segment Match] flujos. |
| Administrar recursos compartidos de audiencia | Este permiso le permite crear, editar y publicar fuentes (el paquete de datos utilizado para [!DNL Segment Match]) con socios activos (socios que han sido conectados por el usuario administrador con acceso de **[!UICONTROL Audience Share Connections]**). |

Consulte la [descripción general del control de acceso](../../../access-control/home.md) para obtener más información sobre el control de acceso y los permisos.

## [!DNL Segment Match] flujo de trabajo de extremo a extremo

Una vez que haya configurado los datos de identidad y las áreas de nombres, la configuración de consentimiento y la etiqueta de uso de datos, podrá empezar a trabajar con [!DNL Segment Match] y sus características.

### Administrar socio

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Segments]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Feeds]** en el encabezado superior.

![segment-feed.png](./images/segments-feed.png)

La página [!UICONTROL Feeds] contiene una lista de fuentes recibidas de socios, así como fuentes que ha compartido. Para ver una lista de socios existentes o establecer una conexión con un socio nuevo, seleccione **[!UICONTROL Manage partners]**.

![manage-partners.png](./images/manage-partners.png)

Una conexión entre dos socios es un &quot;protocolo de enlace bidireccional&quot; que actúa como un método de autoservicio para que los usuarios conecten sus organizaciones de Experience Platform a nivel de zona protegida. La conexión es necesaria para informar a Experience Platform de que se ha establecido un acuerdo y de que Experience Platform puede facilitar el uso compartido de servicios entre usted y sus socios.

>[!NOTE]
>
>El &quot;apretón de manos bidireccional&quot; entre usted y su pareja es estrictamente una conexión. No se intercambian datos durante este proceso.

Puede ver una lista de conexiones con socios existentes en la interfaz principal de la pantalla [!UICONTROL Manage partners]. En el carril derecho se encuentra el panel [!UICONTROL Share setting], que le ofrece la opción de generar un nuevo [!UICONTROL connect ID], así como un cuadro de entrada en el que puede introducir el [!UICONTROL connect ID] de un socio.

![establecer-conexión.png](./images/establish-connection.png)

Para crear un(a) nuevo(a) [!UICONTROL connect ID], seleccione **[!UICONTROL Regenerate]** en [!UICONTROL Share setting] y luego seleccione el icono de copiar junto al ID recién generado.

![share-setting.png](./images/share-setting.png)

Para conectar un socio usando su [!UICONTROL connect ID], ingrese su valor de identificador único en el cuadro de entrada debajo de [!UICONTROL Connect partner] y luego seleccione **[!UICONTROL Request]**.

![connect-partner.png](./images/connect-partner.png)

### Crear fuente   {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Casos de uso de marketing restringidos"
>abstract="Los casos de uso de marketing restringidos ayudan a proporcionar orientación a sus socios para garantizar que los segmentos compartidos se utilizan correctamente según las restricciones de gobernanza de datos."
>text="Learn more in documentation"

Una **fuente** es una agrupación de datos (segmentos), las reglas para exponer o utilizar esos datos y las configuraciones que determinan cómo se comparan los datos con los datos de sus socios. Una fuente se puede administrar de forma independiente e intercambiar con otros usuarios de Experience Platform mediante [!DNL Segment Match].

Para crear una fuente nueva, seleccione **[!UICONTROL Create feed]** en el panel [!UICONTROL Feeds].

![crear-fuente.png](./images/create-feed.png)

La configuración básica de una fuente incluye un nombre, una descripción y configuraciones con respecto a los casos de uso de marketing y la configuración de identidad. Proporcione un nombre y una descripción para la fuente y, a continuación, aplique los casos de uso de marketing de los que desea que se excluyan los datos. Puede seleccionar más de un caso de uso en una lista que incluya:

* [!UICONTROL Analytics]
* [!UICONTROL Combine with PII]
* [!UICONTROL Cross-site targeting]
* [!UICONTROL Data Science]
* [!UICONTROL Email targeting]
* [!UICONTROL Export to third party]
* [!UICONTROL Onsite advertising]
* [!UICONTROL Onsite personalization]
* [!UICONTROL Segment Match]
* [!UICONTROL Single identity personalization]

Finalmente, seleccione las áreas de nombres de identidad adecuadas para la fuente. Para obtener información sobre las áreas de nombres específicas admitidas por [!DNL Segment Match], vea la [tabla de áreas de nombres y datos de identidad](#namespaces). Cuando haya terminado, seleccione **[!UICONTROL Next]**.

![audience-sharing.png](./images/audience-sharing.png)

Una vez que haya establecido la configuración de la fuente, seleccione los segmentos que desee compartir en la lista de segmentos de origen. Puede seleccionar más de un segmento de la lista y puede utilizar el carril derecho para administrar la lista de segmentos seleccionados. Una vez finalizado, seleccione **[!UICONTROL Next]**.

![select-segments.png](./images/select-segments.png)

Aparecerá la página [!UICONTROL Share], que le proporcionará una interfaz para seleccionar los socios con los que desea compartir la fuente. Durante este paso, también puede ver el informe de estimaciones de superposición previo al uso compartido y el número de identidades superpuestas por área de nombres entre usted y su socio, el número de identidades superpuestas que tienen consentimiento para compartir datos.

Seleccione **[!UICONTROL Analyze by segment]** para ver el informe de estimaciones.

![analyze.png](./images/analyze.png)

El informe de estimaciones de superposición le permite administrar las comprobaciones de superposición y consentimiento por socio y por segmento antes de compartir la fuente.

| Métricas | Descripción |
| ------- | ----------- |
| Identidades estimadas con consentimiento | Número total de identidades superpuestas que cumplen los requisitos de consentimiento configurados para su organización. |
| Identidades superpuestas estimadas | El número de identidades que cumplen los requisitos para el segmento seleccionado y que también coinciden con el socio seleccionado. Estas identidades se muestran por área de nombres y no representan identidades de perfil individuales. Las estimaciones de superposición se basan en bocetos de perfil. |

Cuando haya terminado, seleccione **[!UICONTROL Close]**.

![informe-superposición.png](./images/overlap-report.png)

Una vez que haya seleccionado sus socios y visto su informe de estimaciones de superposición, seleccione **[!UICONTROL Next]** para continuar.

![compartir.png](./images/share.png)

Aparecerá el paso [!UICONTROL Review], que le permitirá revisar la nueva fuente antes de que se comparta y publique. Este paso incluye detalles sobre la configuración de identidad que aplicó, así como información sobre los casos de uso de marketing, los segmentos y los socios que seleccionó.

Seleccione **[!UICONTROL Finish]** para continuar.

![review.png](./images/review.png)

### Actualizar fuente

Para agregar o quitar segmentos, seleccione **[!UICONTROL Create feed]** de la página [!UICONTROL Feeds] y luego seleccione **[!UICONTROL Existing feed]**. En la lista de fuentes existentes que aparece, seleccione la fuente que desee actualizar y, a continuación, seleccione **[!UICONTROL Next]**.

![lista de fuentes](./images/feed-list.png)

Aparecerá la lista de segmentos. Desde aquí, puede añadir nuevos segmentos a la fuente y puede utilizar el carril derecho para eliminar los segmentos que ya no necesite. Una vez que haya terminado de administrar los segmentos en la fuente, seleccione **[!UICONTROL Next]** y, a continuación, siga los pasos descritos anteriormente para completar la fuente actualizada.

![actualización del estado](./images/update.png)

>[!NOTE]
>
>Cuando agrega o quita un segmento de una fuente compartida, el socio de recepción debe confirmar el cambio volviendo a habilitar la opción [!DNL Profile] en su lista de fuentes recibidas.

### Aceptar una fuente entrante

Para ver una fuente entrante, seleccione **[!UICONTROL Received]** en el encabezado de la página [!UICONTROL Feeds] y, a continuación, seleccione la fuente que desee ver en la lista. Para aceptar la fuente, seleccione **[!UICONTROL Enable for profile]** y deje pasar unos momentos para que el estado se actualice de [!UICONTROL Pending] a [!UICONTROL Enabled].

![recibido.png](./images/received.png)

Una vez que acepte una fuente compartida, puede empezar a utilizar los datos compartidos para generar nuevos segmentos.

## Próximos pasos

Al leer este documento, ha conseguido comprender [!DNL Segment Match], sus capacidades y su flujo de trabajo de extremo a extremo. Consulte los siguientes documentos para obtener más información acerca de otros servicios de Platform:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [Información general de [!DNL Real-Time Customer Profile]](../../../profile/home.md)
