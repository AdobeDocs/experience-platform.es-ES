---
title: Conexión de Bombora
description: Active perfiles para sus campañas Bombora para la segmentación, personalización y supresión de audiencias, en función de las audiencias de la cuenta.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es#rtcdp-editions newtab=true"
source-git-commit: 026d8e4c2bcea407d2a750e66b11766b1114b758
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 3%

---


# Conexión de Bombora {#bombora}

>[!AVAILABILITY]
>
>La funcionalidad para activar audiencias de cuenta en el destino Bombora está disponible para compañías que compren las ediciones [De empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [De empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Active perfiles para sus campañas Bombora para la segmentación, personalización y supresión de audiencias, según [audiencias de la cuenta](/help/segmentation/types/account-audiences.md).

## Casos de uso {#use-case}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino Bombora, aquí tiene algunos casos de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

### Integración de DSP {#dsp-integration}

Como experto en marketing B2B, puede crear una lista de cuentas en Real-Time CDP que identifique las empresas que muestran una alta intención con sus productos y, a continuación, utilizar este destino para activar esta lista en Bombora.

A través de la integración de Bombora con DSPs puede ejecutar campañas de publicidad dirigidas usando datos de Bombora. Esto garantiza que el gasto en publicidad se centre en las empresas que tienen más probabilidades de realizar una conversión.

### Account-Based Marketing {#abm}

Como experto en marketing B2B, puede crear una lista de cuentas basada en las señales de marketing y CRM. Luego, puede usar este destino para activar esta lista en Bombora, donde los controles con conocimiento de ABM le ayudan a dirigir a los tomadores de decisiones en estas compañías.

### Activación de marketing multicanal basada en cuentas {#multi-channel-abm}

Como experto en marketing B2B, puede crear una lista de cuentas en Real-Time CDP que identifique compañías con alta intención. A continuación, puede utilizar este destino para activar la lista en Bombora y ejecutar campañas dirigidas en varios canales.

En medios sociales de pago, podría publicar anuncios personalizados para profesionales de cuentas de Target en plataformas como [!DNL LinkedIn] y [!DNL Facebook]. Con las plataformas de publicidad nativas, puede asegurarse de que el contenido llegue a los responsables de la toma de decisiones relevantes.

También puede ampliar las campañas a TV avanzada y enviar anuncios a cuentas clave.

Este enfoque multicanal garantiza una mensajería coherente entre plataformas, maximizando las tasas de participación y conversión.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/overview.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Identidades admitidas {#supported-identities}

Bombora requiere el mapeo de la identidad objetivo descrita en la tabla a continuación. Más información sobre [identidades](/help/identity-service/features/namespaces.md).

| Identidad de destino | Descripción |
|---|---|
| `primaryId` | Bombora requiere el mapeo de esta identidad objetivo para que la integración funcione correctamente. Puede asignar cualquier campo de origen a esta identidad. Esta asignación es obligatoria, pero no exporta datos a Bombora. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Está exportando todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en el destino [!DNL Bombora]. |
| Frecuencia de exportación | **[!UICONTROL Transmisión]** | Los destinos de streaming son conexiones basadas en API &quot;siempre activadas&quot;. Tan pronto como se actualiza un perfil en Experience Platform basado en la evaluación de audiencias, el conector envía la actualización de forma descendente a la plataforma de destino. Más información sobre [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para exportar audiencias de cuenta a Bombora, necesita la siguiente información.

1. Una cuenta de Bombora.
2. Un **[!UICONTROL ID de cliente]** y **[!UICONTROL secreto de cliente]** de Bombora.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;para obtener acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Agregar token de portador](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL ID de cliente]**: escriba su ID de cliente [!DNL Bombora].
* **[!UICONTROL Secreto de cliente]**: escriba el secreto de cliente [!DNL Bombora].

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Agregar información sobre la conexión de destino](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.

Ahora está listo para activar sus audiencias en Bombora.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md) para obtener instrucciones sobre cómo activar audiencias de cuenta en este destino.

### Asignaciones obligatorias {#mapping}

El destino Bombora requiere que configure las siguientes asignaciones para que la activación de datos se realice correctamente.



| Campo de origen | Campo de destino | Descripción |
|---------|----------|---------|
| Cualquier valor | `Identity: primaryId` | Esta asignación es obligatoria para que Experience Platform establezca una conexión con Bombora. Este valor no se exporta a Bombora, pero es necesario para la configuración de destino. Puede seleccionar cualquier atributo para el campo de origen. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora utiliza direcciones de sitios web o dominios para crear una lista de cuentas. |

![Agregar asignaciones obligatorias](../..//assets/catalog/advertising/bombora/mappings.png)


## Notas adicionales y llamadas importantes {#additional-notes}

Si una audiencia de cuenta con el mismo nombre se activó anteriormente en Bombora, recibirá un error si intenta activarla de nuevo a través de un flujo de datos diferente al destino de Bombora.

