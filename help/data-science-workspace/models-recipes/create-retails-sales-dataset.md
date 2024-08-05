---
keywords: Experience Platform;fórmula de ventas minoristas;Data Science Workspace;temas populares;fórmulas
solution: Experience Platform
title: Crear el esquema de ventas minoristas y el conjunto de datos
type: Tutorial
description: Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás tutoriales de Adobe Experience Platform Data Science Workspace. Una vez finalizados, el esquema y los conjuntos de datos de ventas minoristas estarán disponibles para usted y los miembros de su organización en Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---


# Creación del esquema de ventas minoristas y el conjunto de datos

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Este tutorial le proporciona los requisitos previos y los recursos necesarios para los demás tutoriales de [!DNL Adobe Experience Platform] [!DNL Data Science Workspace]. Una vez finalizados, el esquema y los conjuntos de datos de ventas minoristas estarán disponibles para usted y los miembros de su organización en [!DNL Experience Platform].

## Introducción

Antes de iniciar este tutorial, debe cumplir los siguientes requisitos previos:
- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.
- Autorización para hacer llamadas a la API [!DNL Experience Platform]. Complete el tutorial [Autenticar y acceder a las API de Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para obtener los siguientes valores y poder completar correctamente este tutorial:
   - Autorización: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Secreto de cliente: `{CLIENT_SECRET}`
   - Certificado de cliente: `{PRIVATE_KEY}`
- Datos de muestra y archivos de origen para la [fórmula de ventas minoristas](../pre-built-recipes/retail-sales.md). Descargue los recursos necesarios para este y otros [!DNL Data Science Workspace] tutoriales desde el [repositorio Git público de Adobe](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) y los siguientes [!DNL Python] paquetes:
   - [pip](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [diccionario](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una comprensión práctica de los siguientes conceptos utilizados en este tutorial:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Conceptos básicos de composición de esquemas](../../xdm/schema/field-dictionary.md)

## Crear esquema y conjunto de datos de ventas minoristas

El esquema y los conjuntos de datos de ventas minoristas se crean automáticamente mediante el script de bootstrap proporcionado. Siga los pasos a continuación en orden:

### Configuración de archivos

1. Dentro del paquete de recursos del tutorial [!DNL Experience Platform], vaya al directorio `bootstrap` y abra `config.yaml` con un editor de texto adecuado.
2. En la sección `Enterprise`, escriba los siguientes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite los valores encontrados en la sección `Platform`; el ejemplo se muestra a continuación:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: ruta de acceso base para las llamadas API. No modifique este valor.
   - `ims_token`: Su `{ACCESS_TOKEN}` se va aquí.
   - `ingest_data`: a los efectos de este tutorial, establezca este valor como `"True"` para crear los esquemas y conjuntos de datos de ventas minoristas. Un valor de `"False"` solo creará los esquemas.
   - `build_recipe_artifacts`: a los efectos de este tutorial, establezca este valor como `"False"` para evitar que el script genere un artefacto de fórmula.
   - `kernel_type`: el tipo de ejecución del artefacto de fórmula. Deje este valor como `Python` si `build_recipe_artifacts` está establecido como `"False"`; de lo contrario, especifique el tipo de ejecución correcto.

4. En la sección `Titles`, proporcione la siguiente información correctamente para los datos de muestra de ventas minoristas, guarde y cierre el archivo una vez realizadas las ediciones. Ejemplo mostrado a continuación:

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

### Ejecutar el script de bootstrap

1. Abra la aplicación de terminal y vaya al directorio de recursos del tutorial [!DNL Experience Platform].
2. Establezca el directorio `bootstrap` como la ruta de trabajo actual y ejecute el script `bootstrap.py` [!DNL Python] al escribir el siguiente comando:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >El script puede tardar varios minutos en completarse.

## Pasos siguientes

Una vez completado correctamente el script de bootstrap, los esquemas y conjuntos de datos de entrada y salida de ventas minoristas se pueden ver en [!DNL Experience Platform]. Ver el [tutorial de vista previa de datos de esquema](./preview-schema-data.md)
para obtener más información.

También ha ingerido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] mediante el script de arranque proporcionado.

Para seguir trabajando con los datos introducidos:
- [Analice sus datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilice Jupyter Notebooks en Data Science Workspace para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] empaquetando los archivos de origen en un archivo de fórmula importable.
