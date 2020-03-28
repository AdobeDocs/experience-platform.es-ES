---
title: Activar perfiles y segmentos en un destino
seo-title: Activar perfiles y segmentos en un destino
description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
seo-description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Activar perfiles y segmentos en un destino

Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado correctamente un destino](/help/rtcdp/destinations/assets/connect-destination.png). Si aún no lo ha hecho, vaya al catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, busque los destinos admitidos y configure uno o varios destinos.

## Activar datos {#activate-data}

1. En **[!UICONTROL Destinations > Browse]**, seleccione el destino en el que desea activar los segmentos.
2. Haga clic en el nombre del destino. Esto le lleva al flujo Activar.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Edit activation]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.
3. Select **[!UICONTROL Activate]**;
4. En el flujo **[!UICONTROL Activate destination]** de trabajo, en la **[!UICONTROL Select Segments]** página, seleccione qué segmentos enviar al destino.
   ![segmentos a destino](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condicional*. Este paso solo se aplica a segmentos asignados a destinos de marketing por correo electrónico. <br> En la **[!UICONTROL Destination Attributes]** página, seleccione **[!UICONTROL Add new field]** y seleccione los atributos que desee enviar al destino.
Se recomienda que uno de los atributos sea un identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) único del esquema de unión. Para obtener más información sobre los atributos obligatorios, consulte Identidad en el artículo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) correo electrónico.
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. En la **[!UICONTROL Schedule]** página puede ver la fecha de inicio para enviar datos al destino, así como la frecuencia con la que se envían datos al destino.
7. En la **[!UICONTROL Review]** página, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancel]** para desglosar el flujo, **[!UICONTROL Back]** para modificar la configuración o **[!UICONTROL Finish]** para confirmar la selección y el inicio al enviar datos al destino.

![confirmación-selección](/help/rtcdp/destinations/assets/confirm-selection.png)

## Editar activación {#edit-activation}

Siga los pasos a continuación para editar los flujos de activación existentes en CDP en tiempo real:

1. Seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda, haga clic en la **[!UICONTROL Browse]** ficha y, a continuación, haga clic en el nombre del destino.
2. Seleccione **[!UICONTROL Edit activation]** en el carril derecho para cambiar qué segmentos enviar al destino.

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

### Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube

Para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube, CDP en tiempo real de Adobe crea un archivo `.txt` o `.csv` delimitado por tabuladores en la ubicación de almacenamiento proporcionada. Se espera que cada día se cree un nuevo archivo en la ubicación del almacenamiento. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Los archivos que recibiría en tres días consecutivos podrían tener este aspecto:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

La presencia de estos archivos en la ubicación del almacenamiento es la confirmación de la activación correcta.

### Destinos publicitarios

Compruebe el destino de publicidad correspondiente en el que está activando los datos. Si la activación se ha realizado correctamente, las audiencias se rellenan en la plataforma de publicidad.

## Deshabilitar activación {#disable-activation}

Para deshabilitar un flujo de activación existente, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinations]** en la barra de navegación izquierda, haga clic en la **[!UICONTROL Browse]** ficha y, a continuación, haga clic en el nombre del destino.
2. Haga clic en el **[!UICONTROL Enabled]** control del carril derecho para cambiar el estado del flujo de activación.
3. En la ventana **Actualizar estado** de flujo de datos, seleccione **Confirmar** para desactivar el flujo de activación.

