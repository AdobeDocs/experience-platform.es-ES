---
keywords: Experience Platform;inicio;temas populares;Phoenix;Phoenix
solution: Experience Platform
title: Crear una conexión de origen de Phoenix en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de Phoenix mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Crear un [!DNL Phoenix] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Phoenix] el conector está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Phoenix] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Phoenix] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md)

### Recopilar credenciales necesarias

Para acceder a su [!DNL Phoenix] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del [!DNL Phoenix] servidor. |
| `port` | El puerto TCP en el que [!DNL Phoenix] El servidor de utiliza para detectar conexiones de cliente. Si se conecta a [!DNL Azure HDInsights], especifique el puerto como 443. |
| `httpPath` | La URL parcial correspondiente a [!DNL Phoenix] servidor. Especifique /hbasephoenix0 si utiliza [!DNL Azure HDInsights] clúster. |
| `username` | El nombre de usuario que utiliza para acceder a [!DNL Phoenix] servidor. |
| `password` | La contraseña que corresponde al usuario. |
| `enableSsl` | Alternancia que especifica si las conexiones con el servidor se cifran mediante SSL. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conecte su [!DNL Phoenix] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Phoenix] cuenta a la que conectarse [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Phoenix]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Phoenix] cuenta.

![catalogar](../../../../images/tutorials/create/phoenix/catalog.png)

El **[!UICONTROL Conectar con Phoenix]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Phoenix] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/phoenix/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Phoenix] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Phoenix] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
