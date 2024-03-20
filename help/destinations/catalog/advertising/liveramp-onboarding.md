---
title: 'LiveRamp: conexión de incorporación'
description: Aprenda a utilizar el conector LiveRamp para incorporar audiencias de Adobe Real-time Customer Data Platform a LiveRamp Connect.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: a235f9a66ea15fc5e72dd6ed03e4a6a384fd30a4
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 3%

---

# [!DNL LiveRamp - Onboarding] conexión {#liveramp-onboarding}

Utilice el [!DNL LiveRamp - Onboarding] conexión a audiencias integradas de Adobe Real-time Customer Data Platform a [!DNL LiveRamp Connect].

## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe utilizar el [!DNL LiveRamp - Onboarding] Destino, este es un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden solucionar mediante este destino.

Como especialista en marketing, quiero enviar audiencias de Adobe Experience Platform a identidades integradas en [!DNL LiveRamp Connect] para poder dirigirme a usuarios en dispositivos móviles, sitios web abiertos, medios sociales y [!DNL CTV] plataformas, usar el [!DNL Ramp ID] identificador.

## Requisitos previos {#prerequisites}

El [!DNL LiveRamp - Onboarding] la conexión exporta archivos mediante [SFTP de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) almacenamiento.

Antes de enviar datos de Experience Platform a [!DNL LiveRamp - Onboarding], necesita su [!DNL LiveRamp] credenciales. Póngase en contacto con su [!DNL LiveRamp] para obtener sus credenciales, si aún no las tiene.

## Identidades admitidas {#supported-identities}

