---
keywords: Experience Platform;inicio;temas populares;Couchbase;couchbase
solution: Experience Platform
title: Crear una conexión de origen de Couchbase en la IU
type: Tutorial
description: Aprenda a crear una conexión de origen de Couchbase mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 4270a48a-843c-4f1e-b280-35b620581d68
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Crear un [!DNL Couchbase] conexión de origen en la interfaz de usuario

>[!NOTE]
>
> El [!DNL Couchbase] el conector está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Conectores de origen en [!DNL Adobe Experience Platform] permite introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Couchbase] conector de origen mediante [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de [!DNL Platform]:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL Couchbase] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para autenticar su [!DNL Couchbase] conector de origen, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Couchbase] ejemplo. El patrón de cadena de conexión para [!DNL Couchbase] es `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Para obtener más información sobre la adquisición de una cadena de conexión, consulte la documentación sobre [[!DNL Couchbase] conexión](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Conecte su [!DNL Couchbase] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL Couchbase] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL Couchbase]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL Couchbase] conector.

![catalogar](../../../../images/tutorials/create/couchbase/catalog.png)

El **[!UICONTROL Conectar con Couchbase]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL Couchbase] credenciales. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/couchbase/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL Couchbase] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![existente](../../../../images/tutorials/create/couchbase/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL Couchbase] cuenta. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
