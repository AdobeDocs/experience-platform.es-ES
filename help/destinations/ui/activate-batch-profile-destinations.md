---
keywords: activar destinos de perfil;activar destinos;activar datos; activar destinos de marketing por correo electrónico; activar destinos de almacenamiento en la nube
title: Activar datos de audiencia en destinos de exportación de perfiles por lotes
type: Tutorial
description: Obtenga información sobre cómo activar los datos de audiencia que tiene en Adobe Experience Platform enviando segmentos a destinos basados en perfiles por lotes.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 5bb2981b8187fcd3de46f80ca6c892421b3590f6
workflow-type: tm+mt
source-wordcount: '3629'
ht-degree: 10%

---

# Activar datos de audiencia en destinos de exportación de perfiles por lotes

>[!IMPORTANT]
> 
> * Para activar los datos y habilitar la variable [paso de asignación](#mapping) del flujo de trabajo, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
> * Para activar los datos sin pasar por el [paso de asignación](#mapping) del flujo de trabajo, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar segmento sin asignación]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
> 
> Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.
>
> Algunos clientes que participan en el programa beta de funcionalidad de exportación de archivos mejorada están viendo el nuevo **[!UICONTROL Asignación]** paso como parte de su flujo de trabajo de activación a [nuevos destinos de almacenamiento en la nube beta](/help/release-notes/2022/october-2022.md#destinations). Tenga en cuenta también lo siguiente [limitaciones conocidas](#known-limitations) como parte de la versión de.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en destinos basados en perfiles por lotes de Adobe Experience Platform, como los destinos de marketing por correo electrónico y el almacenamiento en la nube.

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debe haber [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Seleccione su destino {#select-destination}

1. Ir a **[!UICONTROL Conexiones > Destinos]** y seleccione la opción **[!UICONTROL Catálogo]** pestaña.

   ![Imagen que resalta cómo llegar a la pestaña de catálogo de destinos](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Seleccionar **[!UICONTROL Activar segmentos]** en la tarjeta correspondiente al destino donde desea activar los segmentos, como se muestra en la siguiente imagen.

   ![Imagen que resalta el botón Activar segmentos](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Seleccione la conexión de destino que desee utilizar para activar los segmentos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Imagen que resalta cómo seleccionar uno o varios destinos para activar segmentos](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Mover a la sección siguiente para [seleccione sus segmentos](#select-segments).

## Seleccione sus segmentos {#select-segments}

Utilice las casillas de verificación de la izquierda de los nombres de segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Imagen que resalta cómo seleccionar uno o varios segmentos para activar](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Programar exportación de segmentos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Programación"
>abstract="Utilice el icono de lápiz para establecer el tipo de exportación de archivos (archivos completos o archivos incrementales) y la frecuencia de exportación."

[!DNL Adobe Experience Platform] exporta datos para destinos de marketing por correo electrónico y almacenamiento en la nube en forma de [!DNL CSV] archivos. En el **[!UICONTROL Programación]** , puede configurar la programación y los nombres de archivo para cada segmento que esté exportando. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automáticamente los archivos de exportación en 5 millones de registros (filas) por archivo. Cada fila representa un perfil.
>
>Los nombres de los archivos divididos se anexan con un número que indica que el archivo forma parte de una exportación más grande, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Seleccione el **[!UICONTROL Crear programación]** correspondiente al segmento que desea enviar a su destino.

![Imagen que resalta el botón Crear programación](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportar archivos completos {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Opciones de exportación de archivos"
>abstract="Seleccione **Exportar archivos completos** para exportar una instantánea completa de todos los perfiles que cumplen los requisitos para el segmento. Seleccione **Exportar archivos incrementales** para exportar solo los perfiles que cumplen los requisitos para el segmento desde la última exportación. <br> La primera exportación incremental de archivos incluye todos los perfiles que cumplen los requisitos para el segmento, actuando como relleno. Los futuros archivos incrementales incluyen solo los perfiles que cumplen los requisitos para el segmento desde la primera exportación de archivos incrementales."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=es#export-incremental-files" text="Exportar archivos incrementales"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Activar después de la evaluación de segmentos"
>abstract="La activación se ejecuta inmediatamente después de que se complete el trabajo de segmentación diaria. Esto garantiza que se exporten los perfiles más actualizados."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Activación programada"
>abstract="La activación se ejecuta a una hora fija del día."

Seleccionar **[!UICONTROL Exportar archivos completos]** para almacenar en déclencheur la exportación de un archivo que contenga una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado.

![Imagen de la interfaz de usuario con la opción Exportar archivos completos seleccionada.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Utilice el **[!UICONTROL Frecuencia]** selector para seleccionar la frecuencia de exportación:

   * **[!UICONTROL Una]**: programe una exportación de archivos completa bajo demanda de una sola vez.
   * **[!UICONTROL Diario]**: programe las exportaciones de archivos completas una vez al día, todos los días y a la hora especificada.

1. Utilice el **[!UICONTROL Hora]** cambie para seleccionar si la exportación debe realizarse inmediatamente después de la evaluación del segmento o de forma programada, a una hora especificada. Al seleccionar la variable **[!UICONTROL Programado]** , puede utilizar el selector para elegir la hora del día, en [!DNL UTC] formato, momento en el que se debe realizar la exportación.

   >[!NOTE]
   >
   >El **[!UICONTROL Después de la evaluación de segmentos]** La opción que se describe a continuación solo está disponible actualmente para clientes beta seleccionados.

   Utilice el **[!UICONTROL Después de la evaluación de segmentos]** para que el trabajo de activación se ejecute inmediatamente después de que se complete el trabajo diario de segmentación por lotes de Platform. Esto garantiza que, cuando se ejecute el trabajo de activación, los perfiles más actualizados se exporten al destino.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Imagen que resalta la opción After segment evaluation en el flujo de activación para destinos por lotes.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Utilice el **[!UICONTROL Programado]** para que el trabajo de activación se ejecute a una hora fija. Esto garantiza que los datos de perfil del Experience Platform se exporten a la misma hora cada día, pero es posible que los perfiles exportados no estén los más actualizados, en función de si el trabajo de segmentación por lotes se ha completado antes de que se inicie el trabajo de activación.

   ![Imagen que resalta la opción Programado en el flujo de activación para destinos por lotes y muestra el selector de tiempo.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

   >[!IMPORTANT]
   >
   >Debido al modo en que se configuran los procesos internos del Experience Platform, es posible que la primera exportación de archivo incremental o completa no contenga todos los datos de relleno. <br> <br> Para garantizar una exportación de datos de relleno completa y más actualizada tanto para archivos completos como incrementales, Adobe recomienda configurar la primera hora de exportación de archivo después de las 12 PM GMT del día siguiente. Esta limitación se solucionará en futuras versiones.

1. Utilice el **[!UICONTROL Fecha]** selector para elegir el día o el intervalo en el que debe realizarse la exportación. Para las exportaciones diarias, la práctica recomendada es establecer las fechas de inicio y finalización para que se alineen con la duración de las campañas en las plataformas de flujo descendente.

   >[!IMPORTANT]
   >
   > Al seleccionar un intervalo de exportación, el último día del intervalo no se incluye en las exportaciones. Por ejemplo, si selecciona un intervalo del 4 al 11 de enero, la última exportación de archivos se realizará el 10 de enero.

1. Seleccionar **[!UICONTROL Crear]** para guardar la programación.

### Exportar archivos incrementales {#export-incremental-files}

Seleccionar **[!UICONTROL Exportar archivos incrementales]** para almacenar en déclencheur una exportación en la que el primer archivo es una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado y los archivos siguientes son cualificaciones de perfil incrementales desde la exportación anterior.

>[!IMPORTANT]
>
>El primer archivo incremental exportado incluye todos los perfiles aptos para un segmento que funciona como relleno.

![Imagen de la interfaz de usuario con la opción Exportar archivos incrementales seleccionada.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Utilice el **[!UICONTROL Frecuencia]** selector para seleccionar la frecuencia de exportación:

   * **[!UICONTROL Diario]**: programe las exportaciones de archivos incrementales una vez al día, todos los días y a la hora especificada.
   * **[!UICONTROL Por hora]**: programe las exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

1. Utilice el **[!UICONTROL Hora]** selector para elegir la hora del día, en [!DNL UTC] formato, momento en el que se debe realizar la exportación.

   >[!IMPORTANT]
   >
   >Debido al modo en que se configuran los procesos internos del Experience Platform, es posible que la primera exportación de archivo incremental o completa no contenga todos los datos de relleno. <br> <br> Para garantizar una exportación de datos de relleno completa y más actualizada tanto para archivos completos como incrementales, Adobe recomienda configurar la primera hora de exportación de archivo después de las 12 PM GMT del día siguiente. Esta limitación se solucionará en futuras versiones.

1. Utilice el **[!UICONTROL Fecha]** selector para elegir el intervalo en el que debe realizarse la exportación. La práctica recomendada es establecer las fechas de inicio y finalización para que se alineen con la duración de las campañas en las plataformas de flujo descendente.

   >[!IMPORTANT]
   >
   >El último día del intervalo no se incluye en las exportaciones. Por ejemplo, si selecciona un intervalo del 4 al 11 de enero, la última exportación de archivos se realizará el 10 de enero.

1. Seleccionar **[!UICONTROL Crear]** para guardar la programación.

### Configurar nombres de archivo {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Configurar nombre de archivo"
>abstract="Para los destinos basados en archivos, se genera un nombre de archivo único por segmento. Utilice el editor de nombres de archivo para crear y editar un nombre de archivo único o mantener el nombre predeterminado."

Para la mayoría de los destinos, los nombres de archivo predeterminados constan del nombre de destino, el ID de segmento y un indicador de fecha y hora. Por ejemplo, puede editar los nombres de archivo exportados para distinguir entre diferentes campañas o para que el tiempo de exportación de datos se anexe a los archivos. Tenga en cuenta que algunos desarrolladores de destinos pueden elegir que se muestren opciones de adición de nombres de archivo predeterminadas diferentes para sus destinos.

Seleccione el icono de lápiz para abrir una ventana modal y editar los nombres de archivo. Los nombres de archivo están limitados a 255 caracteres.

>[!NOTE]
>
>La siguiente imagen muestra cómo se pueden editar los nombres de archivo para [!DNL Amazon S3] destinos, pero el proceso es idéntico para todos los destinos por lotes (por ejemplo, SFTP, [!DNL Azure Blob Storage], o [!DNL Google Cloud Storage]).

![Imagen que resalta el icono de lápiz, que se utiliza para configurar los nombres de archivo.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

En el editor de nombres de archivo, puede seleccionar diferentes componentes para agregarlos al nombre del archivo.

![Imagen que muestra todas las opciones de nombre de archivo disponibles.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

El nombre de destino y el ID de segmento no se pueden eliminar de los nombres de archivo. Además de esto, puede agregar lo siguiente:

| Opción de nombre de archivo | Descripción |
|---------|----------|
| **[!UICONTROL Nombre del segmento]** | Nombre del segmento exportado. |
| **[!UICONTROL Fecha y hora]** | Seleccione entre añadir un `MMDDYYYY_HHMMSS` o una marca de tiempo Unix de 10 dígitos de la hora en la que se generan los archivos. Elija una de estas opciones si desea que los archivos tengan un nombre de archivo dinámico generado con cada exportación incremental. |
| **[!UICONTROL Texto personalizado]** | Cualquier texto personalizado que desee agregar a los nombres de archivo. |
| **[!UICONTROL ID de destino]** | El ID del flujo de datos de destino que utiliza para exportar el segmento. <br> **Nota**: Esta opción de adición de nombre de archivo solo está disponible para los clientes beta que participan en el programa beta de funcionalidad de exportación de archivos mejorada. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder al programa beta. |
| **[!UICONTROL Nombre del destino]** | Nombre del flujo de datos de destino que se utiliza para exportar el segmento. <br> **Nota**: Esta opción de adición de nombre de archivo solo está disponible para los clientes beta que participan en el programa beta de funcionalidad de exportación de archivos mejorada. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder al programa beta. |
| **[!UICONTROL Nombre de organización]** | Nombre de su organización en Experience Platform. <br> **Nota**: Esta opción de adición de nombre de archivo solo está disponible para los clientes beta que participan en el programa beta de funcionalidad de exportación de archivos mejorada. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder al programa beta. |
| **[!UICONTROL Nombre de la zona protegida]** | El ID de la zona protegida que utiliza para exportar el segmento. <br> **Nota**: Esta opción de adición de nombre de archivo solo está disponible para los clientes beta que participan en el programa beta de funcionalidad de exportación de archivos mejorada. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder al programa beta. |

{style="table-layout:auto"}

Seleccionar **[!UICONTROL Aplicar cambios]** para confirmar la selección.

>[!IMPORTANT]
> 
>Si no selecciona la opción **[!UICONTROL Fecha y hora]** , los nombres de archivo serán estáticos y el nuevo archivo exportado sobrescribirá el archivo anterior en su ubicación de almacenamiento con cada exportación. Cuando se ejecuta un trabajo de importación recurrente desde una ubicación de almacenamiento a una plataforma de marketing por correo electrónico, esta es la opción recomendada.

Cuando haya terminado de configurar todos los segmentos, seleccione **[!UICONTROL Siguiente]** para continuar.

## Seleccionar atributos de perfil {#select-attributes}

Para los destinos basados en perfiles, debe seleccionar los atributos de perfil que desea enviar al destino de destino.

1. En el **[!UICONTROL Seleccionar atributos]** página, seleccione **[!UICONTROL Añadir nuevo campo]**.

   ![Imagen que resalta el botón Añadir nuevo campo.](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Seleccione la flecha a la derecha de la **[!UICONTROL Campo de esquema]** entrada.

   ![Imagen que resalta cómo seleccionar un campo de origen.](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. En el **[!UICONTROL Seleccionar campo]** , seleccione los atributos XDM o las áreas de nombres de identidad que desee enviar al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   ![Imagen que muestra los distintos campos disponibles como campos de origen.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Para agregar más asignaciones, repita los pasos del uno al tres.

>[!NOTE]
>
> Adobe Experience Platform rellena previamente su selección con cuatro atributos recomendados y utilizados con frecuencia desde su esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

>[!IMPORTANT]
>
>Debido a una limitación conocida, actualmente no puede utilizar la variable **[!UICONTROL Seleccionar campo]** ventana para añadir `segmentMembership.status` a sus exportaciones de archivos. En su lugar, debe pegar manualmente el valor `xdm: segmentMembership.status` en el campo de esquema, como se muestra a continuación.
>
>![Grabación de pantalla que muestra la solución para los miembros de segmentos en el paso de asignación del flujo de trabajo de activación.](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Las exportaciones de archivos variarán de las siguientes maneras, dependiendo de si `segmentMembership.status` está seleccionado:
* Si la variable `segmentMembership.status` está seleccionado, los archivos exportados incluyen **[!UICONTROL Activo]** miembros en la instantánea completa inicial y **[!UICONTROL Activo]** y **[!UICONTROL Caducado]** miembros en exportaciones incrementales subsiguientes.
* Si la variable `segmentMembership.status` no está seleccionado, los archivos exportados solo incluyen **[!UICONTROL Activo]** miembros en la instantánea completa inicial y en las exportaciones incrementales posteriores.

![Imagen que muestra atributos recomendados rellenados previamente en el paso de asignación del flujo de trabajo de activación de segmentos.](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Atributos obligatorios {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Acerca de los atributos obligatorios"
>abstract="Seleccione los atributos de esquema XDM que deben incluir todos los perfiles exportados. Los perfiles sin la clave obligatoria no se exportan al destino. Al no seleccionar una clave obligatoria, se exportan todos los perfiles cualificados independientemente de sus atributos."

Un atributo obligatorio es una casilla de verificación activada por el usuario que garantiza que todos los registros de perfil contengan el atributo seleccionado. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico&#x200B;

Puede marcar los atributos como obligatorios para asegurarse de que [!DNL Platform] exporta únicamente los perfiles que incluyen el atributo específico. Como resultado, se puede utilizar como una forma adicional de filtrado. Marcar un atributo como obligatorio es **no** requerido.

Al no seleccionar un atributo obligatorio, se exportan todos los perfiles cualificados independientemente de sus atributos.

Se recomienda que uno de los atributos sea un [identificador único](../../destinations/catalog/email-marketing/overview.md#identity) desde el esquema. Para obtener más información sobre los atributos obligatorios, consulte la sección de identidad en la [Destinos de marketing por correo electrónico](../../destinations/catalog/email-marketing/overview.md#identity) documentación.

### Claves de deduplicación {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Acerca de las claves de deduplicación"
>abstract="Elimine varios registros del mismo perfil en los archivos de exportación seleccionando una clave de deduplicación. Seleccione una sola área de nombres o hasta dos atributos de esquema XDM como clave de deduplicación. Si no se selecciona una clave de deduplicación, es posible que se dupliquen entradas de perfil en los archivos de exportación."

Una clave de anulación de duplicación es una clave principal definida por el usuario que determina la identidad por la que los usuarios desean que se dedupliquen sus perfiles&#x200B;

Las claves de deduplicación eliminan la posibilidad de tener varios registros del mismo perfil en un archivo de exportación.

Existen tres formas de utilizar claves de deduplicación en [!DNL Platform]:

* Uso de un área de nombres de identidad única como [!UICONTROL clave de deduplicación]
* Uso de un único atributo de perfil de un [!DNL XDM] perfil como [!UICONTROL clave de deduplicación]
* Uso de una combinación de dos atributos de perfil de una variable [!DNL XDM] perfil como clave compuesta

>[!IMPORTANT]
>
> Puede exportar un área de nombres de identidad única a un destino y el área de nombres se establece automáticamente como clave de anulación de duplicación. No se permite enviar varias áreas de nombres a un destino.
> 
> No se puede utilizar una combinación de áreas de nombres de identidad y atributos de perfil como claves de anulación de duplicación.

### Ejemplo de deduplicación {#deduplication-example}

Este ejemplo ilustra el funcionamiento de la deduplicación en función de las claves de deduplicación seleccionadas.

Consideremos los dos perfiles siguientes.

**Perfil A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Perfil B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Caso de uso 1 de deduplicación: sin deduplicación {#deduplication-use-case-1}

Sin anulación de duplicación, el archivo de exportación contendría las siguientes entradas.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Caso de uso de deduplicación 2: deduplicación basada en el área de nombres de identidad {#deduplication-use-case-2}

Suponiendo la deduplicación por parte de [!DNL Email] , el archivo de exportación contendría las siguientes entradas. El perfil B es el más reciente que se clasifica para el segmento, por lo que es el único que se exporta.

| Correo electrónico* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Caso de uso de deduplicación 3: deduplicación basada en un único atributo de perfil {#deduplication-use-case-3}

Suponiendo la deduplicación por parte de `personal Email` , el archivo de exportación contendría la siguiente entrada. El perfil B es el más reciente que se clasifica para el segmento, por lo que es el único que se exporta.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Caso de uso 4 de deduplicación: deduplicación basada en dos atributos de perfil {#deduplication-use-case-4}

Suponiendo la deduplicación por la clave compuesta `personalEmail + lastName`, el archivo de exportación contendría las siguientes entradas.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


El Adobe recomienda seleccionar un área de nombres de identidad como una [!DNL CRM ID] o la dirección de correo electrónico como clave de deduplicación para garantizar que todos los registros de perfil se identifiquen de forma exclusiva.

>[!NOTE]
> 
>Si se han aplicado etiquetas de uso de datos a ciertos campos dentro de un conjunto de datos (en lugar de a todo el conjunto de datos), la aplicación de esas etiquetas de nivel de campo en la activación se produce en las siguientes condiciones:
>
>* Los campos se utilizan en la definición del segmento.
>* Los campos se configuran como atributos proyectados para el destino final.
>
> Por ejemplo, si el campo `person.name.firstName` tiene ciertas etiquetas de uso de datos que entran en conflicto con la acción de marketing del destino. En el paso de revisión, se mostrará una infracción de la política de uso de datos. Para obtener más información, consulte [Administración de datos en Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Asignación de (beta) {#mapping}

>[!IMPORTANT]
> 
>Determinados clientes de la versión beta pueden ver y mejorar **[!UICONTROL Asignación]** paso que sustituye al [Seleccionar atributos de perfil](#select-attributes) paso descrito anteriormente. Esta nueva **[!UICONTROL Asignación]** Este paso le permite editar los encabezados de los archivos exportados con los nombres personalizados que desee.
> 
> La funcionalidad y la documentación están sujetas a cambios. Póngase en contacto con su representante de Adobe o con el Servicio de atención al cliente si desea acceder a este programa beta.

En este paso, debe seleccionar los atributos de perfil que desea añadir a los archivos exportados al destino de destino. Para seleccionar atributos e identidades de perfil para la exportación:

1. En el **[!UICONTROL Asignación]** página, seleccione **[!UICONTROL Añadir nuevo campo]**.

   ![Agregue el nuevo control de campo resaltado en el flujo de trabajo de asignación.](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Seleccione la flecha a la derecha de la **[!UICONTROL Campo de origen]** entrada.

   ![Seleccione el control de campo de origen resaltado en el flujo de trabajo de asignación.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. En el **[!UICONTROL Seleccionar campo de origen]** , seleccione los atributos e identidades de perfil que desee incluir en los archivos exportados al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   >[!TIP]
   > 
   >Puede utilizar el campo de búsqueda para reducir la selección, como se muestra en la siguiente imagen.

   ![Ventana modal que muestra atributos de perfil que se pueden exportar al destino.](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. El campo seleccionado para la exportación ahora aparece en la vista de asignación. Si lo desea, puede editar el nombre del encabezado en el archivo exportado. Para ello, seleccione el icono en el campo de destinatario.

   ![Ventana modal que muestra atributos de perfil que se pueden exportar al destino.](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. En el **[!UICONTROL Seleccionar campo de destino]** , escriba el nombre que desee para el encabezado en el archivo exportado y, a continuación, elija **[!UICONTROL Seleccionar]**.

   ![Ventana modal que muestra un nombre descriptivo escrito para un encabezado.](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. El campo seleccionado para la exportación aparece ahora en la vista de asignación y muestra el encabezado editado en el archivo exportado.

   ![Ventana modal que muestra atributos de perfil que se pueden exportar al destino.](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Opcional) Puede seleccionar el campo exportado para que sea un [clave obligatoria](#mandatory-keys) o una [clave de deduplicación](#deduplication-keys).

   ![Ventana modal que muestra atributos de perfil que se pueden exportar al destino.](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Para agregar más campos para exportar, repita los pasos anteriores.

### Limitaciones conocidas {#known-limitations}

El nuevo **[!UICONTROL Asignación]** tiene las siguientes limitaciones conocidas:

#### El atributo de pertenencia a segmento no se puede seleccionar a través del flujo de trabajo de asignación

Debido a una limitación conocida, actualmente no puede utilizar la variable **[!UICONTROL Seleccionar campo]** ventana para añadir `segmentMembership.status` a sus exportaciones de archivos. En su lugar, debe pegar manualmente el valor `xdm: segmentMembership.status` en el campo de esquema, como se muestra a continuación.

![Grabación de pantalla que muestra la solución para los miembros de segmentos en el paso de asignación del flujo de trabajo de activación.](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)

Las exportaciones de archivos variarán de las siguientes maneras, dependiendo de si `segmentMembership.status` está seleccionado:
* Si la variable `segmentMembership.status` está seleccionado, los archivos exportados incluyen **[!UICONTROL Activo]** miembros en la instantánea completa inicial y **[!UICONTROL Activo]** y **[!UICONTROL Caducado]** miembros en exportaciones incrementales subsiguientes.
* Si la variable `segmentMembership.status` no está seleccionado, los archivos exportados solo incluyen **[!UICONTROL Activo]** miembros en la instantánea completa inicial y en las exportaciones incrementales posteriores.

#### Actualmente no se pueden seleccionar áreas de nombres de identidad para las exportaciones

Actualmente no se admite la selección de áreas de nombres de identidad para exportar, como se muestra en la imagen siguiente. Si se seleccionan áreas de nombres de identidad para la exportación, se producirá un error en la variable **[!UICONTROL Revisar]** paso.

![Asignación no compatible que muestra exportaciones de identidad](/help/destinations/assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

Como solución temporal si necesita agregar áreas de nombres de identidad a los archivos exportados durante la versión beta, puede:
* Utilice los destinos de almacenamiento en la nube heredados para los flujos de datos donde desee incluir áreas de nombres de identidad en las exportaciones
* Cargue identidades como atributos en Experience Platform para luego exportarlas a sus destinos de almacenamiento en la nube.

## Consulte {#review}

En el **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccionar **[!UICONTROL Cancelar]** para romper el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección y comenzar a enviar datos al destino.

![Resumen de la selección en el paso de revisión.](/help/destinations/assets/ui/activate-batch-profile-destinations/review.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_viewApplicableConsentPolicies"
>title="Ver directivas de consentimiento aplicables"
>abstract="Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Este control está deshabilitado si su empresa no tiene acceso a los SKU mencionados anteriormente."

Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Más información [evaluación de directiva de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el **[!UICONTROL Revisar]** paso, el Experience Platform también comprueba si hay alguna infracción de la política de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de segmentos hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, consulte [infracciones de políticas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección documentación de control de datos.

![infracción de política de datos](../assets/common/data-policy-violation.png)

### Filtrar segmentos. {#filter-segments}

Además, en este paso puede utilizar los filtros disponibles en la página para mostrar solo los segmentos cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de segmento disponibles en el paso de revisión.](/help/destinations/assets/ui/activate-batch-profile-destinations/filter-segments-batch-review.gif)

Si está satisfecho con la selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y comenzar a enviar datos al destino.

## Verificar activación de segmento {#verify}

Para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube, Adobe Experience Platform crea un `.csv` en la ubicación de almacenamiento proporcionada. Es de esperar que se cree un nuevo archivo en su ubicación de almacenamiento según la programación establecida en el flujo de trabajo. A continuación se muestra el formato de archivo predeterminado, pero puede [editar los componentes del nombre de archivo](#file-names):
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Por ejemplo, si seleccionara una frecuencia de exportación diaria, los archivos que recibiría en tres días consecutivos podrían tener este aspecto:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de la activación correcta. Para comprender cómo están estructurados los archivos exportados, puede [descargar un archivo .csv de ejemplo](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Este archivo de muestra incluye los atributos de perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, y `personalEmail.address`.
