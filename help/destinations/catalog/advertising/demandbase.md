---
title: Conexión de Demandbase
description: Utilice este destino para activar los públicos de su cuenta para los casos de uso de Account-Based Marketing (ABM). Anuncie para personas y funciones relevantes en sus cuentas de destino a través de B2B Demand Side Platform (DSP) de DemandBase. Las cuentas de destino también se pueden enriquecer con datos de terceros de Demandbase para otros casos de uso posteriores en marketing y ventas.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 08c2c7f5080f0e6afb7be53aad9f88ba0fccf923
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 18%

---

# Conexión de Demandbase {#demandbase}

>[!AVAILABILITY]
>
>&#x200B;>La funcionalidad para activar audiencias de cuenta en el destino de Demandbase está disponible para compañías que compren las ediciones de [empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Active perfiles para sus campañas de Demandbase para la segmentación, personalización y supresión de audiencias, en función de [audiencias de la cuenta](/help/segmentation/types/account-audiences.md)

## Ejemplo de uso {#use-case}

Utilice este destino para activar los públicos de su cuenta para los casos de uso de Account-Based Marketing (ABM). Anuncie para personas y funciones relevantes en sus cuentas de destino a través de B2B Demand Side Platform (DSP) de DemandBase. Las cuentas de destino también se pueden enriquecer con datos de terceros de Demandbase para otros casos de uso posteriores en marketing y ventas.

Por ejemplo, aproveche la tecnología de publicidad de DSP de Demandbase para segmentar personas o funciones específicas dentro de cuentas clave para la generación de posibles clientes en la parte superior del canal o para crear y aumentar grupos de compra. Utilice el destino de Demandbase para explorar otros casos de uso y dirigir las cuentas de forma eficaz.

Con esta integración, también puede personalizar la experiencia del sitio web mediante la búsqueda de información de la cuenta en tiempo real para optimizar la participación.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipo de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas a través del [servicio de segmentación](../../../segmentation/home.md) de Experience Platform. |
| Cargas personalizadas | X | Las audiencias [importadas](../../../segmentation/ui/overview.md#import-audience) en Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-and-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
|--------------|-----------|---------------------------|
| Tipo de exportación | Exportación de audiencia | Todos los miembros de la audiencia se exportarán con identificadores clave como nombre, número de teléfono y más. |
| Frecuencia | Streaming | Conexiones basadas en API &quot;siempre activas&quot;. Las actualizaciones se envían de forma descendente inmediatamente después de los cambios de perfil. |

{style="table-layout:auto"}

## Requisitos previos {#prerequisites}

Para exportar audiencias de cuenta a Demandbase, necesita lo siguiente:

1. Una cuenta de Demandbase.
2. Un token de API de Demandbase. Puede generar un token de API con el usuario en Demandbase. Para generar un token, vaya a [Mi perfil > Token de API](https://web.demandbase.com/o/ad/at) después de iniciar sesión en su cuenta de Demandbase.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;para obtener acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

![Agregar token de portador](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Token de portador]**: complete el token de portador para autenticarse en el destino. Vea [requisitos previos](#prerequisites) para obtener información sobre cómo obtener el token.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Agregar información sobre la conexión de destino](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Tipo de entidad]**: seleccione **[!UICONTROL Cuenta]** como tipo de entidad.

Ahora está listo para activar sus audiencias en Demandbase.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}

Lea [Activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md) para obtener instrucciones sobre cómo activar audiencias de cuenta en este destino.

## Notas adicionales y llamadas importantes {#additional-notes}

* Si una audiencia de cuenta con el mismo nombre se activó anteriormente en Demandbase, no puede volver a activarla a través de un flujo de datos diferente al destino de Demandbase.
* Si ha exportado audiencias a Demandbase y las exportaciones se realizan correctamente en Experience Platform, pero no todos los datos llegan a Demandbase, es posible que haya encontrado una restricción de API en Demandbase. Póngase en contacto con ellos para obtener una aclaración.
