---
keywords: Experience Platform;inicio;temas populares;Azure Table Storage;almacenamiento de tablas de Azure;ats;ATS
solution: Experience Platform
title: Crear una conexión de origen de Azure Table Storage en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Azure Table Storage mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Crear un [!DNL Azure Table Storage] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Azure Table Storage] (en lo sucesivo, &quot;ATS&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión ATS válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su cuenta ATS en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Una cadena de conexión para conectarse a su [!DNL Azure Table Storage] ejemplo. Cadena de conexión para conectarse a la instancia de ATS. El patrón de cadena de conexión para ATS es `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL Azure Table Storage] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Conecte su [!DNL Azure Table Storage] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta ATS a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Azure Table Storage]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un nuevo conector ATS.

![catalogar](../../../../images/tutorials/create/ats/catalog.png)

El **[!UICONTROL Conectar con Azure Table Storage]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de ATS. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/ats/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta ATS con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/ats/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta ATS. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
