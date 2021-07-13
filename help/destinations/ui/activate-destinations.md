---
keywords: activar destino;activar destinos;activar datos
title: Activar perfiles y segmentos en un destino
type: Tutorial
seo-title: Activar perfiles y segmentos en un destino
description: Active los datos que tiene en Adobe Experience Platform asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
seo-description: Active los datos que tiene en Adobe Experience Platform asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
exl-id: c3792046-ffa8-4851-918f-98ced8b8a835
source-git-commit: 4ad261c4ca5878f7ef5abb2c2957b5714cf3101a
workflow-type: tm+mt
source-wordcount: '2888'
ht-degree: 0%

---

# Activar perfiles y segmentos en un destino

## Información general {#overview}

Active los datos que tiene en [!DNL Adobe Experience Platform] asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), busque los destinos admitidos y configure uno o más destinos.

## Activar datos {#activate-data}

Los pasos del flujo de trabajo de activación varían ligeramente entre los tipos de destino. A continuación se describe el flujo de trabajo completo para todos los tipos de destino.

## Seleccione a qué destino activar los datos {#select-destination}

Se aplica a: Todos los destinos

En la interfaz de usuario de Adobe Experience Platform, vaya a **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** y haga clic en el botón **[!UICONTROL Activate]** correspondiente al destino en el que desea activar los segmentos, como se muestra en la imagen siguiente.

![activar en destino](../assets/ui/activate-destinations/browse-tab-activate.png)

Siga los pasos de la siguiente sección para seleccionar los segmentos que desea activar.

## [!UICONTROL Seleccionar paso ] de segmentos {#select-segments}

Se aplica a: Todos los destinos

![Paso Seleccionar segmentos](../assets/ui/activate-destinations/select-segments-icon.png)

En el flujo de trabajo **[!UICONTROL Activate destination]** , en la página **[!UICONTROL Select Segments]**, seleccione uno o varios segmentos para activarlos en el destino. Seleccione **[!UICONTROL Siguiente]** para continuar con el paso siguiente.

![segmentos a destino](../assets/ui/activate-destinations/email-select-segments.png)

##  Paso de asignación {#mapping}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformación"
>abstract="Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform los hash automáticamente en la activación."

Se aplica a: destinos sociales y destino publicitario de Google Customer Match

![Paso de asignación de identidad](../assets/ui/activate-destinations/identity-mapping-icon.png)

Para destinos sociales, debe seleccionar atributos de origen o áreas de nombres de identidad para asignarlos como identidades de destino en el destino.

## Ejemplo: activación de datos de audiencia en [!DNL Facebook Custom Audience] {#example-facebook}

A continuación se muestra un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Facebook].

Selección de campos de origen:

