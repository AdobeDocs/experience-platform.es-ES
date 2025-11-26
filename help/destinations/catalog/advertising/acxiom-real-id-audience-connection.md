---
title: Conexión de audiencia de Acxiom Real ID
description: Use el destino  [!DNL Acxiom Real ID Audience Connection] para mejorar audiencias con la tecnología [!DNL Acxiom's Real ID] y activar audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más.
badge: label="Beta" type="Informative"
exl-id: 5f1f0f7f-ac46-42bd-8002-be50fab5a76b
source-git-commit: fda542e62c448788099d63951277278a146fdfc8
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 6%

---

# Destino [!DNL Acxiom Real ID Audience Connection]

>[!NOTE]
>
>El destino [!DNL Acxiom Real ID Audience Connection] se encuentra en la versión beta. El equipo [!DNL Acxiom] crea y mantiene este conector de destino y esta página de documentación. Para cualquier consulta o solicitud de actualización, comuníquese directamente con Acxiom [aquí](mailto:acxiom-adobe-help@acxiom.com).

Use el destino [!DNL Acxiom Real ID Audience Connection] para mejorar las audiencias con la tecnología [Real ID](https://www.acxiom.com/real-id/real-id/) de [!DNL Acxiom's] y activar audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más.

Este tutorial proporciona instrucciones para crear un conector de destino [!DNL Acxiom Real ID Audience Connection] mediante la interfaz de usuario [!DNL Adobe Experience Platform]. Este conector se utiliza para crear y distribuir audiencias a destinos seleccionados.

## Casos de uso {#use-cases}

Este conector admite clientes que tienen Acxiom Real Identity cargado en Real-Time CDP como identificador. Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL Acxiom Real ID Audience Connection], aquí tiene un ejemplo de caso de uso que los clientes de [!DNL Adobe Experience Platform] pueden resolver mediante este conector.

### Envío de audiencias de Experience Platform a su cuenta de Acxiom {#send-audiences}

Utilice este conector de destino si es un profesional de marketing que desea enviar audiencias de [!DNL Experience Platform] a su cuenta de [!DNL Acxiom] para una adquisición entre canales.

Por ejemplo, el departamento Operaciones de marketing de una marca de servicios financieros globales está interesado en la adquisición de clientes en canales múltiples a través de varias plataformas publicitarias. Pueden usar el conector de destino [!DNL Acxiom Real ID Audience Connection] para enviar audiencias de [!DNL Experience Platform] a [!DNL Acxiom], mejorar las audiencias con la tecnología [!DNL Acxiom's Real ID] y activar las audiencias en varias plataformas, como [!DNL Altice], [!DNL Ampersand], [!DNL Comcast] y más.


## Requisitos previos {#prerequisites}

* **Confirmar condiciones de uso:** Para poder configurar un nuevo destino de [!DNL Acxiom Real ID Audience Connection], debe leer y firmar el Contrato de condiciones de uso de [!DNL Acxiom's]. Recibirá el vínculo al acuerdo una vez que se haya completado el pedido de ventas ejecutado. Hasta que no firme el acuerdo, no verá la tarjeta de destino [!DNL Acxiom Real ID Audience Connection] en el catálogo de destino de Experience Platform. Después de aceptar y firmar el acuerdo, [!DNL Adobe] completará el proceso de incorporación y verá la tarjeta de destino [!DNL Acxiom Real ID Audience Connection].
* **Conozca su ID de organización de Adobe:** Se necesita su ID de organización [!DNL Adobe] para completar las condiciones del contrato de usuario. Consulte el tema [!DNL Adobe's] *Organizaciones en Experience Cloud* para obtener detalles sobre cómo [ver su ID de organización](https://experienceleague.adobe.com/es/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255).
* **Obtener licencia para [!DNL Acxiom's Real ID] producto:** Una vez obtenida la licencia, haga que Real ID de Acxiom esté disponible en Real-Time CDP. Consulte [Mejora de datos de Acxiom](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/data-partner/acxiom-data-enhancement) para obtener más información.


## Identidades admitidas {#supported-identities}

[!DNL Acxiom's Real ID Audience Connection] destino admite la activación de identidades descritas en la tabla siguiente. Más información sobre [identidades](https://experienceleague.adobe.com/es/docs/experience-platform/identity/features/namespaces).

| Identidad de destino | Descripción | Consideraciones |
|---------------|----------------|----------------|
| Real ID | [!DNL Acxiom Real ID] | Seleccione esta identidad de destino cuando su identidad de origen sea un área de nombres Acxiom Real ID. |
| extern_id | ID de usuario personalizados | Seleccione esta identidad de destino cuando la identidad de origen sea un área de nombres personalizada. |

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
|---------------|----------------|----------------|
| Servicio de segmentación | ✓ | Audiencias generadas a través del [servicio de segmentación](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/home) de Experience Platform. |
| Cargas personalizadas | ✓ | Las audiencias [importadas](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/audience-portal#import-audience) en Experience Platform desde archivos CSV. |


## Destinos admitidos {#supported-destinations}

[!DNL Acxiom's Real ID Audience Connection] destino admite actualmente la activación de audiencia en las siguientes plataformas.

* [!DNL Altice]
* [!DNL Ampersand]
* [!DNL Comcast]
* [!DNL Cox]
* [[!DNL LG Ads]](#lg-ads)
* [!DNL Spectrum]
* [!DNL Viant]

## Conectar con el destino {#connect}

Para su comodidad, la autenticación en el destino [!DNL Acxiom's Real ID Audience Connection] se administra automáticamente entre bastidores.

## Configuración específica del destino {#destination-settings}

Algunos [!DNL Acxiom Real ID Audience Connection] destinos requieren información adicional. Las secciones siguientes proporcionan instrucciones detalladas sobre cómo configurar estas opciones.

### [!DNL LG Ads] {#lg-ads}

Para configurar los detalles del destino, rellene los campos siguientes.

* **Categoría del segmento**: La categoría o vertical de destino en la que se encuentra el segmento. Ejemplo: servicios financieros, automoción, salud, etc.

![Detalles de destino de anuncios LG](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_lg_ads_destination_details.png)


## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>* Para activar los datos, necesita los permisos de control de acceso **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** y **[!UICONTROL View Segments]** [5&rbrace;. &#x200B;](/help/access-control/home.md#permissions) Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>* Para exportar *identidades*, necesita el **[!UICONTROL View Identity Graph]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}



Lea [Activar datos de audiencia en destinos de exportación de perfiles por lotes](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) para obtener instrucciones sobre cómo activar audiencias en este destino.

>[!NOTE]
>
>El destino [!DNL Acxiom Real ID Audience Connection] solo admite exportaciones de archivos completas.


### Asignar atributos e identidades {#map}

Para que el destino [!DNL Acxiom Real ID Audience Connection] reciba correctamente los datos de audiencia, debe asignar el campo de origen de Experience Platform al campo de destino [!DNL Acxiom Real ID Audience Connection] correcto.

[!DNL Acxiom Real ID Audience Connection] solo permite la asignación al siguiente campo de destino.

| Nombre del campo | Descripción | Requerido |
|--------------------|------------|--------| 
| Real ID | Un ID real es un identificador alfanumérico (ID) único de 36 bytes del gráfico de resolución de identidad propiedad de Acxiom, similar a una clave principal para una base de datos relacional. Es un identificador que representa a una persona, un hogar o una dirección. | Sí |



En la columna **[!UICONTROL Source Field]**, escriba el nombre del atributo de origen que desea asignar al campo de destino correspondiente o seleccione el icono de flecha para abrir la pantalla **[!UICONTROL &#x200B; Select source field]**. A continuación, seleccione **[!UICONTROL Next]**.
![Pantalla de asignación](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_mapping_screen.png)


Si no usa el esquema estándar [!DNL Adobe's], consulte la documentación de la [guía de la interfaz de usuario del servicio de consultas](../../../query-service/ui/overview.md) para obtener información sobre cómo usar el servicio de consultas para rellenar el esquema estándar [!DNL Adobe] con los nombres de los campos.


### Revisar {#review}

Una vez que haya completado todos los pasos anteriores, tiene la oportunidad de revisar el estado de la conexión de destino y los detalles de audiencia antes de activarla (distribuirla). Las audiencias que seleccionó se mostrarán en la parte inferior de una lista. Cada audiencia será una llamada independiente a la API [!DNL Acxiom Real ID Audience Connection].

Si está satisfecho con los resultados, seleccione **[!UICONTROL Finish]** para activar el destino.

![Revise su audiencia](../../assets/catalog/advertising/acxiom-real-id-audience-connection/real_id_review_audience.png)


## Uso de datos y gobernanza {#data-usage-governance}

Todos los destinos de [!DNL Adobe Experience Platform] cumplen con las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica el control de datos, lea la [Información general sobre el control de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/home).

## Resolución de problemas {#troubleshooting}

Si el representante de destino no puede encontrar la audiencia, póngase en contacto con el representante de [!DNL Adobe] para obtener ayuda.

Deberá proporcionar la siguiente información a su representante de [!DNL Adobe]:

* Nombre del público
* Nombre del destino
* Fecha de activación de audiencia
* Nombre de archivo exportado

## Próximos pasos {#next-steps}

Al seguir este tutorial, ha activado correctamente una audiencia en la plataforma de destino seleccionada. A continuación, póngase en contacto con el representante de la plataforma de destino para comenzar a configurar la campaña.
