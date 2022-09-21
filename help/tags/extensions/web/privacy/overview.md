---
title: Información general sobre la extensión Adobe Privacy
description: Obtenga información acerca de la extensión de etiquetas Adobe Privacy en Adobe Experience Platform.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 9%

---

# Información general sobre la extensión Adobe Privacy

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

La extensión de la etiqueta de privacidad de Adobe le permite recopilar y eliminar ID de usuario asignados a usuarios finales por soluciones de Adobe en dispositivos del lado del cliente. Los ID recopilados se pueden enviar a [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md) para acceder a los datos personales del individuo relacionado o eliminarlos en aplicaciones de Adobe Experience Cloud compatibles.

Esta guía explica cómo instalar y configurar la extensión de privacidad de Adobe en la interfaz de usuario del Experience Platform o la interfaz de usuario de recopilación de datos.

>[!NOTE]
>
>Si prefiere instalar estas funcionalidades sin utilizar etiquetas, consulte la [Resumen de la biblioteca JavaScript de privacidad](../../../../privacy-service/js-library.md) para ver los pasos sobre cómo implementar mediante código sin procesar.

## Instale y configure la extensión de 

Select **[!UICONTROL Extensiones]** en el panel de navegación izquierdo, seguido del **[!UICONTROL Catálogo]** pestaña . Utilice la barra de búsqueda para reducir la lista de extensiones disponibles hasta que encuentre la privacidad de Adobe. Select **[!UICONTROL Instalar]** para continuar.

![Instalación de la extensión](../../../images/extensions/privacy/install.png)

La siguiente pantalla le permite configurar de qué fuentes y soluciones desea que recopile ID de la extensión. Las siguientes soluciones son compatibles con la extensión :

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Servicio de identidad de Adobe Experience Cloud (visitante o ECID)
* Adobe Advertising Cloud (AdCloud)

Seleccione una o varias soluciones y, a continuación, seleccione **[!UICONTROL Actualizar]**.

![Seleccionar soluciones](../../../images/extensions/privacy/select-solutions.png)

La pantalla se actualiza para mostrar entradas para los parámetros de configuración necesarios en función de las soluciones seleccionadas.

![Propiedades requeridas](../../../images/extensions/privacy/required-properties.png)

Con el menú desplegable que aparece a continuación, también puede agregar parámetros adicionales específicos de la solución a la configuración.

![Propiedades opcionales](../../../images/extensions/privacy/optional-properties.png)

