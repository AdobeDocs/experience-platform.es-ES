---
keywords: linkedin connection;linkedin connection;linkedin destinos;linkedin;
title: Conexión de Audiencias coincidentes de Linkedin
description: Active perfiles para las campañas de LinkedIn para la segmentación, personalización y supresión de audiencias, en función de los correos electrónicos con hash.
translation-type: tm+mt
source-git-commit: db2e5d51a5ed07b91997df8a566272c86a7c1708
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audience] connection

Active perfiles para sus [!DNL LinkedIn] campañas de segmentación, personalización y supresión de audiencias, en base a correos electrónicos con hash e ID móviles.

![Destino de LinkedIn en la interfaz de usuario de Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casos de uso

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el destino [!DNL LinkedIn Matched Audience], aquí tiene un caso de uso que los clientes de Adobe Experience Platform pueden resolver mediante esta función.

Una compañía de software organiza una conferencia y desea mantenerse en contacto con los participantes, y mostrarles ofertas personalizadas en función de su estado de asistencia a la conferencia. La compañía puede ingerir direcciones de correo electrónico o ID de dispositivos móviles desde su propia [!DNL CRM] en Adobe Experience Platform, generar segmentos a partir de sus propios datos sin conexión y enviar estos segmentos a la [!DNL LinkedIn] plataforma social, optimizando así la inversión en publicidad.

## Detalles de destino {#destination-specs}

[!DNL LinkedIn Matched Audience] admite la activación de las siguientes identidades: correos electrónicos con hash  [!DNL GAID], y  [!DNL IDFA].

### Tipo de exportación {#export-type}

**Exportación**  de segmentos: está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono, etc.) se utiliza en el destino [!DNL LinkedIn Matched Audience].

### Requisitos previos de la cuenta de LinkedIn {#LinkedIn-account-prerequisites}

Antes de utilizar el destino [!UICONTROL Audiencia coincidente de LinkedIn], asegúrese de que su cuenta [!DNL LinkedIn Campaign Manager] tiene el nivel de permiso [!DNL Creative Manager] o superior.

Para obtener información sobre cómo editar los [!DNL LinkedIn Campaign Manager] permisos de usuario, consulte [Añadir, editar y eliminar permisos de usuario en cuentas de publicidad](https://www.linkedin.com/help/lms/answer/5753) en la documentación de LinkedIn.

### Requisitos de coincidencia de ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audience] exige que no se envíe con claridad ninguna información de identificación personal. Por lo tanto, las audiencias activadas en [!DNL LinkedIn Matched Audience] se pueden desactivar *identificadores con hash*, como direcciones de correo electrónico o ID de dispositivos móviles.

Según el tipo de ID que ingrese en Adobe Experience Platform, debe cumplir los requisitos correspondientes.

#### Requisitos de hash de correo electrónico {#email-hashing-requirements}

Puede elegir hash las direcciones de correo electrónico antes de ingerirlas en Adobe Experience Platform, o puede elegir trabajar con las direcciones de correo electrónico de forma clara en Experience Platform y hacer que nuestro algoritmo las incluya en activación.

Para obtener más información sobre la ingesta de direcciones de correo electrónico en Experience Platform, consulte la [información general sobre la ingestión por lotes](/help/ingestion/batch-ingestion/overview.md) y la [información general sobre la ingestión de flujo](/help/ingestion/streaming-ingestion/overview.md).

Si selecciona hash para las direcciones de correo electrónico usted mismo, asegúrese de cumplir con los siguientes requisitos:

- Recorte todos los espacios al inicio y al final de la cadena de correo electrónico. Por ejemplo: `johndoe@example.com`, no `<space>johndoe@example.com<space>`;
- Al aplicar hash a las cadenas de correo electrónico, asegúrese de que la cadena está en minúsculas;
   - Ejemplo: `example@email.com`, no `EXAMPLE@EMAIL.COM`;
- Asegúrese de que la cadena con hash esté en minúsculas
   - Ejemplo: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, no `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- No escriba la cadena.

>[!NOTE]
>
>Los datos de las Áreas de nombres sin hash se hash automáticamente mediante [!DNL Platform] en el momento de la activación.
> Los datos de origen de atributos no se hash automáticamente.
> 
> Durante el paso [Asignación de identidad](../../ui/activate-destinations.md#identity-mapping), cuando el campo de origen contenga atributos sin hash, marque la opción **[!UICONTROL Aplicar transformación]** para que [!DNL Platform] hash automáticamente los datos en la activación.
> 
> La opción **[!UICONTROL Aplicar transformación]** solo se muestra cuando se seleccionan atributos como campos de origen. No se muestra al elegir Áreas de nombres.

![Transformación de asignación de identidades](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Conectar al destino {#connect-destination}

Para conectarse al destino [!DNL LinkedIn Matched Audience], consulte [Flujo de trabajo de autenticación de destinos de red social](./workflow.md).

## Activar segmentos a [!DNL LinkedIn Matched Audience] {#activate-segments}

Para obtener instrucciones sobre cómo activar segmentos en [!DNL LinkedIn Matched Audience], consulte [Activar datos en destinos](../../ui/activate-destinations.md).

## Datos exportados {#exported-data}

Una activación exitosa significa que se creará una audiencia personalizada [!DNL LinkedIn] mediante programación en [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). La pertenencia a segmentos en la audiencia se agregaría y eliminaría a medida que los usuarios estuvieran cualificados o descalificados para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL LinkedIn Matched Audience] admite los rellenos de audiencia históricos. Todas las cualificaciones del segmento histórico se envían a [!DNL LinkedIn] al activar los segmentos en el destino.