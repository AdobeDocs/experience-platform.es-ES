---
title: Información general sobre la extensión Adobe Privacy
description: Obtenga información acerca de la extensión de etiquetas Adobe Privacy en Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 9%

---

# Información general sobre la extensión Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de Adobe de privacidad permite recopilar y eliminar ID de usuario asignados a usuarios finales por soluciones de Adobe en dispositivos del lado del cliente. Los ID recopilados se pueden enviar a [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) para acceder a los datos personales de las personas relacionadas o eliminarlos en las aplicaciones de Adobe Experience Cloud compatibles.

Esta guía explica cómo instalar y configurar la extensión de privacidad de Adobe en la interfaz de usuario de Experience Platform o en la interfaz de usuario de recopilación de datos.

>[!NOTE]
>
>Si prefiere instalar estas funcionalidades sin utilizar etiquetas, consulte la [Información general sobre la biblioteca JavaScript de privacidad](../../../../privacy-service/js-library.md) para ver los pasos sobre cómo implementar mediante código sin procesar.

## Instale y configure la extensión de 

Seleccionar **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Catálogo]** pestaña. Utilice la barra de búsqueda para reducir la lista de extensiones disponibles hasta que encuentre Privacidad de Adobe. Seleccionar **[!UICONTROL Instalar]** para continuar.

![Instalación de la extensión](../../../images/extensions/client/privacy/install.png)

La siguiente pantalla le permite configurar de qué fuentes y soluciones desea que la extensión recopile ID. Se admiten las siguientes soluciones para la extensión:

* Adobe Analytics (AA)
* Adobe Audience Manager AAM ()
* Adobe Target
* Servicio de identidad de Adobe Experience Cloud (visitante o ECID)
* Adobe Advertising Cloud (AdCloud)

Seleccione una o varias soluciones y, a continuación, seleccione **[!UICONTROL Actualizar]**.

![Seleccionar soluciones](../../../images/extensions/client/privacy/select-solutions.png)

La pantalla se actualiza para mostrar las entradas de los parámetros de configuración necesarios en función de las soluciones seleccionadas.

![Propiedades requeridas](../../../images/extensions/client/privacy/required-properties.png)

Con el menú desplegable siguiente, también puede agregar parámetros adicionales específicos de la solución a la configuración.

