---
keywords: Experience Platform;fórmula de ventas minoristas;Data Science Workspace;temas populares;fórmulas
solution: Experience Platform
title: Crear el esquema de ventas minoristas y el conjunto de datos
type: Tutorial
description: Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás tutoriales de Adobe Experience Platform Data Science Workspace. Una vez finalizados, el esquema y los conjuntos de datos de ventas minoristas estarán disponibles para usted y los miembros de su organización en Experience Platform.
exl-id: 1b868c8c-7c92-4f99-8486-54fd7aa1af48
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---


# Creación del esquema de ventas minoristas y el conjunto de datos

Este tutorial le proporciona los requisitos previos y los recursos necesarios para todos los demás [!DNL Adobe Experience Platform] [!DNL Data Science Workspace] tutoriales. Una vez finalizados, el esquema y los conjuntos de datos de ventas minoristas estarán disponibles para usted y los miembros de su organización en [!DNL Experience Platform].

## Primeros pasos

Antes de iniciar este tutorial, debe cumplir los siguientes requisitos previos:
- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.
- Autorización para realizar [!DNL Experience Platform] Llamadas de API. Complete la [Autenticar y acceder a las API de Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) tutorial para obtener los siguientes valores con el fin de completar correctamente este tutorial:
   - Autorización: `{ACCESS_TOKEN}`
   - x-api-key: `{API_KEY}`
   - x-gw-ims-org-id: `{ORG_ID}`
   - Secreto de cliente: `{CLIENT_SECRET}`
   - Certificado de cliente: `{PRIVATE_KEY}`
- Datos de ejemplo y archivos de origen para [Fórmula de ventas minoristas](../pre-built-recipes/retail-sales.md). Descargue los recursos necesarios para este y otros [!DNL Data Science Workspace] tutoriales de [Adobe del repositorio Git público](https://github.com/adobe/experience-platform-dsw-reference/).
- [Python >= 2.7](https://www.python.org/downloads/) y lo siguiente [!DNL Python] paquetes:
   - [pipa](https://pypi.org/project/pip/)
   - [PyYAML](https://pyyaml.org/)
   - [dictor](https://pypi.org/project/dictor/)
   - [JWT](https://pypi.org/project/jwt/)
- Una comprensión práctica de los siguientes conceptos utilizados en este tutorial:
   - [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)
   - [Conceptos básicos de composición de esquemas](../../xdm/schema/field-dictionary.md)

## Crear esquema y conjunto de datos de ventas minoristas

El esquema y los conjuntos de datos de ventas minoristas se crean automáticamente mediante el script de bootstrap proporcionado. Siga los pasos a continuación en orden:

### Configuración de archivos

1. Dentro de [!DNL Experience Platform] paquete de recursos del tutorial, vaya al directorio `bootstrap`, y abra `config.yaml` utilizar un editor de texto adecuado.
2. En el `Enterprise` , introduzca los siguientes valores:

   ```yaml
   Enterprise:
       api_key: {API_KEY}
       org_id: {ORG_ID}
       tech_acct: {technical_account_id}
       client_secret: {CLIENT_SECRET}
       priv_key_filename: {PRIVATE_KEY}
   ```

3. Edite los valores que se encuentran en `Platform` , Ejemplo mostrado a continuación:

   ```yaml
   Platform:
       platform_gateway: https://platform.adobe.io
       ims_token: {ACCESS_TOKEN}
       ingest_data: "True"
       build_recipe_artifacts: "False"
       kernel_type: Python
   ```

   - `platform_gateway`: Ruta base para llamadas API. No modifique este valor.
   - `ims_token`: su `{ACCESS_TOKEN}` va aquí.
   - `ingest_data`: Para los fines de este tutorial, establezca este valor como `"True"` para crear los esquemas y conjuntos de datos de ventas minoristas. Un valor de `"False"` solo creará los esquemas.
   - `build_recipe_artifacts`: Para los fines de este tutorial, establezca este valor como `"False"` para evitar que el script genere un artefacto de fórmula.
   - `kernel_type`: el tipo de ejecución del artefacto de fórmula. Deje este valor como `Python` if `build_recipe_artifacts` se ha establecido como `"False"`, de lo contrario, especifique el tipo de ejecución correcto.

4. En el `Titles` , proporcione la siguiente información de forma adecuada para los datos de muestra de ventas minoristas, guarde y cierre el archivo una vez realizadas las ediciones. Ejemplo mostrado a continuación:

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

1. Abra la aplicación de terminal y vaya a [!DNL Experience Platform] directorio de recursos del tutorial.
2. Configure las variables `bootstrap` como la ruta de trabajo actual y ejecute el `bootstrap.py` [!DNL Python] escriba el siguiente comando para crear un script:

   ```bash
   python bootstrap.py
   ```

   >[!NOTE]
   >
   >El script puede tardar varios minutos en completarse.

## Pasos siguientes

Una vez completado correctamente el script de bootstrap, los esquemas de entrada y salida de las ventas minoristas y los conjuntos de datos se pueden ver en [!DNL Experience Platform]. Consulte la [tutorial de previsualización de datos de esquema](./preview-schema-data.md)
para obtener más información.

También ha introducido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] utilizando el script de bootstrap proporcionado.

Para seguir trabajando con los datos introducidos:
- [Analice sus datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilice Jupyter Notebooks en el espacio de trabajo de ciencia de datos para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] empaquetando archivos de origen en un archivo de fórmula importable.
