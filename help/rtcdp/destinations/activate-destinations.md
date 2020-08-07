---
title: Activar perfiles y segmentos en un destino
seo-title: Activar perfiles y segmentos en un destino
description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
seo-description: Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.
translation-type: tm+mt
source-git-commit: 86ded28b1830d3607c8b5214c8d31dfcbf446252
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---


# Activar perfiles y segmentos en un destino

Active los datos que tiene en la plataforma de datos del cliente en tiempo real de Adobe asignando segmentos a destinos. Para lograrlo, siga los pasos a continuación.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado correctamente un destino](/help/rtcdp/destinations/connect-destination.md). Si aún no lo ha hecho, vaya al catálogo [de](/help/rtcdp/destinations/destinations-catalog.md)destinos, busque los destinos admitidos y configure uno o varios destinos.

## Activar datos {#activate-data}

1. En **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]**, seleccione el destino en el que desea activar los segmentos.
2. Haga clic en el nombre del destino. Esto le lleva al flujo Activar.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Tenga en cuenta que si ya existe un flujo de activación para un destino, puede ver los segmentos que se están enviando al destino. Seleccione **[!UICONTROL Editar activación]** en el carril derecho y siga los pasos a continuación para modificar los detalles de la activación.
3. Seleccione **[!UICONTROL Activar]**;
4. En el flujo de trabajo **[!UICONTROL Activar destino]** , en la página **[!UICONTROL Seleccionar segmentos]** , seleccione los segmentos que desea enviar al destino.
   ![segmentos a destino](/help/rtcdp/destinations/assets/email-select-segments.png)