![Propiedades opcionales](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>Consulte la sección sobre [parámetros de configuración](../../../../privacy-service/js-library.md#config-params) en Información general de la biblioteca JavaScript de privacidad para obtener más información sobre los valores de configuración aceptados para cada solución admitida.

Cuando haya terminado de agregar parámetros para las soluciones seleccionadas, seleccione **[!UICONTROL Guardar]** para guardar la configuración.

![Propiedades opcionales](../../../images/extensions/client/privacy/save-config.png)

## Uso de la extensión {#using}

La extensión de privacidad de Adobe proporciona tres tipos de acción que se pueden utilizar en una [regla](../../../ui/managing-resources/rules.md) cuando se produce un evento determinado y se cumplen las condiciones:

* **[!UICONTROL Recuperar identidades]**: se recupera la información de identidad almacenada del usuario.
* **[!UICONTROL Eliminar identidades]**: se elimina la información de identidad almacenada del usuario.
* **[!UICONTROL Recuperar y eliminar identidades]**: la información de identidad almacenada del usuario se recupera y, a continuación, se elimina.

Para cada una de las acciones anteriores, debe proporcionar una función de llamada de retorno de JavaScript que acepte y gestione los datos de identidad recuperados como parámetro de objeto. Desde aquí, puede almacenar estas identidades, mostrarlas o enviarlas al [API de Privacy Service](../../../../privacy-service/api/overview.md) según lo requiera.

Al utilizar la extensión de Adobe de privacidad, debe proporcionar la función de llamada de retorno necesaria en forma de elemento de datos. Consulte la siguiente sección para ver los pasos sobre cómo configurar este elemento de datos.

### Definir un elemento de datos para gestionar identidades

Inicie el proceso de creación de un nuevo elemento de datos seleccionando **[!UICONTROL Elementos de datos]** en el panel de navegación izquierdo, seguido de **[!UICONTROL Añadir elemento de datos]**. Una vez que esté en la pantalla de configuración, seleccione **[!UICONTROL Núcleo]** para la extensión y **[!UICONTROL Código personalizado]** para el tipo de elemento de datos. Desde aquí, seleccione **[!UICONTROL Abrir editor]** en el panel derecho.

![Seleccionar tipo de elemento de datos](../../../images/extensions/client/privacy/data-element-type.png)

En el cuadro de diálogo que aparece, defina una función de JavaScript que administre las identidades recuperadas. La llamada de retorno debe aceptar un único argumento de tipo de objeto (`ids` en el ejemplo siguiente). La función puede administrar los ID como desee y también puede invocar cualquier variable y función que estén disponibles globalmente en el sitio para un procesamiento posterior.

>[!NOTE]
>
>Para obtener más información sobre la estructura del `ids` objeto que se espera que gestione la función de llamada de retorno, consulte el [ejemplos de código](../../../../privacy-service/js-library.md#samples) se proporciona en la información general de la Biblioteca de JavaScript de privacidad.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Definir función de llamada de retorno](../../../images/extensions/client/privacy/define-custom-code.png)

Puede seguir creando otros elementos de datos de código personalizado si necesita diferentes llamadas de retorno para diferentes eventos.

### Creación de una regla con una acción de privacidad

Después de configurar un elemento de datos de llamada de retorno para administrar los ID recuperados, puede crear una regla que invoque la extensión de privacidad de Adobe cada vez que se produzca un evento determinado en el sitio junto con cualquier otra condición que requiera.

Al configurar la acción de la regla, seleccione **[!UICONTROL Privacidad de Adobe]** para la extensión de. Para el tipo de acción, seleccione una de las [tres funciones](#using) proporcionada por la extensión de.

![Seleccionar tipo de acción](../../../images/extensions/client/privacy/action-type.png)

El panel derecho le solicita que seleccione un elemento de datos que sirva como llamada de retorno de la acción. Seleccione el icono de base de datos (![Icono de base de datos](../../../images/extensions/client/privacy/database.png)) y elija el elemento de datos que creó anteriormente en la lista. Seleccionar **[!UICONTROL Conservar cambios]** para continuar.

![Seleccionar elemento de datos](../../../images/extensions/client/privacy/add-data-element.png)

A partir de aquí, puede seguir configurando la regla para que la acción Privacidad de Adobe se active en los eventos y condiciones que requiera. Cuando esté satisfecho, seleccione **[!UICONTROL Guardar]**.

![Guarde la regla](../../../images/extensions/client/privacy/save-rule.png)

Ahora puede agregar la regla a una biblioteca para implementarla como una compilación en el sitio web para realizar pruebas. Consulte la descripción general de la [flujo de publicación de etiquetas](../../../ui/publishing/overview.md) para obtener más información.

## Deshabilite o desinstale la extensión

Después de instalar la extensión, puede desactivarla o eliminarla. Seleccione **[!UICONTROL Configurar]** en la tarjeta de privacidad de Adobe de sus extensiones instaladas y, a continuación, seleccione **[!UICONTROL Deshabilitar]** o **[!UICONTROL Desinstalar]**.

## Pasos siguientes

En esta guía se describe el uso de la extensión de Adobe de privacidad en la interfaz de usuario. Para obtener más información sobre las funcionalidades proporcionadas por la extensión, incluidos ejemplos de cómo emplearla con código sin procesar, consulte la [Información general sobre la biblioteca JavaScript de privacidad](../../../../privacy-service/js-library.md) en la documentación del Privacy Service.
