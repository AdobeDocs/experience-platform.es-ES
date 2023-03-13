---
keywords: Experience Platform;inicio;temas populares;Greenplum;greenplum
solution: Experience Platform
title: Crear una conexión de origen de GreenPlum en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de GreenPlum mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Crear un [!DNL GreenPlum] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL GreenPlum] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL GreenPlum] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL GreenPlum] uso del [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL GreenPlum] ejemplo. El patrón de cadena de conexión para [!DNL GreenPlum] es `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obtener más información sobre cómo empezar, consulte [este documento de GreenPlum](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Conecte su [!DNL GreenPlum] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL GreenPlum] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL GreenPlum]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL GreenPlum] conector.

![catalogar](../../../../images/tutorials/create/greenplum/catalog.png)

El **[!UICONTROL Conectar con GreenPlum]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL GreenPlum] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/greenplum/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL GreenPlum] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/greenplum/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL GreenPlum] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
