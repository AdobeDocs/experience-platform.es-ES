---
keywords: Experience Platform;fórmula de ventas minoristas;Área de trabajo de ciencia de datos;temas populares;fórmulas
solution: Experience Platform
title: Crear el esquema y conjunto de datos de ventas minoristas
topic: tutorial
type: Tutorial
description: Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás tutoriales de Adobe Experience Platform Data Science Workspace. Una vez finalizado, el esquema de ventas minoristas y los conjuntos de datos estarán disponibles para usted y los miembros de su organización de IMS en Experience Platform.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Crear el esquema y conjunto de datos de ventas minoristas

Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás tutoriales [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Al finalizar, el esquema de ventas minoristas y los conjuntos de datos estarán disponibles para usted y los miembros de su organización de IMS en [!DNL Experience Platform].

## Primeros pasos

Antes de iniciar este tutorial, debe tener los siguientes requisitos previos:
- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.
- Autorización para realizar [!DNL Experience Platform] llamadas de API. Complete el tutorial [Autentique y acceda a las API de Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para obtener los siguientes valores y completar este tutorial con éxito:
   - Autorización: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{IMS_ORG}`
   - Secreto del cliente: `{CLIENT_SECRET}`
   - Certificado de cliente: `{PRIVATE_KEY}`
- Archivos de origen y datos de muestra para la [fórmula de ventas minoristas](../pre-built-recipes/retail-sales.md). Descargue los recursos necesarios para este y otros [!DNL Data Science Workspace] tutoriales del [repositorio público Git de Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) y los siguientes  [!DNL Python] paquetes:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una explicación práctica de los siguientes conceptos utilizados en este tutorial:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Conceptos básicos de la composición de esquemas](../../xdm/schema/field-dictionary.md)

## Crear esquema y conjunto de datos de ventas minoristas

El esquema de ventas minoristas y los conjuntos de datos se crean automáticamente mediante la secuencia de comandos de arranque proporcionada. Siga los pasos a continuación en orden:

### Configuración de archivos

1. Dentro del paquete de recursos del tutorial [!DNL Experience Platform], navegue al directorio `bootstrap` y abra `config.yaml` con un editor de texto adecuado.
2. En la sección `Enterprise`, introduzca los siguientes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {IMS_ORG}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite los valores que se encuentran en la sección `Platform`, Ejemplo que se muestra a continuación:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway` :: La ruta de acceso base para llamadas de API. No modifique este valor.
   - `ims_token` :: Tu  `{ACCESS_TOKEN}` va aquí.
   - `ingest_data` :: Para este tutorial, establezca este valor como  `"True"` para crear los esquemas y conjuntos de datos de ventas minoristas. Un valor de `"False"` sólo creará los esquemas.
   - `build_recipe_artifacts` :: A los efectos de este tutorial, establezca este valor como  `"False"` para evitar que la secuencia de comandos genere un artefacto de fórmula.
   - `kernel_type` :: Tipo de ejecución del artefacto de fórmula. Deje este valor como `Python` si `build_recipe_artifacts` está establecido como `"False"`, de lo contrario especifique el tipo de ejecución correcto.

4. En la sección `Titles`, proporcione la siguiente información de manera adecuada para los datos de muestra de ventas minoristas, guarde y cierre el archivo después de que se hayan realizado las ediciones. Ejemplo que se muestra a continuación:

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

1. Abra la aplicación terminal y vaya al directorio de recursos del tutorial [!DNL Experience Platform].
2. Configure el directorio `bootstrap` como la ruta de trabajo actual y ejecute la secuencia de comandos `bootstrap.py` [!DNL Python] introduciendo el siguiente comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >La secuencia de comandos puede tardar varios minutos en completarse.

## Pasos siguientes

Una vez finalizado correctamente el script de arranque, los esquemas de entrada y salida de Retail Sales y los conjuntos de datos se pueden ver en [!DNL Experience Platform]. Consulte el [tutorial de datos de esquema de previsualización](./preview-schema-data.md)
para obtener más información.

También ha ingerido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] mediante la secuencia de comandos de arranque proporcionada.

Para continuar trabajando con los datos ingestados:
- [Analizar los datos con los blocs de notas de Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilice los blocs de notas Jupyter en el área de trabajo de ciencia de datos para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] mediante el empaquetado de archivos de origen en un archivo de fórmula importable.