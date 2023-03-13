---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Coincidencia de segmentos;coincidencia de segmentos
solution: Experience Platform
title: Preguntas frecuentes sobre coincidencias de segmentos
description: La coincidencia de segmentos es un servicio de uso compartido de segmentos en Adobe Experience Platform que permite a dos o más usuarios de Platform intercambiar datos de segmentos de una manera segura, controlada y compatible con la privacidad.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 823eb549e5514a3201ba68ed395c69e202cb747f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# [!DNL Segment Match] preguntas más frecuentes

Esta guía proporciona respuestas a preguntas legales y de privacidad que se plantean a menudo sobre la coincidencia de segmentos de Adobe Experience Platform.

## ¿Qué datos se comparten durante las superposiciones de estimaciones y cómo puede el Adobe garantizar que estas métricas se obtengan de forma segura?

![overlap-report.png](./images/overlap-report.png)

No se mueven datos de clientes o segmentos entre zonas protegidas para obtener estas métricas de estimación de superposición. Las identidades aplicables seleccionadas por el cliente y con hash previo en cualquier zona protegida se agregan a una estructura de datos probabilística en la que los propios ID se representan en formato con hash.

Se trata de un proceso unidireccional, lo que significa que los identificadores originales con hash previo no se exponen y no se pueden analizar mediante ingeniería inversa.

Estas estructuras de datos tienen propiedades únicas que permiten a los ingenieros realizar operaciones de unión e intersección entre ellas, incluso si la información codificada está gravemente comprimida o con hash. Estas operaciones permiten [!DNL Segment Match] para obtener la intersección estimada de dos estructuras de datos compuestas de ID de dos zonas protegidas diferentes sin tener que comparar los valores reales. Desde [!DNL Segment Match] Cuando solo utiliza las estructuras de datos, los ID nunca abandonan los almacenes de perfil de sus respectivas organizaciones IMS con fines de estimación. Esto permite al Adobe cumplir con los requisitos de privacidad y seguridad de los clientes, al tiempo que ofrece herramientas de estimación muy precisas para guiar los acuerdos de colaboración de datos.

## ¿Cuál es el proceso detrás de la designación de qué identidades reciben los ID de segmento compartidos?

[!DNL Segment Match] proporciona a los clientes una opción para configurar qué áreas de nombres utilizar en el servicio. Esta selección se aplica tanto al proceso de estimación descrito en la pregunta anterior como al proceso de transferencia de datos, en caso de que el cliente decida publicar la fuente en un entorno limitado de socios.

El proceso de transferencia de datos entre las identidades cifradas de dos organizaciones diferentes se realiza en un entorno de cálculo neutro. El trabajo de transferencia de datos es propiedad de Adobe y las organizaciones involucradas en la asociación no tienen acceso a este entorno ni tienen acceso a ningún registro que pueda ser el resultado del trabajo de transferencia de datos.

Solo se incorpora la pertenencia a segmentos en los fragmentos de perfil superpuestos de una organización de IMS del receptor y no se transfiere ninguna identidad adicional de la organización de IMS del remitente a la organización de IMS del receptor. El trabajo de transferencia de datos no lee ningún texto sin formato con información de identificación personal (PII) porque [!DNL Segment Match] solo permite superposiciones en áreas de nombres cifradas SHA256 (correo electrónico/teléfono) siempre que los datos sean PII. Los resultados nunca se almacenan en el entorno de cálculo.
