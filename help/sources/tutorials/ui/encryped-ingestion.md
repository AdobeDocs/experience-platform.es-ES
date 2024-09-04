---
title: Ingesta de datos cifrados en la IU de fuentes de Workspace
description: Aprenda a introducir datos cifrados en el espacio de trabajo de la interfaz de usuario de fuentes.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# Ingesta de datos cifrados en la interfaz de usuario de orígenes

Lea esta guía para obtener información sobre cómo ingerir datos cifrados en Adobe Experience Platform mediante fuentes de almacenamiento en la nube para datos por lotes.

## Requisitos previos

* Cifrado de datos

## Introducir datos cifrados {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="¿Está cifrado el archivo?"
>abstract="Seleccione este conmutador si está introduciendo un archivo que ya está cifrado."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Seleccionar archivo de muestra"
>abstract="Debe introducir un archivo de muestra al ingerir datos cifrados para crear una asignación."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID de clave de cifrado"
>abstract="Proporcione el ID de la clave de cifrado que corresponde a la clave de cifrado que se utilizó para cifrar los datos de origen."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Identificador de clave de verificación de firma"
>abstract="Proporcione el ID de la clave de verificación de firma que corresponda a los datos de origen cifrados y firmados."

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
