---
title: (Empresas) LinkedIn conexión
description: Utilice este destino para activar los públicos de su cuenta para los casos de uso de Account-Based Marketing (ABM). Active perfiles para sus campañas de LinkedIn para la segmentación, personalización y supresión de audiencias, en función de los correos electrónicos con hash.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edición B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 6%

---

# (Compañías) Conexión de audiencias de LinkedIn Match {#companies-linkedin}

>[!AVAILABILITY]
>
>La funcionalidad para activar audiencias de cuenta en el destino de LinkedIn (Compañías) está disponible para compañías que compran las ediciones de Real-Time Customer Data Platform [De empresa a empresa](/help/rtcdp/overview.md#rtcdp-b2b) y [De empresa a persona](/help/rtcdp/overview.md#rtcdp-b2p).

Use este destino para activar las [audiencias de la cuenta](/help/segmentation/types/account-audiences.md) para los casos de uso de Account-Based Marketing (ABM). Anuncie a personalidades y roles relevantes en sus cuentas de destinatario a través del destino de empresa a empresa **[!UICONTROL (Compañías) LinkedIn]**. Visite la documentación de LinkedIn para [obtener más información acerca de la segmentación de cuentas](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) en la plataforma de LinkedIn.

>[!TIP]
>
>Para casos de uso a nivel individual (o de empresa a consumidor), Adobe recomienda usar el destino [Audiencia coincidente de LinkedIn](/help/destinations/catalog/social/linkedin.md).

![El destino de la cuenta de LinkedIn se muestra en la interfaz de usuario de Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

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

Asegúrese de cumplir los requisitos previos siguientes para exportar audiencias de cuenta a LinkedIn:

### Requisitos previos de cuenta de LinkedIn {#LinkedIn-account-prerequisites}

Antes de poder usar el destino [!UICONTROL (Compañías) LinkedIn Matched Audience], asegúrese de que su cuenta de [!DNL LinkedIn Campaign Manager] tenga el nivel de permiso de [!DNL Creative Manager] o superior.

Para obtener información sobre cómo editar los permisos de usuario de [!DNL LinkedIn Campaign Manager], consulte [Agregar, editar y quitar permisos de usuario en cuentas de Advertising](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de Ver destinos&rbrack;** y **[!UICONTROL Administrar destinos]**&lbrack;para obtener acceso. Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en el [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

1. Busque el destino [!DNL (Companies) LinkedIn Matched Audiences] en el catálogo de destino y seleccione **[!UICONTROL Configurar]**.
2. Seleccione **[!UICONTROL Conectar con destino]**.
   ![Autenticar con LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Escriba sus credenciales de LinkedIn y seleccione **Iniciar sesión**.

Después de completar el proceso de inicio de sesión con LinkedIn, puede continuar con el paso siguiente.

### Rellenar detalles de destino {#destination-details}

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Id. de cuenta]**: Su [!DNL LinkedIn Campaign Manager Account ID]. Puede encontrar este identificador en su cuenta de [!DNL LinkedIn Campaign Manager].

Ya está listo para activar audiencias de cuenta en LinkedIn.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**&#x200B;[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[[!UICONTROL permiso de control de acceso]](/help/access-control/home.md#permissions) de&rbrack;** Ver gráfico de identidad&lbrack;. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos."){width="100" zoomable="yes"}

Lea [Activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md) para obtener instrucciones sobre cómo activar audiencias de cuenta en este destino.

## Pares de asignación requeridos en el paso de asignación al activar audiencias de cuenta en el destino **[!UICONTROL (Compañías) audiencias coincidentes de LinkedIn]** {#required-mappings}

Al activar audiencias de cuenta en el destino **[!UICONTROL (Empresas) de audiencias coincidentes de LinkedIn]**, tenga en cuenta que los dos pares de asignación siguientes son obligatorios para exportar datos correctamente:

![Campos obligatorios de asignación de LinkedIn.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Campo de origen | Campo de destino |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (seleccione este campo en la vista **[!UICONTROL Seleccionar área de nombres de identidad]** al seleccionar el **[!UICONTROL Campo de destino]**). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar las audiencias de cuenta en los destinos."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Datos exportados {#exported-data}

Una activación correcta significa que se crea una audiencia personalizada de [!DNL LinkedIn] mediante programación en [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). La pertenencia a audiencias se ajusta a medida que los usuarios se califican o descalifican para las audiencias activadas.
