---
keywords: Experience Platform;inicio;temas populares;Greenplum;greenplum
solution: Experience Platform
title: Crear una conexión de origen de GreenPlum en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Aprenda a crear una conexión de origen de GreenPlum mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: c3a72d5a4aea33f123f81bd416557a9cfe879224
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Cree un [!DNL GreenPlum] conexión de origen en la interfaz de usuario

Los conectores de origen de Adobe Experience Platform permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un [!DNL GreenPlum] conector de origen utilizando [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco normalizado por el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición del esquema](../../../../../xdm/schema/composition.md): Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

Si ya tiene una [!DNL GreenPlum] conexión, puede omitir el resto de este documento y continuar con el tutorial en [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar las credenciales necesarias

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL GreenPlum] usando la variable [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL GreenPlum] instancia. El patrón de cadena de conexión para [!DNL GreenPlum] es `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obtener más información sobre cómo empezar, consulte [este documento de GreenPlum](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Conecte su [!DNL GreenPlum] account

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para vincular sus [!DNL GreenPlum] cuenta para [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder a la **[!UICONTROL Fuentes]** espacio de trabajo. La variable **[!UICONTROL Catálogo]** muestra una variedad de fuentes para las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccione **[!UICONTROL GreenPlum]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear un [!DNL GreenPlum] conector.

![catálogo](../../../../images/tutorials/create/greenplum/catalog.png)

La variable **[!UICONTROL Conectarse a GreenPlum]** se abre. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, indique un nombre, una descripción opcional y su [!DNL GreenPlum] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, permita que la nueva conexión se establezca durante algún tiempo.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la opción [!DNL GreenPlum] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/greenplum/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL GreenPlum] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos [!DNL Platform]](../../dataflow/databases.md).
