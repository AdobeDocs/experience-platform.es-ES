---
keywords: Experience Platform;inicio;temas populares;mysql;MySQL
solution: Experience Platform
title: Crear una conexión de origen MySQL en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen MySQL mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# Crear un [!DNL MySQL] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL MySQL] conexión de origen mediante la IU de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un [!DNL MySQL] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para acceder a su [!DNL MySQL] cuenta en [!DNL Platform], debe proporcionar el siguiente valor:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | El [!DNL MySQL] cadena de conexión asociada a su cuenta. El [!DNL MySQL] el patrón de cadena de conexión es: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Puede obtener más información acerca de las cadenas de conexión y cómo obtenerlas leyendo el [[!DNL MySQL] documento](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Conecte su [!DNL MySQL] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL MySQL] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

En el **[!UICONTROL Bases de datos]** categoría, seleccionar **[!UICONTROL MySQL]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL MySQL] conector.

![](../../../../images/tutorials/create/my-sql/catalog.png)

El **[!UICONTROL Conectar con MySQL]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y su [!DNL MySQL] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/my-sql/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL MySQL] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta MySQL. Ahora puede continuar con el siguiente tutorial y [configuración de un flujo de datos para introducir datos en [!DNL Platform]](../../dataflow/databases.md).
