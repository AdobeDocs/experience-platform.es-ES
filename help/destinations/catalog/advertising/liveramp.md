---
title: (Alpha) [!DNL LiveRamp SFTP] connection
description: Aprenda a utilizar el conector LiveRamp para incorporar audiencias de Adobe Real-time Customer Data Platform a LiveRamp Connect.
hidefromtoc: true
hide: true
source-git-commit: 367ef59f623acc38e636a6cae0c85f186eaccfda
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---


# (Alpha) [!DNL LiveRamp - SFTP] connection {#liveramp-destination}

Utilice la conexión de LiveRamp para las audiencias integradas de Adobe Real-time Customer Data Platform a [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Esta conexión de destino se encuentra actualmente en fase alfa y solo está disponible para una selección limitada de clientes. La funcionalidad y la documentación están sujetas a cambios.</p>
&gt;<p>La versión final de esta conexión de destino puede requerir la migración del cliente.</p>


## Casos de uso {#use-cases}

Para ayudarle a comprender mejor cómo y cuándo debe usar la variable [!DNL LiveRamp SFTP] destino, aquí hay un ejemplo de caso de uso que los clientes de Adobe Experience Platform pueden resolver utilizando este destino.

Como especialista en marketing, quiero enviar audiencias de Adobe Experience Platform a identidades integradas a [!DNL LiveRamp Connect] para poder orientar a los usuarios hacia [!DNL CTV] plataformas, usando la variable [!DNL Ramp ID] identificador.

## Requisitos previos {#prerequisites}

La variable [!DNL LiveRamp - SFTP] la conexión exporta archivos [SFTP de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) almacenamiento.

Antes de poder enviar datos de Experience Platform a [!DNL LiveRamp SFTP], necesita su [!DNL LiveRamp] credenciales. Póngase en contacto con su [!DNL LiveRamp] para obtener sus credenciales, si aún no las tiene.

## Identidades compatibles {#supported-identities}

LiveRamp SFTP es compatible con la activación de identidades como identificadores basados en PII, identificadores conocidos e ID personalizados, que se describen en el [Documentación de LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

En el [paso de asignación](#map) del flujo de trabajo de activación, debe definir las asignaciones de destino como atributos personalizados.

## Tipo de exportación y frecuencia {#export-type-frequency}

Consulte la tabla siguiente para obtener información sobre el tipo y la frecuencia de exportación de destino.

| Elemento | Tipo | Notas |
---------|----------|---------|
| Tipo de exportación | **[!UICONTROL Exportación de segmentos]** | Está exportando todos los miembros de un segmento (audiencia) con los identificadores (nombre, número de teléfono u otros) utilizados en la variable [!DNL LiveRamp SFTP] destino. |
| Frecuencia de exportación | **[!UICONTROL Lote diario]** | A medida que los perfiles se actualizan en el Experience Platform en función de la evaluación de segmentos, los perfiles (identidades) se actualizan una vez al día después de la plataforma de destino. Más información sobre [destinos basados en archivos por lotes](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Conectarse al destino {#connect}

>[!IMPORTANT]
> 
>Para conectarse al destino, necesita la variable **[!UICONTROL Administrar destinos]** [permiso de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Para conectarse a este destino, siga los pasos descritos en la sección [tutorial de configuración de destino](../../ui/connect-destination.md). En el flujo de trabajo de configuración de destino, rellene los campos que aparecen en las dos secciones siguientes.

### Autenticar en destino {#authenticate}

Para autenticarse en el destino, rellene los campos obligatorios y seleccione **[!UICONTROL Conectarse al destino]**.

**Autenticación SFTP con contraseña** {#sftp-password}

![Captura de pantalla de ejemplo que muestra cómo autenticarse en el destino mediante SFTP con contraseña](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL LiveRamp SFTP] ubicación de almacenamiento.
* **[!UICONTROL Contraseña]**: La contraseña de su [!DNL LiveRamp SFTP] ubicación de almacenamiento.
* **[!UICONTROL Clave de cifrado PGP/GPG]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Vea un ejemplo de una clave de cifrado con formato correcto en la imagen siguiente. Si proporciona una clave de cifrado, también debe proporcionar una **[!UICONTROL ID de subclave de cifrado]** en el [detalles de destino](#destination-details) para obtener más información.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la interfaz de usuario](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP con autenticación de clave SSH** {#sftp-ssh}

![Captura de pantalla de ejemplo que muestra cómo autenticarse en el destino mediante la clave SSH](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Nombre de usuario]**: El nombre de usuario de su [!DNL LiveRamp SFTP] ubicación de almacenamiento.
* **[!UICONTROL Clave SSH]**: El [!DNL SSH] clave utilizada para iniciar sesión en su [!DNL LiveRamp SFTP] ubicación de almacenamiento. La clave privada debe tener el formato de [!DNL Base64]-cadena codificada y no debe estar protegido con contraseña.

   * Para conectar su [!DNL SSH] para [!DNL LiveRamp SFTP] servidor, debe enviar un ticket a través de [!DNL LiveRamp]y proporcione su clave pública. Consulte más información en la [Documentación de LiveRamp](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL Clave de cifrado PGP/GPG]**: Opcionalmente, puede adjuntar su clave pública con formato RSA para agregar cifrado a los archivos exportados. Si proporciona una clave de cifrado, también debe proporcionar una **[!UICONTROL ID de subclave de cifrado]** en el [detalles de destino](#destination-details) para obtener más información. Vea un ejemplo de una clave de cifrado con formato correcto en la imagen siguiente.

   ![Imagen que muestra un ejemplo de una clave PGP con formato correcto en la interfaz de usuario](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Rellenar detalles de destino {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="ID de subclave de cifrado"
>abstract="El ID de subclave utilizado para el cifrado, en función de la clave de cifrado pública de LiveRamp. Este campo es obligatorio si ha proporcionado una clave de cifrado en el paso de autenticación."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Obtenga información sobre cómo obtener el ID de subclave"

Para configurar los detalles del destino, rellene los campos opcionales y requeridos a continuación. Un asterisco junto a un campo en la interfaz de usuario indica que el campo es obligatorio.

![Captura de pantalla de la interfaz de usuario de Platform que muestra cómo rellenar los detalles para el destino](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Nombre]**: Un nombre por el cual reconocerá este destino en el futuro.
* **[!UICONTROL Descripción]**: Descripción que le ayudará a identificar este destino en el futuro.
* **[!UICONTROL Ruta de carpeta]**: La ruta al [!DNL LiveRamp] `uploads` subcarpeta que alojará los archivos exportados. La variable `uploads` se añade automáticamente a la ruta de la carpeta.
   * Por ejemplo, si desea exportar los archivos a `uploads/my_export_folder`, escriba `my_export_folder` en el **[!UICONTROL Ruta de carpeta]** campo .
* **[!UICONTROL Formato de compresión]**: Seleccione el tipo de compresión que debe utilizar el Experience Platform para los archivos exportados. Las opciones disponibles son **[!UICONTROL GZIP]** o **[!UICONTROL Ninguna]**.
* **[!UICONTROL ID de subclave de cifrado]**: La subclave utilizada para el cifrado, en función de la variable [!DNL LiveRamp] clave pública de cifrado. Este campo es obligatorio si ha proporcionado una clave de cifrado en la variable [autenticación](#authenticate) paso a paso. Consulte la [!DNL LiveRamp] [documentación de cifrado](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) para obtener información sobre cómo obtener el ID de subclave.

### Habilitar alertas {#enable-alerts}

Puede activar las alertas para recibir notificaciones sobre el estado del flujo de datos a su destino. Seleccione una alerta de la lista para suscribirse y recibir notificaciones sobre el estado de su flujo de datos. Para obtener más información sobre las alertas, consulte la guía de [suscripción a alertas de destinos mediante la interfaz de usuario](../../ui/alerts.md).

Cuando haya terminado de proporcionar detalles para la conexión de destino, seleccione **[!UICONTROL Siguiente]**.

## Activar segmentos en este destino {#activate}

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

Lectura [Activar datos de audiencia en destinos de exportación de perfiles en lote](/help/destinations/ui/activate-batch-profile-destinations.md) para obtener instrucciones sobre la activación de segmentos de audiencia en este destino.

### Programación {#scheduling}

En el [!UICONTROL Programación] , cree una programación de exportación para cada segmento, con la configuración que se muestra a continuación.

>[!IMPORTANT]
>
>Todos los segmentos activados en este destino deben configurarse con la misma programación, como se muestra a continuación.

* **[!UICONTROL Opciones de exportación de archivos]**: [!UICONTROL Exportar archivos completos]. [Exportaciones de archivos incrementales](../../ui/activate-batch-profile-destinations.md#export-incremental-files) actualmente no son compatibles con el [!DNL LiveRamp] destino.
* **[!UICONTROL Frecuencia]**: [!UICONTROL Diario]
* Configure la hora de exportación a **[!UICONTROL Después de la evaluación de segmentos]**. Exportaciones de segmentos programadas y [exportaciones de archivos bajo demanda](../../ui/export-file-now.md) actualmente no son compatibles con el [!DNL LiveRamp] destino.
* **[!UICONTROL Fecha]**: Seleccione las horas de inicio y finalización de la exportación que desee.

![Captura de pantalla de la interfaz de usuario de Platform que muestra el paso de programación del segmento.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

El nombre de archivo exportado no se puede configurar por el usuario. Todos los archivos exportados a [!DNL LiveRamp SFTP] el nombre de destino se asigna automáticamente en función de la siguiente plantilla:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Captura de pantalla de la interfaz de usuario de Platform que muestra la plantilla de nombre de archivo exportada.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Por ejemplo, el nombre de un archivo exportado para una organización llamada [!DNL Luma] podría tener un aspecto similar al siguiente:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Asignación de atributos e identidades {#map}

En el **[!UICONTROL Asignación]** , puede seleccionar qué atributos e identidades desea exportar para sus perfiles.

>[!IMPORTANT]
>
>Este destino admite la activación de un área de nombres de identidad de origen por flujo de activación. Si necesita exportar varias áreas de nombres de identidad, como `Email` y `Phone`, debe [crear un flujo de activación independiente](../../ui/activate-batch-profile-destinations.md) para cada identidad.

En el **[!UICONTROL Asignación]** paso, la variable **[!UICONTROL Campo de destino]** la asignación define el nombre del encabezado de columna del archivo CSV exportado. Puede cambiar los encabezados de columna CSV del archivo exportado a cualquier nombre descriptivo que desee, proporcionando un nombre personalizado para el **[!UICONTROL Campo de destino]**.

1. En el **[!UICONTROL Asignación]** paso, seleccione **[!UICONTROL Añadir nueva asignación]**. Verá una nueva fila de asignación en la pantalla.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la pantalla Asignación .](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione **[!UICONTROL Seleccionar atributos]** y seleccione el atributo XDM que desea asignar o elija la **[!UICONTROL Seleccionar área de nombres de identidad]** y seleccione una identidad para asignarla a su destino.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la pantalla de asignación de origen.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. En el **[!UICONTROL Seleccionar campo de destino]** , introduzca el nombre de atributo al que desea asignar el campo de origen seleccionado. El nombre de atributo definido aquí se reflejará en el archivo CSV exportado como encabezado de columna.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la pantalla Asignación de destino.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   También puede especificar el nombre del atributo escribiéndolo directamente en el **[!UICONTROL Campo de destino]**.

   ![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la pantalla Asignación de destino.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Una vez que haya añadido todas las asignaciones deseadas, seleccione **[!UICONTROL Siguiente]** y finalizar el flujo de trabajo de activación.

## Datos exportados / Validar exportación de datos {#exported-data}

Los datos se exportan al [!DNL LiveRamp SFTP] ubicación de almacenamiento que configuró, como archivos CSV.

Al exportar archivos a la variable [!DNL LiveRamp SFTP] destino, Platform genera un archivo CSV para cada [combinar id. de directiva](../../../profile/merge-policies/overview.md).

Por ejemplo, veamos los siguientes segmentos:

* Segmento A (política de combinación 1)
* Segmento B (política de combinación 2)
* Segmento C (política de combinación 1)
* Segmento D (política de combinación 1)

Platform exportará dos archivos CSV a [!DNL LiveRamp SFTP]:

* Un archivo CSV que contiene los segmentos A, C y D;
* Un archivo CSV que contiene el segmento B.

Los archivos CSV exportados contienen perfiles con los atributos seleccionados y el estado del segmento correspondiente, en columnas independientes, con el nombre del atributo y los ID de segmento como encabezados de columna.

Los perfiles incluidos en los archivos exportados pueden coincidir con uno de los siguientes estados de clasificación de segmentos:

* `Active`: El perfil está cualificado para el segmento.
* `Expired`: El perfil ya no está cualificado para el segmento, pero se ha clasificado en el pasado.
* `""`(cadena vacía): El perfil nunca se calificó para el segmento.


Por ejemplo, un archivo CSV exportado con un `email` y 3 segmentos podrían tener el siguiente aspecto:

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Dado que Platform genera un archivo CSV para cada [combinar id. de directiva](../../../profile/merge-policies/overview.md), también genera un flujo de datos independiente para cada ID de política de combinación.

Esto significa que la variable **[!UICONTROL Identidades activadas]** y **[!UICONTROL Perfiles recibidos]** métricas de [se ejecuta dataflow](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) se agregan para cada grupo de segmentos que utilizan la misma directiva de combinación, en lugar de mostrarse para cada segmento.

Como consecuencia de que se generan ejecuciones de flujo de datos para un grupo de segmentos que utilizan la misma política de combinación, los nombres de los segmentos no se muestran en la variable [panel de monitorización](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Captura de pantalla de la interfaz de usuario del Experience Platform que muestra la métrica de identidades activadas.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Carga de datos exportados a LiveRamp {#upload-to-liveramp}

Una vez exportados correctamente los datos a la variable [!DNL LiveRamp - SFTP] , debe cargar los datos en la variable [!DNL LiveRamp] plataforma.

Para obtener más información sobre cómo cargar los archivos desde la variable [!DNL LiveRamp - SFTP] almacenamiento en un [!DNL LiveRamp] , consulte la siguiente documentación: [Consideraciones al cargar el primer archivo en una audiencia](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Uso y gobernanza de los datos {#data-usage-governance}

Todo [!DNL Adobe Experience Platform] Los destinos de cumplen las políticas de uso de datos al administrar los datos. Para obtener información detallada sobre cómo [!DNL Adobe Experience Platform] exige la administración de datos, lea la [Información general sobre la administración de datos](/help/data-governance/home.md).

## Recursos adicionales {#additional-resources}

Para obtener más información sobre cómo configurar el almacenamiento SFTP de LiveRamp, consulte la [documentación oficial](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
