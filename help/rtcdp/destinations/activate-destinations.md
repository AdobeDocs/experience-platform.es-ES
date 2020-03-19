---
title: Activar perfiles y segmentos en un destino
seo-title: Activar perfiles y segmentos en un destino
description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
seo-description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
translation-type: tm+mt
source-git-commit: 73925aa59f9981d8945fb0be6c4924e1831cf902

---


# Activar perfiles y segmentos en un destino

Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado correctamente un destino](/help/rtcdp/destinations/assets/connect-destination.png). Si aún no lo ha hecho, vaya al catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, busque los destinos admitidos y configure uno o varios destinos.

## Activar datos {#activate-data}

1. En **Destinos > Examinar**, seleccione el destino en el que desea activar los segmentos.
2. Haga clic en el nombre del destino. Esto le lleva al flujo Activar.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **Editar activación** en el carril derecho y siga los pasos a continuación para modificar los detalles de activación.
3. Seleccione **Activar**;
4. En el asistente **Activar destino** , en la página **Seleccionar segmentos** , seleccione los segmentos que desea enviar al destino.
   ![segmentos a destino](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condicional*. Este paso solo se aplica a segmentos asignados a destinos de marketing por correo electrónico. <br> En la página Atributos **de** destino, seleccione **Agregar nuevo campo** y seleccione los atributos que desee enviar al destino.
Se recomienda que uno de los atributos sea un identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) único del esquema de unión. Para obtener más información sobre los atributos obligatorios, consulte Identidad en el artículo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) correo electrónico.
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. En la página **Programar** , puede ver la fecha de inicio para enviar datos al destino, así como la frecuencia de envío de datos al destino.
7. En la página **Revisar** , puede ver un resumen de su selección. Seleccione **Cancelar** para desglosar el flujo, **Atrás** para modificar la configuración o **Finalizar** para confirmar la selección y empezar a enviar datos al destino.

![confirmación-selección](/help/rtcdp/destinations/assets/confirm-selection.png)

## Editar activación {#edit-activation}

Siga los pasos a continuación para editar los flujos de activación existentes en CDP en tiempo real:

1. Seleccione **Destinos** en la barra de navegación izquierda, luego haga clic en la ficha **Examinar** y, a continuación, haga clic en el nombre del destino.
2. Seleccione **[!UICONTROL Editar activación]** en el carril derecho para cambiar los segmentos que se van a enviar al destino.

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

### Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube

Para destinos de marketing por correo electrónico y destinos de almacenamiento en la nube, CDP en tiempo real de Adobe crea un archivo `.txt` `.csv` o un archivo delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Se espera que cada día se cree un nuevo archivo en la ubicación de almacenamiento. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Los archivos que recibiría en tres días consecutivos podrían tener este aspecto:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La presencia de estos archivos en la ubicación de almacenamiento es la confirmación de la activación correcta.

### Destinos publicitarios

Compruebe el destino de publicidad correspondiente en el que está activando los datos. Si la activación se ha realizado correctamente, las audiencias se rellenan en la plataforma de publicidad.

## Deshabilitar activación {#disable-activation}

Para deshabilitar un flujo de activación existente, siga los pasos a continuación:

1. Seleccione **Destinos** en la barra de navegación izquierda, luego haga clic en la ficha **Examinar** y, a continuación, haga clic en el nombre del destino.
2. Haga clic en el control **[!UICONTROL Habilitado]** en el carril derecho para cambiar el estado del flujo de activación.
3. En la ventana **Actualizar estado** del flujo de datos, seleccione **Confirmar** para desactivar el flujo de activación.

