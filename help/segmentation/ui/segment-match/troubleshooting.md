---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Coincidencia de segmentos;coincidencia de segmentos
solution: Experience Platform
title: Preguntas frecuentes sobre la coincidencia de segmentos
description: Coincidencia de segmentos es un servicio para compartir segmentos en Adobe Experience Platform que permite a dos o más usuarios de Platform intercambiar datos de segmentos de una manera segura, regulada y compatible con la privacidad.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# [!DNL Segment Match] preguntas más frecuentes

Esta guía proporciona respuestas a preguntas legales y de privacidad que se plantean a menudo sobre la coincidencia de segmentos de Adobe Experience Platform.

## ¿Qué datos se comparten durante la superposición de la estimación y cómo puede garantizar el Adobe que estas métricas se obtengan de forma segura?

![overlap-report.png](./images/overlap-report.png)

Ningún dato de cliente o segmento se mueve entre entornos limitados para obtener estas métricas de estimación de superposición. Las identidades aplicables preconfiguradas y seleccionadas por el cliente en cualquier entorno limitado dado se añaden a una estructura de datos probabilística en la que los propios ID se representan en un formato hash.

Se trata de un proceso unidireccional, lo que significa que los identificadores prehash originales no están expuestos y no se pueden aplicar ingeniería inversa.

Estas estructuras de datos tienen propiedades únicas que permiten a los ingenieros realizar operaciones de unión e intersección entre ellas, incluso si la información codificada está comprimida o tiene un cifrado hash graves. Estas operaciones permiten [!DNL Segment Match] para obtener la intersección estimada de dos estructuras de datos compuestas por ID de dos entornos limitados diferentes sin tener que comparar los valores reales. Since [!DNL Segment Match] solo utiliza las estructuras de datos, los ID nunca abandonan los almacenes de perfil de sus respectivas organizaciones con fines de estimación. Esto permite que el Adobe cumpla los requisitos de privacidad y seguridad de los clientes, a la vez que ofrece herramientas de estimación muy precisas para guiar los acuerdos de colaboración de datos.

## ¿Cuál es el proceso detrás de la designación de qué identidades reciben los ID de segmento compartidos?

[!DNL Segment Match] proporciona a los clientes una opción para configurar qué áreas de nombres utilizar en el servicio. Esta selección se aplica tanto al proceso de estimación descrito en la pregunta anterior como al proceso de transferencia de datos, en caso de que el cliente decida publicar la fuente en un entorno limitado de un socio.

El proceso de transferencia de datos entre las identidades cifradas de dos organizaciones diferentes se realiza en un entorno de cálculo neutro. El trabajo de transferencia de datos es propiedad de Adobe, y las organizaciones involucradas en la sociedad no tienen acceso a este entorno, ni tienen acceso a ningún registro que pueda resultar del trabajo de transferencia de datos.

Solo la pertenencia a segmentos se incorpora en los fragmentos de perfil superpuestos de una organización receptora y no se transfiere ninguna identidad adicional de la organización remitente a la organización receptora. El trabajo de transferencia de datos no lee información de identificación personal (PII) de texto sin formato porque [!DNL Segment Match] permite superposiciones solo en espacios de nombres cifrados SHA256 (correo electrónico/teléfono) siempre que los datos sean PII. Los resultados nunca se almacenan en el entorno de cálculo.
