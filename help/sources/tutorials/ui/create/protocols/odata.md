---
keywords: Experience Platform;inicio;temas populares;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Creación de una conexión genérica de OData Source en la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen de Protocolo de datos abiertos genérico mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Generic OData] en la interfaz de usuario

Los conectores de Source en Adobe Experience Platform permiten introducir datos de origen externo de forma programada. Este tutorial proporciona los pasos para crear un conector de origen [!DNL Generic Open Data Protocol] (denominado en adelante &quot;[!DNL OData]&quot;) mediante la interfaz de usuario [!DNL Experience Platform].

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una conexión [!DNL OData] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/protocols.md)

### Recopilar credenciales necesarias

Para tener acceso a su cuenta de [!DNL OData] en [!DNL Experience Platform], debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La URL raíz del servicio [!DNL OData]. |

Para obtener más información sobre cómo empezar, consulte [este [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conectar su cuenta de [!DNL OData]

Una vez que haya recopilado las credenciales requeridas, puede seguir los pasos a continuación para vincular su cuenta de [!DNL OData] a [!DNL Experience Platform].

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de **[!UICONTROL Fuentes]**. La pantalla **[!UICONTROL Catálogo]** muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría **[!UICONTROL Protocolos]**, seleccione **[!UICONTROL OData genérico]**. Si es la primera vez que usa este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Agregar datos]** para crear un nuevo conector [!DNL OData].

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con OData genérico]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está usando credenciales nuevas, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, proporcione a la conexión un nombre, una descripción opcional y las credenciales de [!DNL OData]. Cuando termine, seleccione **[!UICONTROL Conectar]** y deje pasar un tiempo para que se establezca la nueva conexión.

![conectar](../../../../images/tutorials/create/odata/connect.png)

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de [!DNL OData] con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta de [!DNL OData]. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para introducir datos de protocolos en [!DNL Experience Platform]](../../dataflow/protocols.md).
