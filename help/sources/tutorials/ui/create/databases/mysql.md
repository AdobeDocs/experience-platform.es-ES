---
keywords: Experience Platform;inicio;temas populares;mysql;MySQL
solution: Experience Platform
title: Crear una conexión de Source MySQL en la interfaz de usuario
type: Tutorial
description: Aprenda a crear una conexión de origen MySQL mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL MySQL] en la interfaz de usuario

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una conexión de origen de [!DNL MySQL] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión de [!DNL MySQL], puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/databases.md).

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL MySQL] en [!DNL Experience Platform], debe proporcionar el siguiente valor:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión [!DNL MySQL] asociada a su cuenta. El patrón de cadena de conexión [!DNL MySQL] es: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Puede obtener más información sobre las cadenas de conexión y cómo obtenerlas leyendo el [[!DNL MySQL] documento](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Conectar su cuenta de [!DNL MySQL]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL MySQL] a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

En la categoría **[!UICONTROL Bases de datos]**, seleccione **[!UICONTROL MySQL]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL MySQL].

![](../../../../images/tutorials/create/my-sql/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con MySQL]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione un nombre, una descripción opcional y sus credenciales de [!DNL MySQL]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![](../../../../images/tutorials/create/my-sql/new.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL MySQL] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta MySQL. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos en [!DNL Experience Platform]](../../dataflow/databases.md).
