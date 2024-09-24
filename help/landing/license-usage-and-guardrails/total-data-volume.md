---
title: Métrica de volumen total de datos
description: Obtenga información acerca de la nueva métrica Volumen total de datos y cómo reemplaza la métrica de riqueza de perfiles promedio anterior.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Métrica Volumen total de datos

A partir del 24 de septiembre de 2024, la métrica Volumen total de datos reemplazará a la métrica anterior de Riqueza promedio de perfiles.

Volumen total de datos representa la cantidad total de datos disponibles para el perfil del cliente en tiempo real de Adobe Experience Platform que se utilizará en los flujos de trabajo de participación. Este valor equivale a la métrica Audiencia direccionable multiplicada por la Riqueza media de perfiles.

## Preguntas frecuentes {#faq}

La siguiente sección enumera las preguntas más frecuentes sobre esta actualización.

### ¿Por qué se ha hecho este cambio?

Este cambio se ha realizado para simplificar el proceso de cumplimiento de las métricas de derechos de licencia. A menudo, los clientes nos han dicho que les resulta difícil comprender y gestionar la riqueza de perfiles promedio. Con este cambio, esperamos que pueda comprender y administrar mejor su uso con licencia del Perfil del cliente en tiempo real.

### ¿Este cambio en la métrica cambia mi derecho al almacén de perfiles?

No. El derecho al almacén de perfiles seguirá siendo el mismo que antes, ya que el volumen total de datos es equivalente a la audiencia direccionable multiplicada por la riqueza de perfiles promedio.

### ¿Este cambio afecta a los paquetes de derechos que he adquirido?

No. Todavía obtendrá los beneficios de los paquetes de derechos que compró anteriormente.

### ¿Cómo puedo ver un valor diferente para mi volumen total de datos en comparación con mi asignación de almacén de perfiles?

El volumen total de datos representa la **cantidad total** de datos disponibles para que el perfil los use en los flujos de trabajo de participación. La medición se ha actualizado para que sea más determinística y explicable. La mayoría de los usuarios **no** debería ver un cambio significativo entre su volumen total de datos y el almacenamiento total de su perfil. Si tiene alguna duda, póngase en contacto con el representante del servicio de atención al cliente.

### ¿Debo volver a crear los cambios para seguir administrando la riqueza promedio de perfiles?

No. Cualquier acción, como filtrar, deshabilitar el perfil para conjuntos de datos, así como configurar las caducidades de los eventos de experiencia y las caducidades de los datos del perfil seudónimo, seguirá desempeñando un papel en la administración del volumen total de datos.

### ¿Por qué el tamaño del archivo que he introducido en la zona protegida es diferente al volumen total de datos?

El perfil optimiza los datos para un procesamiento rápido a fin de ejecutar los flujos de trabajo de personalización y participación para los que está diseñado el sistema. El tamaño del archivo del lado del cliente puede ser diferente del volumen total de datos debido a factores como el tipo de codificación, compresión y formato.

### ¿Se aplica este cambio a los SKU que tienen un límite compartido tanto para el perfil como para el lago de datos?

Los clientes que estén en SKU que hayan compartido la riqueza de perfiles promedio entre el perfil y el lago de datos seguirán viendo la métrica Almacenamiento consumido total y **no** verán la métrica Riqueza de perfiles promedio.
