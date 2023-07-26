---
title: Conectar su cuenta de Phoenix mediante la interfaz de usuario de Experience Platform
description: Aprenda a conectar su cuenta de Phoenix y a llevar los datos de la base de datos de Phoenix al Experience Platform de mediante la interfaz de usuario de.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Conecte su [!DNL Phoenix] cuenta de al Experience Platform mediante la interfaz de usuario de

Este tutorial proporciona pasos sobre cómo conectar su [!DNL Phoenix] y traer datos de su cuenta [!DNL Phoenix] base de datos a Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un [!DNL Phoenix] cuenta, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos para una base de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL Phoenix] cuenta en el Experience Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| --- | --- |
| Host | La dirección IP o el nombre de host del [!DNL Phoenix] servidor. |
| Puerto | El puerto TCP en el que [!DNL Phoenix] El servidor de utiliza para detectar conexiones de cliente. Si se conecta a [!DNL Azure HDInsights], luego especifique el puerto como 443. Si no se proporciona este parámetro, el valor predeterminado es 8765. |
| Ruta HTTP | La URL parcial correspondiente a [!DNL Phoenix] servidor. Especifique /hbasephoenix0 si utiliza [!DNL Azure HDInsights] clúster. |
| Nombre de usuario | El nombre de usuario que utiliza para acceder a [!DNL Phoenix] servidor. |
| Una contraseña | La contraseña que corresponde al usuario. |
| Habilitar SSL | Alternar que especifica si las conexiones al servidor se cifran mediante SSL. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para conectar su [!DNL Phoenix] cuenta para el Experience Platform.

## Conecte su [!DNL Phoenix] account

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la navegación izquierda para acceder al espacio de trabajo de orígenes. El *[!UICONTROL Catálogo]* La pantalla muestra una variedad de fuentes disponibles en el catálogo de fuentes de Experience Platform.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar una fuente específica utilizando la opción de búsqueda.

Seleccionar **[!UICONTROL Bases de datos]** en la lista de categorías de fuentes y, a continuación, seleccione **[!UICONTROL Añadir datos]** desde el [!DNL Phoenix] Tarjeta de.

>[!TIP]
>
>Las fuentes del catálogo de fuentes pueden mostrar diferentes indicadores según el estado de la fuente.
> 
>* **[!UICONTROL Añadir datos]** significa que hay cuentas autenticadas existentes asociadas con el origen seleccionado.
>
>* **[!UICONTROL Configuración de]** significa que debe proporcionar credenciales y autenticar una cuenta nueva para utilizar el origen seleccionado.

![El catálogo de fuentes en la interfaz de usuario de Experience Platform con la tarjeta de fuente Phoenix seleccionada.](../../../../images/tutorials/create/phoenix/catalog.png)

El **[!UICONTROL Conectar con Phoenix]** página. En esta página, puede usar credenciales nuevas o existentes.

>[!BEGINTABS]

>[!TAB Usar una cuenta existente de Phoenix]

Para usar una cuenta existente, seleccione [!UICONTROL Cuenta existente] y, a continuación, seleccione la cuenta que desee utilizar en la lista que aparece. Cuando termine, seleccione [!UICONTROL Siguiente] para continuar.

![Una lista de cuentas de base de datos Phoenix autenticadas que ya existen en su organización.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Crear una nueva cuenta de Phoenix]

Para usar una cuenta nueva, seleccione [!UICONTROL Nueva cuenta] y proporcione un nombre, una descripción y su [!DNL Phoenix] credenciales de autenticación. Cuando termine, seleccione [!UICONTROL Conectar con el origen] y espere unos segundos para que se establezca la nueva conexión.

![La nueva interfaz de cuenta donde puede proporcionar credenciales de autenticación y crear una cuenta de Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Phoenix] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en Experience Platform](../../dataflow/databases.md).
