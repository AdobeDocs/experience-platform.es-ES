---
keywords: Experience Platform;inicio;temas populares;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Crear una conexión de origen OData genérica en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Protocolo de datos abiertos genérico mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Crear un [!DNL Generic OData] conexión de origen en la interfaz de usuario

Los conectores de origen en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear una [!DNL Generic Open Data Protocol] (en lo sucesivo, &quot;[!DNL OData]&quot;) utilizando el conector de origen [!DNL Platform] interfaz de usuario.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene un válido [!DNL OData] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/protocols.md)

### Recopilar credenciales necesarias

Para acceder a su [!DNL OData] cuenta en [!DNL Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La URL raíz del [!DNL OData] servicio. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conecte su [!DNL OData] account

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para vincular su [!DNL OData] cuenta a [!DNL Platform].

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com) y luego seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a **[!UICONTROL Fuentes]** workspace. El **[!UICONTROL Catálogo]** La pantalla muestra una variedad de fuentes para las que puede crear una cuenta con.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el **[!UICONTROL Protocolos]** categoría, seleccionar **[!UICONTROL OData genérico]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva [!DNL OData] conector.

![catalogar](../../../../images/tutorials/create/odata/catalog.png)

El **[!UICONTROL Conectar con OData genérico]** página. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione a la conexión un nombre, una descripción opcional y su [!DNL OData] credenciales. Cuando termine, seleccione **[!UICONTROL Connect]** y, a continuación, espere un poco para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/odata/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la [!DNL OData] cuenta con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su [!DNL OData] cuenta. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para incorporar datos de protocolos a [!DNL Platform]](../../dataflow/protocols.md).
