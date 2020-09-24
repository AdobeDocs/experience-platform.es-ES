---
keywords: Experience Platform;retail sales recipe;Data Science Workspace;popular topics;recipes
solution: Experience Platform
title: Crear el esquema y conjunto de datos de ventas minoristas
topic: tutorial
type: Tutorial
description: Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás tutoriales de Adobe Experience Platform Data Science Workspace. Una vez finalizado, el esquema de ventas minoristas y los conjuntos de datos estarán disponibles para usted y los miembros de su organización de IMS en Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Crear el esquema y conjunto de datos de ventas minoristas

Este tutorial le proporciona los requisitos previos y los recursos necesarios para el resto [!DNL Adobe Experience Platform] de tutoriales [!DNL Data Science Workspace] . Una vez finalizado, el esquema de ventas minoristas y los conjuntos de datos estarán disponibles para usted y los miembros de su organización de IMS en [!DNL Experience Platform].

## Primeros pasos

Antes de iniciar este tutorial, debe tener los siguientes requisitos previos:
- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.
- Autorización para realizar llamadas [!DNL Experience Platform] de API. Complete el tutorial [Autenticar y acceder a las API](../../tutorials/authentication.md) de Adobe Experience Platform para obtener los siguientes valores y completar este tutorial con éxito:
   - Autorización: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Client secret: `{CLIENT_SECRET}`
   - Certificado de cliente: `{PRIVATE_KEY}`
- Datos de muestra y archivos de origen para la fórmula de venta [minorista](../pre-built-recipes/retail-sales.md). Descargue los recursos necesarios para este y otros [!DNL Data Science Workspace] tutoriales del repositorio [Git público de](https://github.com/adobe/experience-platform-dsw-reference/)Adobe.
- [Python >= 2.7](https://www.python.org/downloads/) y los siguientes [!DNL Python] paquetes:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una explicación práctica de los siguientes conceptos utilizados en este tutorial:
   - [[!Modelo de datos de experiencia DNL (XDM)]](../../xdm/home.md)
   - [Conceptos básicos de la composición de esquemas](../../xdm/schema/field-dictionary.md)

## Crear esquema y conjunto de datos de ventas minoristas

El esquema de ventas minoristas y los conjuntos de datos se crean automáticamente mediante la secuencia de comandos de arranque proporcionada. Siga los pasos a continuación en orden:

### Configuración de archivos

1. Dentro del paquete de recursos del [!DNL Experience Platform] tutorial, navegue hasta el directorio `bootstrap`y abra `config.yaml` con un editor de texto adecuado.
2. En la `Enterprise` sección , introduzca los siguientes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite los valores que se encuentran en la sección `Platform` , Ejemplo que se muestra a continuación:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :: La ruta de acceso base para llamadas de API. No modifique este valor.
   - `ims_token` :: Tu `{ACCESS_TOKEN}` va aquí.
   - `ingest_data` :: Para este tutorial, establezca este valor como `"True"` para crear los esquemas y conjuntos de datos de ventas minoristas. Un valor de sólo `"False"` creará los esquemas.
   - `build_recipe_artifacts` :: A los efectos de este tutorial, establezca este valor como `"False"` para evitar que la secuencia de comandos genere un artefacto de fórmula.
   - `kernel_type` :: Tipo de ejecución del artefacto de fórmula. Deje este valor como `Python` si `build_recipe_artifacts` se configura como `"False"`; de lo contrario, especifique el tipo de ejecución correcto.

4. En la `Titles` sección, proporcione la siguiente información de manera adecuada para los datos de muestra de Ventas al por menor, guarde y cierre el archivo después de realizar las ediciones. Ejemplo que se muestra a continuación:

   ```yaml
   Titles:
       input_class_title: retail_sales_input_class
       input_mixin_title: retail_sales_input_mixin
       input_mixin_definition_title: retail_sales_input_mixin_definition
       input_schema_title: retail_sales_input_schema
       input_dataset_title: retail_sales_input_dataset
       file_replace_tenant_id: DSWRetailSalesForXDM0.9.9.9.json
       file_with_tenant_id: DSWRetailSales_with_tenant_id.json
       is_output_schema_different: "True"
       output_mixin_title: retail_sales_output_mixin
       output_mixin_definition_title: retail_sales_output_mixin_definition
       output_schema_title: retail_sales_output_title
       output_dataset_title: retail_sales_output_dataset
   ```

### Ejecutar la secuencia de comandos de arranque

1. Abra la aplicación terminal y vaya al directorio de recursos del [!DNL Experience Platform] tutorial.
2. Defina el `bootstrap` directorio como la ruta de trabajo actual y ejecute la `bootstrap.py` secuencia de comandos [!DNL Python] introduciendo el siguiente comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >La secuencia de comandos puede tardar varios minutos en completarse.

## Pasos siguientes

Una vez finalizado correctamente el script de arranque, se pueden ver los esquemas y conjuntos de datos de entrada y salida de Retail Sales en [!DNL Experience Platform]. Consulte el tutorial [de datos de esquema de](./preview-schema-data.md)previsualización para obtener más información.

También ha ingerido correctamente los datos de muestra de ventas minoristas en [!DNL Experience Platform] el uso de la secuencia de comandos de arranque proporcionada.

Para continuar trabajando con los datos ingestados:
- [Analizar los datos con los blocs de notas de Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilice los blocs de notas Jupyter en el área de trabajo de ciencia de datos para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo [!DNL Data Science Workspace] mediante el empaquetado de archivos de origen en un archivo de fórmula importable.