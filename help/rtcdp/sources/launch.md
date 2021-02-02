---
keywords: iniciar etiquetas web;inicio de etiquetas web;etiquetas web;etiquetas de sitio web;etiquetas web;inicio;inicio;inicio
title: Tutorial Implemente etiquetas de sitios web con Adobe Launch
seo-title: Implementación de etiquetas de sitios web con Adobe Launch
description: Uso de Adobe Launch para implementar las etiquetas de sitios web en Adobe Experience Platform
seo-description: Uso de Adobe Launch para implementar las etiquetas de sitios web en Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 8%

---


# Tutorial: Implementación de etiquetas de sitios web con Adobe Launch

En este tutorial se explica cómo implementar las etiquetas del sitio web para enviar datos a Adobe Experience Platform mediante Adobe Launch.

## Requisitos previos

* El esquema y el conjunto de datos necesarios se crean en [!DNL Platform].
* La configuración necesaria se ha implementado en Experience Edge y tiene el ID de configuración y el dominio de Edge coincidentes.
* El CMS de compañía ya se ha configurado para entregar un objeto JavaScript en cada página con los datos que necesita enviar a Platform.

## Pasos

Este tutorial contiene los siguientes pasos:

1. Instale la extensión [!DNL Web SDK] de Adobe Experience Platform.
1. Cree una regla para indicar [!DNL Launch] qué datos enviar.
1. Agrupar la extensión y la regla en una biblioteca.

## Instalar la extensión Adobe Experience Platform [!DNL Web SDK]

En primer lugar, instale la extensión [!DNL Web SDK] de Adobe Experience Platform.

1. En [!DNL Launch], abra la ficha **[!UICONTROL Extensiones]**.

   ![imagen](assets/launch-overview.png)

1. Seleccione la extensión de Adobe Experience Platform Web SDK en el catálogo de Launch Extension
Se abre la pantalla de configuración.

   ![imagen](assets/launch-extension-install.png)

   Para obtener más información, consulte [Extensiones](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) en la documentación de [!DNL Launch].

1. Configurar la extensión de.

   Los únicos ajustes que necesita ahora son:

   * **ID de configuración:** especifique el ID de configuración que obtuvo de su representante de Adobe.
   * **Dominio de Edge:** especifique el dominio de Edge que obtuvo de su representante de Adobe.

1. Seleccione **[!UICONTROL Guardar]** y continúe con el paso siguiente.

## Cree una regla para indicar [!DNL Launch] qué datos enviar

A continuación, cree una regla para que [!DNL Launch] sepa qué datos desea enviar a Adobe Experience Platform y cuándo desea enviarlos.

1. En la ficha **[!UICONTROL Reglas]**, configure un evento que déclencheur en cada nueva página del sitio Web cuando se cargue la biblioteca [!DNL Launch].

   ![imagen](assets/launch-make-a-rule.png)

1. Añada una acción.

   Para configurar la acción, indique [!DNL Launch] dónde encontrar la capa de datos. La capa de datos es un objeto JavaScript que existe en la página y que se entrega desde el mismo CMS que procesa la página web. Proporcione la ruta de JavaScript al objeto de datos.

   ![imagen](assets/launch-add-aep-action.png)

   El objeto de datos que envía debe ser XDM válido que pase la validación con el esquema que utiliza el conjunto de datos conectado a su ID de configuración.

1. Seleccione **[!UICONTROL Mantener cambios]**.

Para obtener más información, consulte [Reglas](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) en la documentación de [!DNL Launch].

## Agrupar la extensión y la regla en una biblioteca

A continuación, [agrupe la extensión](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) y la nueva regla en una biblioteca y pruebe esos cambios en un entorno de desarrollo.

![imagen](assets/launch-add-changes-to-library.png)

Después de completar la prueba, promocione la biblioteca a través del flujo de trabajo para que se pueda implementar en el sitio de producción. Los datos fluyen desde cada usuario individual a Adobe Experience Platform.

![imagen](assets/launch-promote-library.png)

Para obtener más información, consulte [Bibliotecas](https://docs.adobe.com/content/help/es-ES/launch/using/reference/publish/libraries.html) en la documentación de [!DNL Launch].