[!DNL LiveRamp - Onboarding] admite la activación de identidades como identificadores basados en PII, identificadores conocidos e ID personalizados, descritos en el [Documentación de LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

En el [paso de asignación](#map) del flujo de trabajo de activación, debe definir las asignaciones de destino como atributos personalizados.

## Audiencias compatibles {#supported-audiences}

Esta sección describe qué tipos de audiencias puede exportar a este destino.

| Origen de audiencia | Admitido | Descripción |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiencias generadas mediante el Experience Platform [Servicio de segmentación](../../../segmentation/home.md). |
| Cargas personalizadas | ✓ | Audiencias [importado](../../../segmentation/ui/overview.md#import-audience) en el Experience Platform desde archivos CSV. |

{style="table-layout:auto"}

## Tipo y frecuencia de exportación {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de audiencia]** | Va a exportar todos los miembros de una audiencia con los identificadores (nombre, número de teléfono u otros) utilizados en [!DNL LiveRamp - Onboarding] destino. |
| Frecuencia de exportación | **[!UICONTROL Lote diario]** | A medida que los perfiles se actualizan en Experience Platform según la evaluación de audiencias, los perfiles (identidades) se actualizan una vez al día de forma descendente a la plataforma de destino. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conexión al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita el **[!UICONTROL Ver destinos]** y **[!UICONTROL Administrar destinos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos enumerados en las dos secciones siguientes.

### Autenticarse en el destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectar con destino]**.

**Autenticación SFTP con contraseña** {#sftp-password}

![Captura de pantalla de ejemplo que muestra cómo autenticarse en el destino mediante SFTP con contraseña](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Puerto]**: El puerto utilizado para el [!DNL LiveRamp - Onboarding] ubicación de almacenamiento.  Utilice el puerto que corresponda a su ubicación geográfica, tal como se describe a continuación:
   * **[!UICONTROL NA]**: utilice el puerto `22`
   * **[!UICONTROL AU]**: utilice el puerto `2222`
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL LiveRamp - Onboarding] ubicación de almacenamiento.
* **[!UICONTROL Contraseña]**: La contraseña de su [!DNL LiveRamp - Onboarding] ubicación de almacenamiento.
* **[!UICONTROL Clave de cifrado PGP/GPG]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.
  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL ID de subclave]**: Si proporciona una clave de cifrado, también debe proporcionar un cifrado **[!UICONTROL ID de subclave]**. Consulte la [!DNL LiveRamp] [documentación de cifrado](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) para obtener información sobre cómo obtener el ID de subclave.

**SFTP con autenticación de clave SSH** {#sftp-ssh}

![Captura de pantalla de ejemplo que muestra cómo autenticarse en el destino con una clave SSH](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Puerto]**: El puerto utilizado para el [!DNL LiveRamp - Onboarding] ubicación de almacenamiento.  Utilice el puerto que corresponda a su ubicación geográfica, tal como se describe a continuación:
   * **[!UICONTROL UE]**: utilice el puerto `4222`
* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL LiveRamp - Onboarding] ubicación de almacenamiento.
* **[!UICONTROL Clave SSH]**: el privado [!DNL SSH] clave utilizada para iniciar sesión en su [!DNL LiveRamp - Onboarding] ubicación de almacenamiento. La clave privada debe tener el formato [!DNL Base64]cadena codificada en y no debe estar protegida con contraseña.

   * Para conectar su [!DNL SSH] clave para el [!DNL LiveRamp - Onboarding] servidor, debe enviar un ticket a través de [!DNL LiveRamp]Portal de asistencia técnica de y proporcione la clave pública. Consulte más información en la [Documentación de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Clave de cifrado PGP/GPG]**: Opcionalmente, puede adjuntar la clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la siguiente imagen.
  ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la IU de](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL ID de subclave]**: Si proporciona una clave de cifrado, también debe proporcionar un cifrado **[!UICONTROL ID de subclave]**. Consulte la [!DNL LiveRamp] [documentación de cifrado](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) para obtener información sobre cómo obtener el ID de subclave.

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID de subclave de cifrado"
>abstract="El ID de subclave utilizado para el cifrado, en función de la clave de cifrado pública de LiveRamp. Este campo es obligatorio si ha proporcionado una clave de cifrado en el paso de autenticación."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Información sobre cómo obtener el ID de subclave"

Para configurar los detalles del destino, rellene los campos obligatorios y opcionales a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de la IU de Platform que muestra cómo rellenar los detalles del destino](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-destination-details.png)

* **[!UICONTROL Nombre]**: Un nombre con el que reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Una descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Región]**: Región geográfica de la instancia de almacenamiento SFTP de LiveRamp.
* **[!UICONTROL Ruta de carpeta]**: La ruta al [!DNL LiveRamp] `uploads` subcarpeta que alojará los archivos exportados. El `uploads` El prefijo se añade automáticamente a la ruta de la carpeta. [!DNL LiveRamp] recomienda crear una subcarpeta específica para las entregas de Adobe Real-Time CDP a fin de mantener los archivos separados de cualquier otra fuente existente y garantizar que toda la automatización se ejecute sin problemas.
   * Por ejemplo, si desea exportar los archivos a `uploads/my_export_folder`, escriba `my_export_folder` en el **[!UICONTROL Ruta de carpeta]** field.
* **[!UICONTROL Formato de compresión]**: seleccione el tipo de compresión que el Experience Platform debe utilizar para los archivos exportados. Las opciones disponibles son **[!UICONTROL GZIP]** o **[!UICONTROL Ninguno]**.

### Habilitar alertas {#enable-alerts}

