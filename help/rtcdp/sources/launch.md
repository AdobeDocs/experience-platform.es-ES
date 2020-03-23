---
title: Tutorial Implemente etiquetas de sitios web con Adobe Launch
seo-title: Implementación de etiquetas de sitios web con Adobe Launch
description: Utilice Adobe Launch para implementar etiquetas de sitios web en Adobe Experience Platform
seo-description: Utilice Adobe Launch para implementar etiquetas de sitios web en Adobe Experience Platform
translation-type: tm+mt
source-git-commit: b8eda33a88b81dff5f3b45a131a5585a062519c2

---


# Tutorial: Implementación de etiquetas de sitios web con Adobe Launch

Este tutorial explica cómo implementar las etiquetas de su sitio web para enviar datos a Adobe Experience Platform mediante Adobe Launch.

## Requisitos previos

* El esquema y el conjunto de datos necesarios se crean en Plataforma.
* La configuración necesaria se ha implementado en Experience Edge y tiene el ID de configuración y el dominio de Edge coincidentes.
* La empresa CMS ya se ha configurado para entregar un objeto JavaScript en cada página con los datos que necesita enviar a Platform.

## Pasos

Este tutorial contiene los siguientes pasos:

1. Instale la extensión SDK web de Adobe Experience Platform.
1. Cree una regla para indicar a Launch qué datos enviar.
1. Agrupar la extensión y la regla en una biblioteca.

## Instalación de la extensión SDK web de Adobe Experience Platform

En primer lugar, instale la extensión SDK web de Adobe Experience Platform.

1. En Launch, abra la pestaña **[!UICONTROL Extensions]**.

   ![image](assets/launch-overview.png)

1. Seleccione la extensión del SDK web de la plataforma Adobe Experience Platform en el catálogo de Launch ExtensionSe abre la pantalla de configuración.

   ![image](assets/launch-extension-install.png)

   Para obtener más información, consulte [Extensiones](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) en la documentación de Launch.

1. Configurar la extensión de.

   Los únicos ajustes que necesita ahora son:

   * **ID de configuración:** Especifique el ID de configuración que obtuvo de su representante de Adobe.
   * **Dominio de Edge:** Especifique el dominio Edge que obtuvo de su representante de Adobe.

1. Haga clic **[!UICONTROL Save]** y continúe con el paso siguiente.

## Crear una regla que indique a Launch qué datos enviar

A continuación, cree una regla para que Launch sepa qué datos desea enviar a Adobe Experience Platform y cuándo desea enviarlos.

1. En la **[!UICONTROL Rules]** ficha , configure un evento que se activará en cada nueva página del sitio web cuando se cargue la biblioteca Iniciar.

   ![image](assets/launch-make-a-rule.png)

1. Añada una acción.

   Para configurar la acción, indique a Launch dónde buscar la capa de datos. La capa de datos es un objeto JavaScript que existe en la página y que se entrega desde el mismo CMS que procesa la página web. Proporcione la ruta de JavaScript al objeto de datos.

   ![image](assets/launch-add-aep-action.png)

   El objeto de datos que envía debe ser XDM válido que pase la validación con el esquema que utiliza el conjunto de datos conectado a su ID de configuración.

1. Haga clic en **[!UICONTROL Keep Changes]**.

Para obtener más información, consulte [Reglas](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) en la documentación de Launch.

## Agrupar la extensión y la regla en una biblioteca

A continuación, [agrupe la extensión](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) y la nueva regla en una biblioteca y pruebe esos cambios en un entorno de desarrollo.

![image](assets/launch-add-changes-to-library.png)

Después de completar la prueba, promocione la biblioteca a través del flujo de trabajo para que se pueda implementar en el sitio de producción. Ahora fluyen datos de cada usuario individual a Adobe Experience Platform.

![image](assets/launch-promote-library.png)

Para obtener más información, consulte [Bibliotecas](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) en la documentación de Launch.