5. *Condicional*. Este paso varía en función del tipo de destino en el que se activan los segmentos. <br> Para los destinos *de marketing de* correo electrónico y los destinos *de almacenamiento de* nube, en la página **[!UICONTROL Seleccionar atributos]** , seleccione **[!UICONTROL Añadir nuevo campo]** y seleccione los atributos que desee enviar al destino.
Se recomienda que uno de los atributos sea un identificador [](/help/rtcdp/destinations/email-marketing-destinations.md#identity) único del esquema de unión. Para obtener más información sobre los atributos obligatorios, consulte Identidad en el artículo Destinos [de marketing de](/help/rtcdp/destinations/email-marketing-destinations.md#identity) correo electrónico.

   >[!NOTE]
   > 
   >Si se han aplicado etiquetas de uso de datos a ciertos campos dentro de un conjunto de datos (en lugar de a todo el conjunto de datos), la aplicación de las etiquetas de nivel de campo en la activación se produce bajo las siguientes condiciones:
   >* Los campos se utilizan en la definición del segmento.
   >* Los campos se configuran como atributos proyectados para el destino de destinatario.

   >
   > Considere la captura de pantalla de abajo. Si, por ejemplo, el campo `person.name.first.Name` tenía ciertas etiquetas de uso de datos que entran en conflicto con el caso de uso de marketing del destino, se le mostraría una infracción de directiva de uso de datos en el paso de revisión (paso 7). Para obtener más información, consulte Administración [de datos en CDP en tiempo real](/help/rtcdp/privacy/data-governance-overview.md#destinations)

   ![destination-attributes](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Para los destinos ** sociales, en el paso Asignación **[!UICONTROL de]** identidad, puede seleccionar atributos de origen para asignarlos como identidades de destinatario en el destino. Este paso es opcional u obligatorio, según la identidad principal que utilice en el esquema. <br> 

   *Dirección de correo electrónico como identidad* principal: Si utiliza la dirección de correo electrónico como identidad principal en el esquema, puede omitir el paso de asignación de identidad, como se muestra a continuación:

   ![Dirección de correo electrónico como identidad](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Otro ID como identidad* principal: Si utiliza otro ID, como ID *de* recompensas o ID *de* lealtad, como identidad principal en el esquema, deberá asignar manualmente la dirección de correo electrónico del esquema de identidad como identidad de destinatario en el destino social, como se muestra a continuación:

   ![ID de fidelidad como identidad](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Seleccione `Email_LC_SHA256` como identidad de destinatario si ha marcado las direcciones de correo electrónico de los clientes al ingerir datos en Adobe Experience Platform, según los requisitos [!DNL Facebook] de hash de [](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)correo electrónico. <br> Seleccione `Email` como identidad de destinatario si las direcciones de correo electrónico que utiliza no están marcadas por hash. CDP en tiempo real de Adobe realizará un hash de las direcciones de correo electrónico para cumplir con [!DNL Facebook] los requisitos.

   ![asignación de identidad después de rellenar los campos](/help/rtcdp/destinations/assets/identity-mapping.png)

6. En la página Programación **[!UICONTROL de]** segmentos, puede ver la fecha de inicio para enviar datos al destino, así como la frecuencia con la que se envían datos al destino.

   >[!IMPORTANT]
   >
   >Para los destinos sociales, debe seleccionar el origen de la audiencia en este paso. Sólo puede continuar con el paso siguiente después de seleccionar una de las opciones de la siguiente imagen.

   ![elegir origen de datos](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. En la página **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y el inicio de envío de datos al destino.

   >[!IMPORTANT]
   >
   >En este paso, CDP en tiempo real comprueba las infracciones de las políticas de uso de datos. A continuación se muestra un ejemplo de violación de una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver las infracciones de políticas, consulte Aplicación de [políticas](/help/rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de administración de datos.

![confirmación-selección](/help/rtcdp/destinations/assets/data-policy-violation.png)

Si no se ha detectado ninguna infracción de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y el inicio al enviar datos al destino.

![confirmación-selección](/help/rtcdp/destinations/assets/confirm-selection.png)



## Editar activación {#edit-activation}

Siga los pasos a continuación para editar los flujos de activación existentes en CDP en tiempo real:

1. Seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda, luego haga clic en la ficha **[!UICONTROL Examinar]** y, a continuación, haga clic en el nombre del destino.
2. Seleccione **[!UICONTROL Editar activación]** en el carril derecho para cambiar los segmentos que se van a enviar al destino.

## Verifique que la activación del segmento se haya realizado correctamente {#verify-activation}

### Destinos de marketing por correo electrónico y destinos de almacenamiento en la nube {#esp-and-cloud-storage}

Para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube, CDP en tiempo real de Adobe crea un archivo delimitado por tabuladores `.csv` o `.txt` en la ubicación de almacenamiento proporcionada. Se espera que cada día se cree un nuevo archivo en la ubicación del almacenamiento. The file format is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv|txt`

Los archivos que recibiría en tres días consecutivos podrían tener este aspecto:

```
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presencia de estos archivos en la ubicación del almacenamiento es la confirmación de la activación correcta. Para comprender la estructura de los archivos exportados, puede [descargar un archivo](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv).csv de muestra. Este archivo de ejemplo incluye los atributos `person.firstname`de perfil, `person.lastname`, `person.gender`, `person.birthyear`y `personalEmail.address`.

### Destinos publicitarios

Compruebe su cuenta en el destino de publicidad correspondiente en el que está activando sus datos. Si la activación se ha realizado correctamente, las audiencias se rellenan en la plataforma de publicidad.

### Destinos de redes sociales

Por ejemplo, [!DNL Facebook]una activación exitosa significa que se crearía una audiencia [!DNL Facebook] personalizada mediante programación en el Administrador [[!UICONTROL de publicidades de]](https://www.facebook.com/adsmanager/manage/)Facebook. La pertenencia a segmentos en la audiencia se agregaría y eliminaría a medida que los usuarios estuvieran cualificados o descalificados para los segmentos activados.

>[!TIP]
>
>La integración entre CDP en tiempo real de Adobe y [!DNL Facebook] admite los rellenos históricos de audiencias. Todas las cualificaciones del segmento histórico se envían [!DNL Facebook] cuando activa los segmentos en el destino.

## Deshabilitar activación {#disable-activation}

Para deshabilitar un flujo de activación existente, siga los pasos a continuación:

1. Seleccione **[!UICONTROL Destinos]** en la barra de navegación izquierda, luego haga clic en la ficha **[!UICONTROL Examinar]** y, a continuación, haga clic en el nombre del destino.
2. Haga clic en el control **[!UICONTROL Habilitado]** en el carril derecho para cambiar el estado del flujo de activación.
3. En la ventana **Actualizar estado** de flujo de datos, seleccione **Confirmar** para desactivar el flujo de activación.
