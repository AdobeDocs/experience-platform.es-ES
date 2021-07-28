---
title: Información general sobre la extensión Adobe Privacy
description: Obtenga información sobre la extensión de la etiqueta de privacidad de Adobe en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 92%

---

# Información general sobre la extensión Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de Adobe Privacy proporciona funcionalidad para recopilar y eliminar ID de usuario asignados a usuarios finales por soluciones de Adobe.

## Configurar soluciones durante la instalación

Al instalar la extensión de privacidad de Adobe desde el Catálogo de extensiones, se le pedirá que seleccione las soluciones que desee actualizar. Actualmente puede actualizar las siguientes soluciones:

* Analytics (AA)
* Audience Manager (AAM)
* Target
* Servicio de visitante
* Adcloud
* Seleccione una o varias soluciones y, a continuación, seleccione Actualizar.
* Cuando haya seleccionado y configurado las soluciones, seleccione Guardar. La extensión de privacidad de Adobe se agrega a la lista de extensiones instaladas.

   A continuación se describen las opciones de cada solución.

### Analytics

![](../../../images/ext-privacy-aa.jpg)

De forma predeterminada, debe especificar el grupo de informes introduciendo una cadena o seleccionando un elemento de datos.

Para configurar otros elementos, seleccione **[!UICONTROL Elegir un elemento]**, seleccione el elemento que desea configurar y, a continuación, seleccione **[!UICONTROL Añadir]** y escriba el parámetro o el elemento de datos solicitado.

### Audience Manager

![](../../../images/ext-privacy-aam.jpg)

Seleccione **[!UICONTROL Elegir un elemento]**, seleccione el elemento que desea configurar y, a continuación, seleccione **[!UICONTROL Añadir]** y escriba el parámetro o elemento de datos solicitado. Actualmente, solo puede configurar `aamUUIDCookieName`.

### Target

![](../../../images/ext-privacy-target.jpg)

Introduzca el código de cliente de Target.

### Servicio de visitante

![](../../../images/ext-privacy-visitor.jpg)

Introduzca su ID de organización de IMS.

### Adcloud

![](../../../images/ext-privacy-adcloud.jpg)

No hay parámetros específicos que configurar para adcloud.

## Configurar la extensión de Adobe Privacy

Después de instalar la extensión, puede desactivarla o eliminarla. Seleccione **[!UICONTROL Configurar]** en la tarjeta de privacidad de Adobe de sus extensiones instaladas y, a continuación, seleccione **[!UICONTROL Deshabilitar]** o **[!UICONTROL Desinstalar]**.

## Acciones

Las siguientes acciones están disponibles cuando se configura una regla con la extensión de privacidad de Adobe.

### Recuperar identidades

Cuando se cumplan los eventos y las condiciones, recupere la información de identidad que esté almacenada para el visitante.

Escriba el nombre de una función JavaScript a la que desee enviar los datos. Esta función o método gestiona las identidades recuperadas. Dependerá de usted si los almacena, los muestra o los envía a la API de Adobe RGPD.

### Eliminar identidades

Cuando se cumplan los eventos y las condiciones, quite la información de identidad que esté almacenada para el visitante.

Escriba el nombre de una función JavaScript a la que desee enviar los datos. Esta función o método gestiona las identidades recuperadas. Dependerá de usted si los almacena, los muestra o los envía a la API de Adobe RGPD.

### Recuperar y eliminar identidades

Cuando se cumplan los eventos y las condiciones, recupere la información de identidad que esté almacenada para el visitante y, a continuación, quítela.

## Tutorial: Configuración de la extensión Privacy

A continuación, se muestra un ejemplo combinado de la configuración de un elemento de datos y su uso con la extensión Privacy.

1. Crear un elemento de datos `privacyFunc`.

   ```JavaScript
   window.privacyFunc = function(a,b){
       console.log(a,b);
   }
   return window.privacyFunc
   ```

1. Cree una regla para ejecutarla en la carga de biblioteca (parte superior de la página), con una acción de la extensión Adobe Privacy. Seleccione `privacyFunc` como elemento de datos.

   * **Extensión**: Adobe Privacy
   * **Tipo de acción**: Recuperar identidades
Este tipo de acción muestra las identidades creadas, eliminadas o no eliminadas.
   * **Nombre**: Recuperar identidades

1. Actualice la biblioteca de desarrollo y, a continuación, publique y realice pruebas.