* Seleccione el espacio de nombres `Email` como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente sobre la ingesta de datos a [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de correo electrónico](../catalog/social/facebook.md#email-hashing-requirements).
* Seleccione el espacio de nombres `PHONE_E.164` como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] realizará un hash de los números de teléfono para cumplir con los  [!DNL Facebook] requisitos.
* Seleccione el espacio de nombres `Phone_SHA256` como identidad de origen si ha hash los números de teléfono sobre la ingesta de datos en [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de números de teléfono](../catalog/social/facebook.md#phone-number-hashing-requirements).
* Seleccione el espacio de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el espacio de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el espacio de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el espacio de nombres `Phone_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `PHONE_E.164` o `Phone_SHA256`.
* Seleccione los espacios de nombres `IDFA` o `GAID` como identidad de destino cuando los espacios de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el espacio de nombres `Extern_ID` como identidad de destino cuando el espacio de nombres de origen sea personalizado.

![Asignación de identidad](../assets/ui/activate-destinations/identity-mapping.png)

Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.

Los datos de origen de atributos no se colocan automáticamente en hash. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación.
![Transformación de asignación de identidad](../assets/ui/activate-destinations/identity-mapping-transformation.png)

 

## Ejemplo: activación de datos de audiencia en [!DNL Google Customer Match] {#example-gcm}

Este es un ejemplo de asignación de identidad correcta al activar datos de audiencia en [!DNL Google Customer Match].

Selección de campos de origen:

* Seleccione el espacio de nombres `Email` como identidad de origen si las direcciones de correo electrónico que utiliza no tienen valores hash.
* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de origen si ha pasado por hash las direcciones de correo electrónico del cliente sobre la ingesta de datos a [!DNL Platform], de acuerdo con los [!DNL Google Customer Match] [requisitos de hash de correo electrónico](../catalog/social/../advertising/google-customer-match.md).
* Seleccione el espacio de nombres `PHONE_E.164` como identidad de origen si los datos están formados por números de teléfono sin hash. [!DNL Platform] realizará un hash de los números de teléfono para cumplir con los  [!DNL Google Customer Match] requisitos.
* Seleccione el espacio de nombres `Phone_SHA256_E.164` como identidad de origen si ha hash los números de teléfono sobre la ingesta de datos en [!DNL Platform], de acuerdo con los [!DNL Facebook] [requisitos de hash de números de teléfono](../catalog/social/../advertising/google-customer-match.md).
* Seleccione el espacio de nombres `IDFA` como identidad de origen si los datos constan de [!DNL Apple] ID de dispositivo.
* Seleccione el espacio de nombres `GAID` como identidad de origen si los datos constan de [!DNL Android] ID de dispositivo.
* Seleccione el espacio de nombres `Custom` como identidad de origen si los datos constan de otro tipo de identificadores.

Selección de campos de destino:

* Seleccione el espacio de nombres `Email_LC_SHA256` como identidad de destino cuando los espacios de nombres de origen sean `Email` o `Email_LC_SHA256`.
* Seleccione el espacio de nombres `Phone_SHA256_E.164` como identidad de destino cuando los espacios de nombres de origen sean `PHONE_E.164` o `Phone_SHA256_E.164`.
* Seleccione los espacios de nombres `IDFA` o `GAID` como identidad de destino cuando los espacios de nombres de origen sean `IDFA` o `GAID`.
* Seleccione el espacio de nombres `User_ID` como identidad de destino cuando el espacio de nombres de origen sea personalizado.

![Asignación de identidad](../assets/ui/activate-destinations/identity-mapping-gcm.png)

Los datos de espacios de nombres sin hash se colocan automáticamente en hash mediante [!DNL Platform] al activarlos.

Los datos de origen de atributos no se colocan automáticamente en hash. Cuando el campo de origen contiene atributos sin hash, marque la opción **[!UICONTROL Apply transformation]** para que [!DNL Platform] hash automáticamente los datos en la activación.
![Transformación de asignación de identidad](../assets/ui/activate-destinations/identity-mapping-gcm-transformation.png)

## **** Paso de programación {#scheduling}

Se aplica a: Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube

![Paso de programación](../assets/ui/activate-destinations/scheduling-icon.png)

[!DNL Adobe Experience Platform] exporta datos para destinos de marketing por correo electrónico y almacenamiento en la nube en forma de  [!DNL CSV] archivos. En el paso **[!UICONTROL Scheduling]**, puede configurar la programación y los nombres de archivo para cada segmento que exporte. La configuración de la programación es obligatoria, pero la configuración del nombre del archivo es opcional.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automáticamente los archivos de exportación en 5 millones de registros (filas) por archivo. Cada fila representa un perfil.
>
>Los nombres de archivos divididos se añaden con un número que indica que el archivo forma parte de una exportación más grande, como por ejemplo: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Seleccione el botón **[!UICONTROL Create schedule]** correspondiente al segmento que desea enviar al destino.

![Botón Crear programación](../assets/ui/activate-destinations/create-schedule-button.png)

### Exportar archivos completos {#export-full-files}

Seleccione **[!UICONTROL Exportar archivos completos]** para que los archivos exportados contengan una instantánea completa de todos los perfiles aptos para ese segmento.

![Exportar archivos completos](../assets/ui/activate-destinations/export-full-files.png)

1. Utilice el selector **[!UICONTROL Frequency]** para elegir entre exportaciones únicas (**[!UICONTROL Once]**) o **[!UICONTROL Daily]**. Exportar un archivo completo **[!UICONTROL Daily]** exporta el archivo todos los días desde la fecha de inicio hasta la fecha de finalización a las 12:00 AM UTC (7:00 PM EST).
2. Utilice el selector **[!UICONTROL Time]** para elegir la hora del día, en formato [!DNL UTC], en la que se debe realizar la exportación. Exportar un archivo **[!UICONTROL Daily]** exporta el archivo todos los días desde la fecha de inicio hasta la fecha de finalización en el momento seleccionado.

   >[!IMPORTANT]
   >
   >La opción para exportar archivos a una hora determinada del día está actualmente en fase beta y solo está disponible para un número determinado de clientes.<br> <br> Debido a la forma en que se configuran los procesos de Experience Platform internos, es posible que la primera exportación incremental o completa de archivos no contenga todos los datos de relleno.  <br> <br> Para garantizar una exportación de datos de relleno completa y actualizada tanto para archivos completos como incrementales, Adobe recomienda configurar la hora de exportación del primer archivo después de las 22 PM GMT del día siguiente. Se trata de una limitación que se abordará en futuras versiones.

3. Utilice el selector **[!UICONTROL Fecha]** para elegir el día o el intervalo en el que se debe realizar la exportación.
4. Seleccione **[!UICONTROL Crear]** para guardar la programación.

>[!IMPORTANT]
>
>Actualmente no se puede cambiar la programación de exportación de archivos para segmentos que ya se han exportado. Para volver a exportar segmentos con una programación diferente, debe crear una nueva instancia de destino. Se trata de una limitación que se abordará en futuras versiones.

### Exportar archivos incrementales {#export-incremental-files}

Seleccione **[!UICONTROL Exportar archivos incrementales]** para que los archivos exportados contengan solo los perfiles que cumplen los requisitos para ese segmento desde la última exportación.

>[!IMPORTANT]
>
>El primer archivo incremental exportado incluye todos los perfiles aptos para un segmento que funcionan como relleno.

![Exportar archivos incrementales](../assets/ui/activate-destinations/export-incremental-files.png)

1. Utilice el selector **[!UICONTROL Frequency]** para elegir entre las exportaciones **[!UICONTROL Daily]** o **[!UICONTROL Por hora]**. Exportar un archivo incremental **[!UICONTROL Daily]** exporta el archivo todos los días desde la fecha de inicio hasta la fecha de finalización a las 12:00 PM UTC (7:00 AM EST).
   * Al seleccionar **[!UICONTROL Por hora]**, utilice el selector **[!UICONTROL Cada]** para elegir entre las opciones de horas **[!UICONTROL 3]**, **[!UICONTROL 6]**, **[!UICONTROL 8]** y **[!UICONTROL 12]**.

      >[!IMPORTANT]
      >
      >La opción para exportar archivos incrementales cada 3, 6, 8 o 12 horas está actualmente en fase beta y solo está disponible para un número determinado de clientes. Los clientes que no sean de la versión beta pueden exportar archivos incrementales una vez al día.

2. Utilice el selector **[!UICONTROL Time]** para elegir la hora del día, en formato [!DNL UTC], en la que se debe realizar la exportación.

   >[!IMPORTANT]
   >
   >La opción para seleccionar la hora del día para la exportación solo está disponible para un número determinado de clientes. <br> <br> Debido a la forma en que se configuran los procesos de Experience Platform internos, es posible que la primera exportación incremental o completa de archivos no contenga todos los datos de relleno.  <br> <br> Para garantizar una exportación de datos de relleno completa y actualizada tanto para archivos completos como incrementales, Adobe recomienda configurar la hora de exportación del primer archivo después de las 22 PM GMT del día siguiente. Se trata de una limitación que se abordará en futuras versiones.

3. Utilice el selector **[!UICONTROL Fecha]** para elegir el día o el intervalo en el que se debe realizar la exportación.
4. Seleccione **[!UICONTROL Crear]** para guardar la programación.

>[!IMPORTANT]
>
>Actualmente no se puede cambiar la programación de exportación de archivos para segmentos que ya se han exportado. Para volver a exportar segmentos con una programación diferente, debe crear una nueva instancia de destino. Se trata de una limitación que se abordará en futuras versiones.

### Configurar nombres de archivo {#file-names}

Los nombres de archivo predeterminados constan del nombre de destino, el ID de segmento y un indicador de fecha y hora. Por ejemplo, puede editar los nombres de archivo exportados para distinguir entre diferentes campañas o para que se añada el tiempo de exportación de datos a los archivos.

Seleccione el icono de lápiz para abrir una ventana modal y editar los nombres de archivo. Los nombres de archivo están limitados a 255 caracteres.

![configurar nombre de archivo](../assets/ui/activate-destinations/configure-name.png)

En el editor de nombres de archivo, puede seleccionar diferentes componentes para agregarlos al nombre del archivo.

![editar opciones de nombre de archivo](../assets/ui/activate-destinations/activate-workflow-configure-step-2.png)

El nombre de destino y el ID de segmento no se pueden eliminar de los nombres de archivo. Además de esto, puede agregar lo siguiente:

* **[!UICONTROL Nombre]** del segmento: Puede anexar el nombre del segmento al nombre del archivo.
* **[!UICONTROL Fecha y hora]**: Seleccione entre añadir un  `MMDDYYYY_HHMMSS` formato o una marca de tiempo de 10 dígitos Unix del momento en que se generan los archivos. Elija una de estas opciones si desea que los archivos tengan un nombre de archivo dinámico generado con cada exportación incremental.
* **[!UICONTROL Texto]** personalizado: Agregue texto personalizado a los nombres de archivo.

Seleccione **[!UICONTROL Aplicar cambios]** para confirmar la selección.

>[!IMPORTANT]
> 
>Si no selecciona el componente **[!UICONTROL Fecha y hora]**, los nombres de archivo serán estáticos y el nuevo archivo exportado sobrescribirá el archivo anterior en su ubicación de almacenamiento con cada exportación. Cuando se ejecuta un trabajo de importación recurrente desde una ubicación de almacenamiento a una plataforma de marketing por correo electrónico, esta es la opción recomendada.

Una vez que haya terminado de configurar todos los segmentos, seleccione **[!UICONTROL Siguiente]** para continuar.

## **[!UICONTROL Paso de]** programación de segmentos {#segment-schedule}

Se aplica a: destinos publicitarios, destinos sociales

![paso de programación de segmentos](../assets/ui/activate-destinations/segment-schedule-icon.png)

En la página **[!UICONTROL Programación del segmento]** puede establecer la fecha de inicio para enviar datos al destino y la frecuencia de envío de datos al destino.

>[!IMPORTANT]
>
>Para destinos sociales, debe seleccionar el origen de la audiencia en este paso. Solo puede continuar con el paso siguiente después de seleccionar una de las opciones de la imagen siguiente.

![Origen de audiencia de facebook](../assets/catalog/social/facebook/facebook-origin-audience.png)

>[!IMPORTANT]
>
>Para Google Customer Match, debe proporcionar el [!UICONTROL ID de la aplicación] en este paso, al activar los segmentos [!DNL IDFA] o [!DNL GAID].

![introducir id de aplicación](../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

## **[!UICONTROL Seleccionar paso de]** atributos {#select-attributes}

Se aplica a: destinos de marketing por correo electrónico y destinos de almacenamiento en la nube

![paso seleccionar atributos](../assets/ui/activate-destinations/select-attributes-icon.png)

En la página **[!UICONTROL Select attributes]**, seleccione **[!UICONTROL Add new field]** y elija los atributos que desea enviar al destino.

>[!NOTE]
>
> Adobe Experience Platform prefiere la selección con cuatro atributos recomendados y utilizados comúnmente del esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Las exportaciones de archivos variarán de las siguientes maneras, en función de si se selecciona `segmentMembership.status`:
* Si se selecciona el campo `segmentMembership.status`, los archivos exportados incluyen **[!UICONTROL miembros activos]** en la instantánea completa inicial y miembros **[!UICONTROL activos]** y **[!UICONTROL caducados]** en las exportaciones incrementales posteriores.
* Si el campo `segmentMembership.status` no está seleccionado, los archivos exportados incluyen solo miembros **[!UICONTROL activos]** en la instantánea completa inicial y en las exportaciones incrementales posteriores.

![atributos recomendados](../assets/ui/activate-destinations/mandatory-deduplication.png)

### Atributos obligatorios {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Acerca de los atributos obligatorios"
>abstract="Seleccione los atributos de esquema XDM que deben incluir todos los perfiles exportados. Los perfiles sin la clave obligatoria no se exportan al destino. Al no seleccionar una clave obligatoria, se exportan todos los perfiles cualificados independientemente de sus atributos."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Más información en la documentación"

Puede marcar los atributos como obligatorios para asegurarse de que [!DNL Platform] exporta solo los perfiles que incluyen el atributo específico. Como resultado, se puede utilizar como una forma adicional de filtrado. Marcar un atributo como obligatorio es **no** obligatorio.

Al no seleccionar un atributo obligatorio, se exportan todos los perfiles cualificados independientemente de sus atributos.

Se recomienda que uno de los atributos sea un [identificador único](../../destinations/catalog/email-marketing/overview.md#identity) del esquema. Para obtener más información sobre los atributos obligatorios, consulte la sección de identidad en la documentación [Destinos de marketing por correo electrónico](../../destinations/catalog/email-marketing/overview.md#identity) .

### Claves de deduplicación {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Acerca de las claves de deduplicación"
>abstract="Elimine varios registros del mismo perfil en los archivos de exportación seleccionando una clave de deduplicación. Seleccione un solo espacio de nombres o hasta dos atributos de esquema XDM como clave de deduplicación. Si no se selecciona una clave de deduplicación, es posible que se dupliquen entradas de perfil en los archivos de exportación."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Más información en la documentación"

>[!IMPORTANT]
>
>La opción para utilizar claves de deduplicación se encuentra actualmente en fase beta y solo está disponible para un número determinado de clientes.

Las claves de deduplicación eliminan la posibilidad de tener varios registros del mismo perfil en un archivo de exportación.

Existen tres maneras de utilizar las claves de deduplicación en [!DNL Platform]:

* Uso de un solo área de nombres de identidad como [!UICONTROL clave de deduplicación]
* Uso de un atributo de perfil único de un perfil [!DNL XDM] como [!UICONTROL clave de deduplicación]
* Uso de una combinación de dos atributos de perfil de un perfil [!DNL XDM] como clave compuesta

>[!IMPORTANT]
>
> Puede exportar un solo área de nombres de identidad a un destino y el área de nombres se establece automáticamente como clave de deduplicación. No se admite el envío de varias áreas de nombres a un destino.
> 
> No puede utilizar una combinación de áreas de nombres de identidad y atributos de perfil como claves de deduplicación.

### Ejemplo de deduplicación {#deduplication-example}

Este ejemplo ilustra cómo funciona la deduplicación, según las claves de deduplicación seleccionadas.

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
        "status": "existing",
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
        "status": "existing",
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

### Caso de uso de deduplicación 1: sin deduplicación

Si no se utiliza ninguna deduplicación, el archivo de exportación contendría las siguientes entradas.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Caso de uso de deduplicación 2: deduplicación basada en el área de nombres de identidad

Suponiendo que el espacio de nombres [!DNL Email] deduplique, el archivo de exportación contendría las siguientes entradas. El Perfil B es el último que cumple los requisitos para el segmento, por lo que es el único que se exporta.

| Correo electrónico* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Caso de uso de deduplicación 3: deduplicación basada en un único atributo de perfil

Suponiendo que el atributo `personal Email` deduplique, el archivo de exportación contendría la siguiente entrada. El Perfil B es el último que cumple los requisitos para el segmento, por lo que es el único que se exporta.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Caso de uso de deduplicación 4: deduplicación basada en dos atributos de perfil (clave de deduplicación compuesta)

Suponiendo que la deduplicación se realice mediante la clave compuesta `personalEmail + lastName`, el archivo de exportación contendrá las siguientes entradas.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe recomienda seleccionar un área de nombres de identidad como [!DNL CRM ID] o una dirección de correo electrónico como clave de deduplicación para garantizar que todos los registros de perfil se identifiquen de forma única.

>[!NOTE]
> 
>Si se ha aplicado alguna etiqueta de uso de datos a ciertos campos dentro de un conjunto de datos (en lugar de todo el conjunto de datos), la aplicación de esas etiquetas de nivel de campo en la activación se produce bajo las siguientes condiciones:
>
>* Los campos se utilizan en la definición del segmento.
>* Los campos se configuran como atributos proyectados para el destino de destino.

>
> 
Por ejemplo, si el campo `person.name.firstName` tiene ciertas etiquetas de uso de datos que entran en conflicto con la acción de marketing del destino, en el paso de revisión se mostrará una infracción de la política de uso de datos. Para obtener más información, consulte [Control de datos en Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## **** Reviewstep {#review}

Se aplica a: todos los destinos

![paso de revisión](../assets/ui/activate-destinations/review-icon.png)

En la página **[!UICONTROL Revisar]**, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de control de datos.

![violación de la política de datos](../assets/common/data-policy-violation.png)

Si no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![confirm-selection](../assets/ui/activate-destinations/confirm-selection.png)

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

### Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube {#esp-and-cloud-storage}

Para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube, Adobe Experience Platform crea un archivo `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Espere a que se cree un nuevo archivo en la ubicación de almacenamiento todos los días. El formato de archivo predeterminado es:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Los archivos que recibiría en tres días consecutivos podrían tener este aspecto:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presencia de estos archivos en su ubicación de almacenamiento es la confirmación de que la activación se ha realizado correctamente. Para comprender cómo se estructuran los archivos exportados, puede [descargar un archivo .csv de muestra](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Este archivo de ejemplo incluye los atributos de perfil `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` y `personalEmail.address`.

## Destinos publicitarios

Compruebe su cuenta en el destino publicitario correspondiente al que está activando sus datos. Si la activación se ha realizado correctamente, las audiencias se rellenan en la plataforma de publicidad.

## Destinos sociales

Para [!DNL Facebook], una activación correcta significa que se crearía una audiencia personalizada [!DNL Facebook] mediante programación en [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). La pertenencia a segmentos en la audiencia se agregaría y eliminaría ya que los usuarios están cualificados o no cumplen los requisitos para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Experience Platform y [!DNL Facebook] admite los rellenos históricos de audiencias. Todas las cualificaciones históricas de segmentos se envían a [!DNL Facebook] al activar los segmentos en el destino.

## Desactivar activación {#disable-activation}

Para desactivar un flujo de activación existente, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda, haga clic en la pestaña **[!UICONTROL Browse]** y haga clic en el nombre de destino.
2. Haga clic en el control **[!UICONTROL Enabled]** en el carril derecho para cambiar el estado del flujo de activación.
3. En la ventana **Update data flow state**, seleccione **Confirm** para desactivar el flujo de activación.
