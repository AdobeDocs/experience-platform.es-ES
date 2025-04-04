---
keywords: Experience Platform;inicio;temas populares;HP Vertica
solution: Experience Platform
title: Creación de una conexión de Source de HP Vertica en la IU
type: Tutorial
description: Aprenda a crear una conexión de origen de HP Vertica mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 2%

---

# Crear una conexión de origen de HP [!DNL Vertica] en la interfaz de usuario

>[!NOTE]
>
> El conector HP [!DNL Vertica] está en fase beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen HP [!DNL Vertica] mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión HP [!DNL Vertica] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a HP [!DNL Vertica] mediante la API [!DNL Flow Service].

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Cadena de conexión utilizada para conectarse a la instancia de HP [!DNL Vertica]. El patrón de cadena de conexión para HP [!DNL Vertica] es `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obtener más información sobre cómo empezar, consulte [este documento de HP [!DNL Vertica] document](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Conecte su cuenta de HP [!DNL Vertica]

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su cuenta de HP [!DNL Vertica] a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL HP Vertica]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector de HP [!DNL Vertica].

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con HP Vertica]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de HP [!DNL Vertica]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/hp-vertica/new.png)

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de HP [!DNL Vertica] con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de HP [!DNL Vertica]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Experience Platform]](../../dataflow/databases.md).
