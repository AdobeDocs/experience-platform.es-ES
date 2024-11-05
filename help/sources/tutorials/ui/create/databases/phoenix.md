---
title: Conectar su cuenta de Phoenix mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Phoenix y a llevar los datos de la base de datos de Phoenix al Experience Platform de mediante la interfaz de usuario de.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# Conecte su cuenta de [!DNL Phoenix] al Experience Platform mediante la interfaz de usuario

>[!IMPORTANT]
>
>El origen [!DNL Phoenix] quedará obsoleto a finales de mayo de 2025. Como alternativa, puede utilizar el origen [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Este tutorial proporciona pasos sobre cómo conectar su cuenta de [!DNL Phoenix] y traer datos de su base de datos de [!DNL Phoenix] al Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL Phoenix] autenticada, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para una base de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su cuenta de [!DNL Phoenix] en el Experience Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| --- | --- |
| Host | La dirección IP o el nombre de host del servidor [!DNL Phoenix]. |
| Puerto | El puerto TCP que utiliza el servidor [!DNL Phoenix] para detectar conexiones de cliente. Si se está conectando a [!DNL Azure HDInsights], especifique el puerto como 443. Si no se proporciona este parámetro, el valor predeterminado es 8765. |
| Ruta HTTP | La dirección URL parcial correspondiente al servidor [!DNL Phoenix]. Especifique /hbasephoenix0 si utiliza el clúster [!DNL Azure HDInsights]. |
| Nombre de usuario | Nombre de usuario que utiliza para obtener acceso al servidor [!DNL Phoenix]. |
| Contraseña | La contraseña que corresponde al usuario. |
| Habilitar SSL | Alternar que especifica si las conexiones al servidor se cifran mediante SSL. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para conectar su cuenta de [!DNL Phoenix] al Experience Platform.

## Conectar su cuenta de [!DNL Phoenix]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en el panel de navegación izquierdo para acceder al área de trabajo de sources. La pantalla *[!UICONTROL Catálogo]* muestra una variedad de orígenes disponibles en el catálogo de orígenes de Experience Platform.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar una fuente específica utilizando la opción de búsqueda.

Seleccione **[!UICONTROL Bases de datos]** de la lista de categorías de orígenes y luego seleccione **[!UICONTROL Agregar datos]** de la tarjeta [!DNL Phoenix].

>[!TIP]
>
>Las fuentes del catálogo de fuentes pueden mostrar diferentes indicadores según el estado de la fuente.
> 
>* **[!UICONTROL Agregar datos]** significa que existen cuentas autenticadas asociadas con el origen seleccionado.
>
>* **[!UICONTROL Configurado]** significa que debe proporcionar credenciales y autenticar una cuenta nueva para usar el origen seleccionado.

![El catálogo de orígenes en la interfaz de usuario de Experience Platform con la tarjeta de origen de Phoenix seleccionada.](../../../../images/tutorials/create/phoenix/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Phoenix]**. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Usar una cuenta existente de Phoenix]

Para usar una cuenta existente, seleccione [!UICONTROL Cuenta existente] y luego seleccione la cuenta que desee usar en la lista que aparece. Cuando termine, seleccione [!UICONTROL Siguiente] para continuar.

![Una lista de cuentas de base de datos Phoenix autenticadas que ya existen en su organización.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Crear una nueva cuenta de Phoenix]

Para usar una cuenta nueva, selecciona [!UICONTROL Cuenta nueva] y proporciona un nombre, una descripción y tus credenciales de autenticación [!DNL Phoenix]. Cuando termine, seleccione [!UICONTROL Conectarse al origen] y espere unos segundos para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta donde puede proporcionar credenciales de autenticación y crear una cuenta de Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Phoenix]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en el Experience Platform](../../dataflow/databases.md).
