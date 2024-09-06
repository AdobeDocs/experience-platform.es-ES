---
title: Ingesta de datos cifrados en la IU de fuentes de Workspace
description: Aprenda a introducir datos cifrados en el espacio de trabajo de la interfaz de usuario de fuentes.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 7%

---

# Ingesta de datos cifrados en la interfaz de usuario de orígenes

>[!AVAILABILITY]
>
>La compatibilidad con la ingesta de datos cifrados en la interfaz de usuario de fuentes está en versión beta y es posible que no esté disponible para su organización. La funcionalidad y la documentación están sujetas a cambios.

Puede ingerir archivos y carpetas de datos cifrados en Adobe Experience Platform mediante fuentes por lotes de almacenamiento en la nube. Con la ingesta de datos cifrados, puede aprovechar los mecanismos de cifrado asimétricos para transferir datos por lotes de forma segura a Experience Platform. Actualmente, los mecanismos de cifrado asimétrico admitidos son PGP y GPG.

Esta función está disponible para las siguientes fuentes:

* [Amazon S3]
* [blob de Azure]
* [Azure Data Lake Storage Gen2]
* [Almacenamiento de archivos de Azure]
* [Zona de aterrizaje de datos]
* [FTP]
* [Almacenamiento en la nube de Google]
* [HDFS]
* [Almacenamiento de objetos de Oracle]
* [SFTP]

Lea esta guía para obtener información sobre cómo ingerir datos cifrados con fuentes por lotes de almacenamiento en la nube mediante la interfaz de usuario.

## Introducción 

Es útil conocer las siguientes funciones y conceptos de los Experience Platform antes de trabajar con la ingesta de datos cifrados en la interfaz de usuario:

* [Fuentes](../../home.md): Use fuentes en Experience Platform para introducir datos de una aplicación de Adobe o de una fuente de datos de terceros.
* [Flujos de datos](../../../dataflows/home.md): los flujos de datos son representaciones de trabajos de datos que mueven datos a través del Experience Platform. Puede utilizar el espacio de trabajo de fuentes para crear flujos de datos que introduzcan datos de una fuente determinada en el Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): utilice las zonas protegidas en Experience Platform para crear particiones virtuales entre las instancias de Experience Platform y crear entornos dedicados al desarrollo o la producción.

### Esquema de alto nivel

1. Cree un par de claves de cifrado con el espacio de trabajo de orígenes en la interfaz de usuario de Experience Platform. De forma opcional, también puede crear un par de claves de verificación de firma para proporcionar una capa adicional de seguridad a los datos cifrados.
2. Utilice la clave pública para cifrar los datos.
3. Coloque los datos cifrados en su proveedor de almacenamiento en la nube. Durante este paso, también debe asegurarse de que tiene un archivo de muestra que puede utilizarse como referencia para asignar los datos de origen a un esquema Experience Data Model (XDM).
4. Introduzca los datos cifrados en Experience Platform creando una conexión de origen.
5. Al crear la conexión de origen, proporcione el ID de clave que corresponda a la clave pública que utilizó para cifrar los datos. Si también ha utilizado el mecanismo de par de claves de verificación de firma, también debe proporcionar el ID de clave de verificación de firma que corresponda a los datos cifrados.
6. Continúe con los pasos de creación del flujo de datos.

## Crear un par de claves de cifrado {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID de clave de cifrado"
>abstract="Proporcione el ID de la clave de cifrado que corresponde a la clave de cifrado que se utilizó para cifrar los datos de origen."

* En la interfaz de usuario de Platform, vaya al área de trabajo de orígenes y, a continuación, seleccione [!UICONTROL Pares de claves] en el encabezado superior.
* Se le dirigirá a una página que muestra una lista de pares de claves de cifrado existentes en su organización. Esta página proporciona información sobre el título, el ID, el tipo, el algoritmo de cifrado, la caducidad y el estado de una clave determinada. Para crear un nuevo par de claves, seleccione **[!UICONTROL Crear clave]**.
* A continuación, elija el tipo de clave que desea crear. Para crear una clave de cifrado, seleccione **[!UICONTROL Clave de cifrado]** y proporcione un título y una frase de contraseña para la clave de cifrado. La frase de contraseña es una capa adicional de protección para las claves de cifrado. Una vez creada, el Experience Platform almacena la frase de contraseña en un almacén seguro diferente de la clave pública. Debe proporcionar una cadena que no esté vacía como frase de contraseña.

### Crear una clave de verificación de firma {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Identificador de clave de verificación de firma"
>abstract="Proporcione el ID de la clave de verificación de firma que corresponda a los datos de origen cifrados y firmados."

## Introducir datos cifrados {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="¿Está cifrado el archivo?"
>abstract="Seleccione este conmutador si está introduciendo un archivo que ya está cifrado."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Seleccionar archivo de muestra"
>abstract="Debe introducir un archivo de muestra al ingerir datos cifrados para crear una asignación."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
