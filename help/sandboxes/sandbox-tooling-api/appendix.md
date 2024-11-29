---
title: Apéndice de la guía API de Sandbox Tools
description: Este documento proporciona información complementaria relacionada con el trabajo con la API de herramientas de zona protegida.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# Apéndice de guía de API de zona protegida

Este documento proporciona información adicional relacionada con el trabajo con la API [!DNL Sandbox].

## Uso de parámetros de consulta {#query}

La API de herramientas de zona protegida admite el uso de parámetros de consulta para paginar y filtrar los resultados al enumerar paquetes.

>[!NOTE]
>
>`limit` se puede pasar e iniciar individualmente.

| Parámetro | Descripción |
| --- | --- |
| `limit` | Número máximo de registros que se devolverán en la respuesta. El límite predeterminado es 20. |
| `start` | Inicio de donde debe comenzar una lista subconfigurada de elementos. |
| `targetSandbox` | Representa el nombre de la zona protegida donde desea importar los artefactos. |
| `jobType` | El tipo de trabajo. Este valor puede ser `NEW`, `RESUME` o `ROLLBACK`. |
| `jobStatus` | El estado del trabajo. Este valor puede ser `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` o `CANCELLED`. |
| `requestType` | El tipo de solicitud. Este valor puede ser `EXPORT`, `IMPORT` o `COPY`. |
| `expiryPeriod` | Este período de tiempo especificado por el usuario define la fecha de caducidad del paquete (en días) desde el momento en que se publicó. Este valor no debe ser negativo. El valor predeterminado es de 90 días desde el momento en que se llama a la API de actualización o publicación. |
| `packageType` | El tipo de paquete. Este valor puede ser `PARTIAL` o `FULL`. |
| `status` | El estado del paquete. Este valor puede ser `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` o `PUBLISH_FAILED`. |
