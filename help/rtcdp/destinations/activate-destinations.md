---
title: Activar perfiles y segmentos en un destino
seo-title: Activar perfiles y segmentos en un destino
description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
seo-description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
translation-type: tm+mt
source-git-commit: 237ca5fc950b46ae4718850ab1360cdf52b8b112
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 0%

---


# Activar perfiles y segmentos en un destino

Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado correctamente un destino](/help/rtcdp/destinations/assets/connect-destination.png). Si aún no lo ha hecho, vaya al catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, busque los destinos admitidos y configure uno o varios destinos.

## Activar datos {#activate-data}

1. En **[!UICONTROL Destinos > Examinar]**, seleccione el destino en el que desea activar los segmentos.
2. Haga clic en el nombre del destino. Esto le lleva al flujo Activar.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.
3. Seleccione **[!UICONTROL Activar]**;
4. En el flujo de trabajo **[!UICONTROL Activar destino]** , en la página **[!UICONTROL Seleccionar segmentos]** , seleccione los segmentos que desea enviar al destino.
   ![segmentos a destino](/help/rtcdp/destinations/assets/select-segments.png)
5. *Condicional*. Este paso varía en función del tipo de destino en el que se activan los segmentos. <br> Para los destinos *de marketing de* correo electrónico y los destinos *de almacenamiento de* nube, en la página **[!UICONTROL Seleccionar atributos]** , seleccione **[!UICONTROL Añadir nuevo campo]** y seleccione los atributos que desee enviar al destino.
Se recomienda que uno de los atributos sea un identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) único del esquema de unión. Para obtener más información sobre los atributos obligatorios, consulte Identidad en el artículo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) correo electrónico.
   ![destination-attributes](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Para los destinos ** sociales, en el paso Asignación **[!UICONTROL de]** identidad, puede seleccionar atributos de origen para asignarlos como identidades de destinatario en el destino. Este paso es opcional u obligatorio, según la identidad principal que utilice en el esquema. <br> 

   *Dirección de correo electrónico como identidad* principal: Si utiliza la dirección de correo electrónico como identidad principal en el esquema, puede omitir el paso de asignación de identidad, como se muestra a continuación:

   ![Dirección de correo electrónico como identidad](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Otro ID como identidad* principal: Si utiliza otro ID, como ID *de* recompensas o ID *de* lealtad, como identidad principal en el esquema, deberá asignar manualmente la dirección de correo electrónico del esquema de identidad como identidad de destinatario en el destino social, como se muestra a continuación:

   ![ID de fidelidad como identidad](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Seleccione `Email_LC_SHA256` como identidad de destinatario si ha marcado las direcciones de correo electrónico de los clientes en la ingesta de datos en Adobe Experience Platform, según los requisitos [de hash de](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)correo electrónico de Facebook. <br> Seleccione `Email` como identidad de destinatario si las direcciones de correo electrónico que utiliza no están marcadas por hash. CDP en tiempo real de Adobe realizará un hash de las direcciones de correo electrónico para cumplir con los requisitos de Facebook.

   ![asignación de identidad después de rellenar los campos](/help/rtcdp/destinations/assets/identity-mapping.png)

6. En la página Programación **[!UICONTROL de]** segmentos, puede ver la fecha de inicio para enviar datos al destino, así como la frecuencia con la que se envían datos al destino.

   >[!IMPORTANT]
   >
   >Para los destinos sociales, debe seleccionar el origen de la audiencia en este paso. Sólo puede continuar con el paso siguiente después de seleccionar una de las opciones de la siguiente imagen.

   ![elegir origen de datos](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. En la página **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio de envío de datos al destino.

![confirmación-selección](/help/rtcdp/destinations/assets/confirm-selection.png)

## Editar activación {#edit-activation}

Siga los pasos a continuación para editar los flujos de activación existentes en CDP en tiempo real:

1. Seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda, luego haga clic en la ficha **[!UICONTROL Examinar]** y, a continuación, haga clic en el nombre del destino.
2. Seleccione **[!UICONTROL Editar activación]** en el carril derecho para cambiar los segmentos que se van a enviar al destino.

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

### Destinos de redes sociales

Para Facebook, una activación exitosa significa que una audiencia personalizada de Facebook se crearía mediante programación en el Administrador [de publicidades de](https://www.facebook.com/adsmanager/manage/)Facebook. La pertenencia a segmentos en la audiencia se agregaría y eliminaría a medida que los usuarios estuvieran cualificados o descalificados para los segmentos activados.

>[!TIP]
>
>La integración entre Adobe Real-time CDP y Facebook admite los rellenos de audiencia históricos. Todas las cualificaciones del segmento histórico se envían a Facebook cuando activa los segmentos en el destino.

## Deshabilitar activación {#disable-activation}

Para deshabilitar un flujo de activación existente, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda, luego haga clic en la ficha **[!UICONTROL Examinar]** y, a continuación, haga clic en el nombre del destino.
2. Haga clic en el control **[!UICONTROL Habilitado]** en el carril derecho para cambiar el estado del flujo de activación.
3. En la ventana **Actualizar estado** de flujo de datos, seleccione **Confirmar** para desactivar el flujo de activación.

En AWS Kinesis, genere una clave de acceso: par de claves de acceso secreto para otorgar acceso CDP en tiempo real de Adobe a su cuenta de AWS Kinesis. Obtenga más información en la documentación [de](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)AWS Kinesis.