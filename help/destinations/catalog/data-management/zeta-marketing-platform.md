---
title: Plataforma de marketing de Zeta
description: Zeta Marketing Platform (ZMP) es un sistema basado en la nube que le ayuda a adquirir, crecer y retener clientes de forma más eficiente, impulsado por la inteligencia (datos propietarios e IA).
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Plataforma de marketing de Zeta {#zeta-marketing-platform}

## Información general {#overview}

Zeta Marketing Platform (ZMP) es un sistema basado en la nube que le ayuda a adquirir, crecer y retener clientes de forma más eficiente, impulsado por la inteligencia (datos propietarios e IA). Para obtener más información, consulte [Zeta Global](https://zetaglobal.com/).

Con el conector Zeta Marketing Platform disponible en Adobe Experience Platform, puede sincronizar fácilmente sus audiencias de Experience Platform a ZMP.

>[!IMPORTANT]
>
>El equipo *Zeta Global* crea y mantiene el conector de destino y la página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese con el equipo en [Contáctenos](https://zetaglobal.com/about/contact-us/).

## Casos de uso {#use-cases}

### Generar segmentos de audiencia {#use-case-build-audiences}

Un experto en marketing quiere crear perfiles de audiencia únicos, identificar sus segmentos más valiosos y utilizarlos en cualquier canal digital que admita Zeta Marketing Platform. Quieren crear una vista 360 real de un perfil de consumidor, crear y activar audiencias significativas. Se pueden encontrar más detalles sobre los canales compatibles con Zeta Marketing Platform [aquí](https://zetaglobal.com/platform/integrations/).

### Usuarios de Target con anuncios {#use-case-target-users}

Un anunciante tiene como objetivo dirigirse a usuarios dentro de audiencias específicas a través del Demand Side Platform Zeta (en inglés, Zeta DSP), ya que estos usuarios interactúan con sus marcas. DSP Para obtener más información sobre la Zeta, haga clic en [aquí](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## Requisitos previos {#prerequisites}

### Requisitos previos de Zeta Marketing Platform

* Antes de configurar una nueva conexión al destino de Zeta Marketing Platform, debe crear una lista de clientes vacía en su cuenta de Zeta Marketing Platform. Debe elegir una de estas listas de clientes como destino designado para recibir la audiencia de Adobe Experience Platform que desea enviar. Puede crear una lista de clientes vacía en el ZMP siguiendo las instrucciones [aquí](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Aunque Adobe Experience Platform permite la activación de varias audiencias a una instancia de destino ZMP concreta, es obligatorio que cada instancia de destino ZMP reciba solo una audiencia de Experience Platform. Para gestionar varias audiencias del Experience Platform, cree instancias de destino ZMP adicionales para cada audiencia y seleccione una lista de clientes diferente en el menú desplegable. Este método garantiza que las audiencias ZMP de destino no se sobrescriban. Consulte [Rellenar detalles de destino](#destination-details) para obtener más detalles.
* Utilice las siguientes credenciales para configurar el destino:
   * Nombre de usuario: **api**
   * Contraseña: su clave de API de REST de ZMP. Para encontrar la clave de API de REST, inicia sesión en tu cuenta ZMP y navega a la sección **Configuración** > **Integraciones** > **Claves y aplicaciones**. Consulte la [documentación de ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) para obtener más información.

## Identidades admitidas {#supported-identities}

[!DNL Zeta Marketing Platform] admite la activación de los identificadores de usuario personalizados que se describen en la tabla siguiente. Para obtener más información, consulte [identidades](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> El destino de Zeta Marketing Platform requiere que asigne un área de nombres de identidad de origen a la identidad de destino ZMP `uid`. Esto ayuda a la plataforma de marketing Zeta a diferenciar cada perfil de forma exclusiva.

| Identidad de destino | Descripción | Consideraciones | Notas |
---------|----------|----------|----------|
| uid | ID único que ZMP utiliza para diferenciar los perfiles de cliente | Obligatorio | Elija el área de nombres de identidad estándar `Email` si desea identificar perfiles únicos mediante sus direcciones de correo electrónico. También puede optar por asignar su área de nombres personalizada a `uid` si los perfiles de los clientes no tienen un correo electrónico. |
| email_md5_id | Correo electrónico MD5 que representa cada perfil de cliente | Opcional | Elija esta identidad de destino cuando pretenda identificar perfiles de clientes de forma exclusiva mediante valores MD5 de correo electrónico. Es esencial que las direcciones de correo electrónico ya estén en formato MD5 dentro del Experience Platform, ya que Platform no convierte el texto sin formato a MD5. En este escenario, establezca `uid` (obligatorio) en los mismos valores MD5 de correo electrónico u otra área de nombres de identidad adecuada. |

{style="table-layout:auto"}

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/audience-portal.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

>[!NOTE]
> A medida que se agregan o eliminan miembros individuales de la audiencia de Platform, se enviarán actualizaciones al ZMP para garantizar que la lista de clientes de destino se sincronice en consecuencia.

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform según la evaluación de segmentos, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL permiso Administrar destinos]** [control de acceso](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

* **[!UICONTROL Nombre de usuario]**: `api`
* **[!UICONTROL Contraseña]**: Su clave de API REST de ZMP. Para encontrar la clave de API de REST, inicia sesión en tu cuenta ZMP y navega a la sección **Configuración** > **Integraciones** > **Claves y aplicaciones**. Consulte la [documentación de ZMP](https://knowledgebase.zetaglobal.com/zmp/integrations) para obtener más información.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Imagen que muestra la configuración de ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Id. de sitio de cuenta ZMP]**: Su **Id. de sitio** ZMP al que desea enviar sus audiencias. Para ver el identificador del sitio, ve a la sección **Configuración** > **Integraciones** > **Claves y aplicaciones**. Encontrará más información [aquí](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL Segmento ZMP]**: El segmento de lista de clientes de su cuenta de ID de sitio ZMP que desea actualizar con la audiencia de Platform.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, consulte la guía sobre [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando termine de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar perfiles y segmentos en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md) para obtener instrucciones sobre cómo activar segmentos de audiencia en este destino.

### Asignar atributos e identidades {#map}

A continuación se muestra un ejemplo de asignación de identidad correcta al exportar perfiles a [!DNL Zeta Marketing Platform].

Selección de campos de origen:
* Seleccione un área de nombres de identidad de origen (personalizada o estándar, como `Email`) que identifique de forma exclusiva un perfil en Adobe Experience Platform y [!DNL Zeta Marketing Platform].
* Seleccione cualquier atributo de perfil de origen XDM al que deba exportarse y actualizarse en [!DNL Zeta Marketing Platform].

Selección de campos de destino:
* (Obligatorio) Seleccione `uid` como la identidad de destino a la que asigna un área de nombres de identidad de origen.
* (Opcional) Seleccione `email_md5_id` como la identidad de destino a la que asignó el área de nombres de identidad de origen que representa los valores md5 de correo electrónico. Es esencial que las direcciones de correo electrónico ya estén en formato MD5 dentro del Experience Platform, ya que Platform no convierte el texto sin formato a MD5
* Seleccione cualquier asignación de destino adicional si es necesario.

![Asignación de identidad](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## Datos exportados / Validar exportación de datos {#exported-data}

Una activación de audiencia exitosa de Experience Platform a Zeta Marketing Platform actualiza la lista de clientes objetivo en el ZMP. El recuento y los perfiles de muestra en la lista de clientes objetivo serán iguales al número de identidades activadas correctamente.

![Lista de clientes en ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Cada miembro de la audiencia que se activó desde el Experience Platform también será visible en **Audiencias** > **Personas** en el ZMP. También podrá ver el segmento **Lista de clientes** al que pertenece un perfil en la vista Cliente único, como se muestra a continuación.

![SingleCustomerViewInZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

* [Base de conocimiento Zeta](https://knowledgebase.zetaglobal.com/zmp/)