Puede activar alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista a la que suscribirse para recibir notificaciones sobre el estado del flujo de datos. Para obtener más información sobre las alertas, lea la guía de [suscripción a alertas de destinos mediante la IU](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar públicos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Leer [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre cómo activar audiencias en este destino.

### Programación {#scheduling}

En el [!UICONTROL Programación] , cree una programación de exportación para cada audiencia con la configuración que se muestra a continuación.

* **[!UICONTROL Opciones de exportación de archivos]**: [!UICONTROL Exportar archivos completos]. [Exportaciones incrementales de archivos](../../ui/activate-batch-profile-destinations.md#export-incremental-files) actualmente no son compatibles con [!DNL LiveRamp] destino.
* **[!UICONTROL Frecuencia]**: [!UICONTROL Diario]
* **[!UICONTROL Fecha]**: seleccione las horas de inicio y finalización de la exportación según desee.

![Captura de pantalla de la IU de Platform que muestra el paso de programación de audiencias.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

El nombre del archivo exportado no se puede configurar por el usuario en este momento. Todos los archivos exportados a [!DNL LiveRamp - Onboarding] Los nombres de los destinos de se asignan automáticamente en función de la siguiente plantilla:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Captura de pantalla de la IU de Platform que muestra la plantilla de nombre de archivo exportada.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

Por ejemplo, el nombre de un archivo exportado para una organización denominada [!DNL Luma] podría tener un aspecto similar al siguiente:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Asignar atributos e identidades {#map}

En el **[!UICONTROL Asignación]** , puede seleccionar qué atributos e identidades desea exportar para sus perfiles.

>[!IMPORTANT]
>
>Este destino admite la activación de un área de nombres de identidad de origen por flujo de activación. Si necesita exportar varias áreas de nombres de identidad, como `Email` y `Phone`, debe [crear un flujo de activación independiente](../../ui/activate-batch-profile-destinations.md) para cada identidad.

En el **[!UICONTROL Asignación]** step, la **[!UICONTROL Campo de destino]** La asignación define el nombre del encabezado de columna en el archivo CSV exportado. Puede cambiar los encabezados de columna CSV del archivo exportado a cualquier nombre descriptivo que desee, proporcionando un nombre personalizado para la variable **[!UICONTROL Campo de destino]**.

>[!IMPORTANT]
>
>Para cualquier cambio realizado en los campos de destino después de la entrega inicial del archivo a [!DNL LiveRamp], notifique a su [!DNL LiveRamp] equipo de la cuenta o [enviar un ticket al Soporte de LiveRamp](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) para garantizar que los cambios se reflejen en el proceso de automatización.

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.

   ![Captura de pantalla de la IU del Experience Platform que muestra la pantalla Asignación.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione la **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM que desee asignar o elija el **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad para asignar a su destino.

   ![Captura de pantalla de la IU del Experience Platform que muestra la pantalla Asignación de origen.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. En el **[!UICONTROL Seleccionar campo de destino]** , introduzca el nombre de atributo al que desea asignar el campo de origen seleccionado. El nombre del atributo definido aquí se reflejará en el archivo CSV exportado como un encabezado de columna.

   ![Captura de pantalla de la IU del Experience Platform que muestra la pantalla Asignación de destino.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   También puede escribir el nombre del atributo directamente en la variable **[!UICONTROL Campo de destino]**.

   ![Captura de pantalla de la IU del Experience Platform que muestra la pantalla Asignación de destino.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Una vez que haya añadido todas las asignaciones deseadas, seleccione **[!UICONTROL Siguiente]** y finalizar el flujo de trabajo de activación.

## Datos exportados / Validar exportación de datos {#exported-data}

Los datos se exportan a [!DNL LiveRamp - Onboarding] ubicación de almacenamiento que ha configurado como archivos CSV.

Los archivos exportados tienen un tamaño máximo de 10 millones de filas. Experience Platform genera varios archivos por envío si las audiencias seleccionadas superan los 10 millones de filas. Si espera superar el límite de un solo archivo, póngase en contacto con su [!DNL LiveRamp] y pídale que configure la ingesta por lotes.

Al exportar archivos a [!DNL LiveRamp - Onboarding] destino, Platform genera un archivo CSV para cada [ID de política de combinación](../../../profile/merge-policies/overview.md).

Por ejemplo, consideremos las siguientes audiencias:

* Audiencia A (política de combinación 1)
* Audiencia B (política de combinación 2)
* Audiencia C (política de combinación 1)
* Audience D (política de combinación 1)

Platform exportará dos archivos CSV a [!DNL LiveRamp - Onboarding]:

* Un archivo CSV que contiene las audiencias A, C y D;
* Un archivo CSV que contiene la audiencia B.

Los archivos CSV exportados contienen perfiles con los atributos seleccionados y el estado de audiencia correspondiente, en columnas independientes, con el nombre del atributo y `audience_namespace:audience_ID` pares como encabezados de columna, como se muestra en el ejemplo siguiente:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1_AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2_AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X_AUDIENCE_ID_X`

Los perfiles incluidos en los archivos exportados pueden coincidir con uno de los siguientes estados de cualificación de audiencia:

* `Active`: el perfil está cualificado actualmente para la audiencia.
* `Expired`: el perfil ya no está cualificado para la audiencia, pero lo ha estado en el pasado.
* `""`(cadena vacía): El perfil nunca cumplió los requisitos para la audiencia.

Por ejemplo, un archivo CSV exportado con una `email` atributo, dos audiencias que se originan en el Experience Platform [Servicio de segmentación](../../../segmentation/home.md), y uno [importado](../../../segmentation/ui/overview.md#importing-an-audience) audiencia externa, podría tener este aspecto:

```csv
email,ups_aa2e3d98-974b-4f8b-9507-59f65b6442df,ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

En el ejemplo anterior, la variable `ups_aa2e3d98-974b-4f8b-9507-59f65b6442df` y `ups_45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` Las secciones de describen audiencias que se originan en el servicio de segmentación, mientras que `CustomerAudienceUpload_7729e537-4e42-418e-be3b-dce5e47aaa1e` describe una audiencia importada en Platform as a [carga personalizada](../../../segmentation/ui/overview.md#importing-an-audience).

Dado que Platform genera un archivo CSV para cada [ID de política de combinación](../../../profile/merge-policies/overview.md)Además, también genera una ejecución de flujo de datos independiente para cada ID de política de combinación.

Esto significa que la variable **[!UICONTROL Identidades activadas]** y **[!UICONTROL Perfiles recibidos]** métricas en la [ejecuciones de flujo de datos](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) Las páginas se agregan para cada grupo de audiencias que utilizan la misma política de combinación, en lugar de mostrarse para cada audiencia.

Como consecuencia de la generación de ejecuciones de flujo de datos para un grupo de audiencias que utilizan la misma política de combinación, los nombres de audiencia no se muestran en la [panel de monitorización](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Captura de pantalla de la IU del Experience Platform que muestra la métrica de identidades activadas.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Cargar datos exportados a LiveRamp {#upload-to-liveramp}

Una vez que los datos se hayan exportado correctamente a [!DNL LiveRamp - Onboarding] almacenamiento, debe cargar los datos en el [!DNL LiveRamp] plataforma.

Para obtener más información sobre cómo cargar los archivos desde [!DNL LiveRamp - Onboarding] almacenamiento en una [!DNL LiveRamp] Consulte la siguiente documentación: [Consideraciones al cargar el primer archivo en una audiencia](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Uso de datos y gobernanza {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen con las políticas de uso de datos al gestionar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] aplica la gobernanza de datos, lea la [Resumen de gobernanza de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener más información sobre cómo configurar su [!DNL LiveRamp - Onboarding] , consulte la [documentación oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).

## Changelog {#changelog}

Esta sección recoge la funcionalidad y las actualizaciones significativas de la documentación realizadas en este conector de destino.

+++ Ver registro de cambios

| Mes de lanzamiento | Tipo de actualización | Descripción |
|---|---|---|
| Marzo de 2024 | Actualización de funcionalidad y documentación | <ul><li>Se añadió la compatibilidad con las entregas a Europa y Australia [!DNL LiveRamp] [!DNL SFTP] instancias.</li><li>Se ha actualizado la documentación para describir configuraciones específicas para regiones de reciente compatibilidad.</li><li>Se ha aumentado el tamaño máximo de archivo a 10 millones de filas (de 5 millones, anteriormente).</li><li>Se ha actualizado la documentación para reflejar el aumento del tamaño de los archivos.</li></ul> |
| Julio de 2023 | Versión inicial | Versión de destino inicial y documentación publicada. |

{style="table-layout:auto"}

+++
