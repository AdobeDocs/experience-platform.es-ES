---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;resolución de problemas;API
title: Introducción a los atributos calculados
type: Documentation
description: Los atributos calculados son funciones para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Alpha) Resumen de atributos calculados

>[!IMPORTANT]
>
>Actualmente, la funcionalidad de atributos calculados está en formato alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin que sea necesario realizar manualmente cálculos complejos cada vez que se necesite la información. Estos valores de atributo calculados se pueden ver en un perfil, utilizarse para crear un segmento o acceder a ellos a través de una serie de patrones de acceso diferentes.

Esta guía le ayudará a comprender mejor la función de los atributos calculados dentro de Adobe Experience Platform.

## Explicación de los atributos calculados

Adobe Experience Platform permite importar y combinar fácilmente datos de varias fuentes para generar [!DNL Real-Time Customer Profiles]. Cada perfil contiene información importante relacionada con un individuo, como su información de contacto, preferencias e historial de compras, lo que proporciona una vista del cliente en 360 grados.

Parte de la información recopilada en el perfil se entiende fácilmente al leer los campos de datos directamente (por ejemplo, &quot;nombre&quot;), mientras que otros datos requieren realizar varios cálculos o depender de otros campos y valores para generar la información (por ejemplo, &quot;total de compra de por vida&quot;). Para que estos datos sean más fáciles de entender de un vistazo, [!DNL Platform] permite crear atributos calculados que realizan automáticamente estas referencias y cálculos, devolviendo el valor en el campo correspondiente.

Los atributos calculados incluyen la creación de una expresión, o &quot;regla&quot;, que funciona en los datos entrantes y almacena el valor resultante en un atributo de perfil. Las expresiones se pueden definir de varias formas diferentes, lo que permite especificar que una regla evalúe solo eventos entrantes, un evento entrante y datos de perfil, o un evento entrante, datos de perfil y eventos históricos.

### Casos de uso

Los casos de uso de los atributos calculados pueden variar desde cálculos simples hasta referencias muy complejas. Estos son algunos ejemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Porcentajes]:** Un atributo calculado simple podría incluir la toma de dos campos numéricos en un registro y su división para crear un porcentaje. Por ejemplo, puede tomar el número total de correos electrónicos enviados a un individuo y dividirlo por el número de correos electrónicos que abre el individuo. Si se mira el campo de atributo calculado resultante, se mostrará rápidamente el porcentaje del total de correos electrónicos abiertos por el individuo.
1. **[!UICONTROL Uso de aplicaciones]:** Otro ejemplo incluye la capacidad de agregar la cantidad de veces que un usuario abre la aplicación. Al rastrear el número total de aperturas de aplicaciones, en función de eventos abiertos individuales, puede enviar ofertas o mensajes especiales a los usuarios en su 100.ª apertura, lo que fomenta una participación más profunda con su marca.
1. **[!UICONTROL Valores de duración]:** Recopilar totales acumulados, como el valor de compra de por vida de un cliente, puede resultar muy difícil. Esto requiere actualizar el total histórico cada vez que se produce un nuevo evento de compra. Un atributo calculado le permite hacer esto mucho más fácilmente manteniendo el valor de duración en un único campo que se actualiza automáticamente después de cada evento de compra exitoso relacionado con el cliente.

## Limitaciones conocidas

### Disponibilidad retrasada de nuevos atributos calculados

La disponibilidad de los nuevos atributos calculados se puede retrasar hasta 2 horas después de que el atributo de esquema correspondiente se añada al esquema de unión.

Este retraso se debe a la configuración actual del almacenamiento en caché. Post-Alpha: se pudo aumentar la frecuencia de actualización de la caché.

### Seguimiento de dependencias en segmentos

Los atributos de esquema que ya se han utilizado en una expresión de definición de segmento, pero que luego se convierten en un atributo calculado, no se rastrearán como una dependencia de ese segmento.

Debido a que no se ha detectado ninguna dependencia, Experience Platform no evaluará automáticamente el atributo calculado asociado cada vez que se evalúe la definición del segmento.

Alternativamente, la creación de atributos calculados se puede administrar a través de un grupo de campos de esquema específico que agregue nuevos atributos calculados que no entren en conflicto con los atributos existentes. Otra alternativa es simplemente volver a crear el segmento con el seguimiento de dependencia correcto para los nuevos atributos calculados.
