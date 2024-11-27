---
keywords: Experience Platform;inicio;temas populares;Couchbase;couchbase
solution: Experience Platform
title: Creación de una conexión de Couchbase Source en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen de Couchbase mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Couchbase] en la interfaz de usuario

>[!WARNING]
>
>El origen [!DNL Couchbase] quedará obsoleto a finales de junio de 2025.

Los conectores Source de [!DNL Adobe Experience Platform] permiten la ingesta de datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Couchbase] mediante la interfaz de usuario [!DNL Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL Couchbase] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para autenticar el conector de origen [!DNL Couchbase], debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | Cadena de conexión utilizada para conectarse a la instancia [!DNL Couchbase]. El patrón de cadena de conexión de [!DNL Couchbase] es `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Para obtener más información sobre cómo adquirir una cadena de conexión, consulte la documentación sobre [[!DNL Couchbase] conexión](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Conectar su cuenta de [!DNL Couchbase]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL Couchbase] a [!DNL Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL Couchbase]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL Couchbase].

![catálogo](../../../../images/tutorials/create/couchbase/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con Couchbase]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL Couchbase]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/couchbase/new.png)

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta de [!DNL Couchbase] con la que deseas conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/couchbase/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL Couchbase]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