>[!NOTE]
>
>Consulte la sección sobre [parámetros de configuración](../../../../privacy-service/js-library.md#config-params) en la descripción general de la biblioteca JavaScript de privacidad para obtener más información sobre los valores de configuración aceptados para cada solución admitida.

Una vez que haya terminado de agregar parámetros para las soluciones seleccionadas, seleccione **[!UICONTROL Guardar]** para guardar la configuración.

![Propiedades opcionales](../../../images/extensions/privacy/save-config.png)

## Uso de la extensión {#using}

La extensión de privacidad de Adobe proporciona tres tipos de acciones que se pueden usar en una [regla](../../../ui/managing-resources/rules.md) cuando se produce un determinado evento y se cumplen determinadas condiciones:

* **[!UICONTROL Recuperar identidades]**: Se recupera la información de identidad almacenada del usuario.
* **[!UICONTROL Eliminar identidades]**: Se elimina la información de identidad almacenada del usuario.
* **[!UICONTROL Recuperar y eliminar identidades]**: La información de identidad almacenada del usuario se recupera y se elimina.

Para cada una de las acciones anteriores, debe proporcionar una función de llamada de retorno JavaScript que acepte y gestione los datos de identidad recuperados como parámetro de objeto. Desde aquí, puede almacenar estas identidades, mostrarlas o enviarlas a la [API de Privacy Service](../../../../privacy-service/api/overview.md) según sea necesario.

Al utilizar la extensión de etiqueta de privacidad de Adobe, debe proporcionar la función de llamada de retorno necesaria en forma de elemento de datos. Consulte la siguiente sección para ver los pasos sobre cómo configurar este elemento de datos.

### Definir un elemento de datos para gestionar identidades

Inicie el proceso de creación de un nuevo elemento de datos seleccionando **[!UICONTROL Elementos de datos]** en la navegación izquierda, seguido de **[!UICONTROL Añadir elemento de datos]**. Una vez que esté en la pantalla de configuración, seleccione **[!UICONTROL Principal]** para la extensión y **[!UICONTROL Código personalizado]** para el tipo de elemento de datos. Desde aquí, seleccione **[!UICONTROL Abrir editor]** en el panel derecho.

![Seleccionar tipo de elemento de datos](../../../images/extensions/privacy/data-element-type.png)

En el cuadro de diálogo que aparece, defina una función de JavaScript que gestione las identidades recuperadas. La rellamada debe aceptar un único argumento de tipo de objeto (`ids` en el ejemplo siguiente). A continuación, la función puede gestionar los ID como desee y también puede invocar cualquier variable y función que esté disponible globalmente en el sitio para un procesamiento posterior.

>[!NOTE]
>
>Para obtener más información sobre la estructura de la variable `ids` que se espera que gestione la función de llamada de retorno, consulte la sección [muestras de código](../../../../privacy-service/js-library.md#samples) en la descripción general de la biblioteca JavaScript de privacidad.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Definir la función de llamada de retorno](../../../images/extensions/privacy/define-custom-code.png)

Puede seguir creando otros elementos de datos de código personalizado si necesita llamadas de retorno diferentes para eventos diferentes.

### Crear una regla con una acción de privacidad

Después de configurar un elemento de datos de llamada de retorno para administrar los ID recuperados, puede crear una regla que invoque la extensión de privacidad de Adobe siempre que se produzca un evento determinado en el sitio junto con cualquier otra condición que requiera.

Al configurar la acción para la regla, seleccione **[!UICONTROL Privacidad del Adobe]** para la extensión de . Para el tipo de acción, seleccione una de las [tres funciones](#using) proporcionado por la extensión de .

![Seleccionar tipo de acción](../../../images/extensions/privacy/action-type.png)

El panel derecho le solicita que seleccione un elemento de datos que servirá como llamada de retorno de la acción. Seleccione el icono de base de datos (![Icono de base de datos](../../../images/extensions/privacy/database.png)) y elija el elemento de datos que creó anteriormente desde la lista. Select **[!UICONTROL Conservar cambios]** para continuar.

![Seleccionar elemento de datos](../../../images/extensions/privacy/add-data-element.png)

Desde aquí, puede continuar configurando la regla para que la acción de privacidad del Adobe se active según los eventos y las condiciones que requiera. Cuando esté satisfecho, seleccione **[!UICONTROL Guardar]**.

![Guarde la regla](../../../images/extensions/privacy/save-rule.png)

Ahora puede añadir la regla a una biblioteca para implementarla como una compilación en el sitio web para realizar pruebas. Consulte la descripción general de la [flujo de publicación de etiquetas](../../../ui/publishing/overview.md) para obtener más información.

## Desactivar o desinstalar la extensión

Después de instalar la extensión, puede desactivarla o eliminarla. Seleccione **[!UICONTROL Configurar]** en la tarjeta de privacidad de Adobe de sus extensiones instaladas y, a continuación, seleccione **[!UICONTROL Deshabilitar]** o **[!UICONTROL Desinstalar]**.

## Pasos siguientes

Esta guía abarcaba el uso de la extensión de etiqueta de privacidad de Adobe en la interfaz de usuario. Para obtener más información sobre las funcionalidades proporcionadas por la extensión, incluidos ejemplos de cómo emplearla con código sin procesar, consulte la [Resumen de la biblioteca JavaScript de privacidad](../../../../privacy-service/js-library.md) en la documentación del Privacy Service.
