---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Introducción a los atributos calculados
topic: guía
type: Documentación
description: Los atributos calculados son funciones para datos acumulados de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# (Alfa) Descripción general de los atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumulados datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Estos valores de atributos calculados se pueden ver en un perfil, utilizar para crear un segmento o acceder a ellos a través de una serie de patrones de acceso diferentes.

Esta guía le ayudará a comprender mejor la función de los atributos calculados dentro de Adobe Experience Platform.

## Explicación de los atributos calculados

Adobe Experience Platform le permite importar y combinar fácilmente datos de múltiples fuentes para generar [!DNL Real-time Customer Profiles]. Cada perfil contiene información importante relacionada con un individuo, como su información de contacto, preferencias e historial de compras, lo que proporciona una vista de 360 grados del cliente.

Parte de la información recopilada en el perfil se puede entender fácilmente al leer los campos de datos directamente (por ejemplo, &quot;nombre&quot;), mientras que otros datos requieren realizar varios cálculos o basarse en otros campos y valores para generar la información (por ejemplo, &quot;total de compras de duración&quot;). Para facilitar la comprensión de estos datos de un vistazo, [!DNL Platform] permite crear atributos calculados que realizan automáticamente estas referencias y cálculos, devolviendo el valor en el campo correspondiente.

Los atributos calculados incluyen la creación de una expresión, o &quot;regla&quot;, que funciona con los datos entrantes y almacena el valor resultante en un atributo de perfil. Las expresiones se pueden definir de varias formas diferentes, lo que le permite especificar que una regla evalúe únicamente los eventos entrantes, los datos de evento y perfil entrantes o los eventos de evento, perfil e historial entrantes.

### Casos de uso

Los casos de uso para atributos calculados pueden ir desde cálculos simples a referencias muy complejas. Estos son algunos ejemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Porcentajes]:** un atributo simple calculado podría incluir la toma de dos campos numéricos en un registro y su división para crear un porcentaje. Por ejemplo, puede tomar el número total de correos electrónicos enviados a un individuo y dividirlos por el número de correos electrónicos que se abre el individuo. Al consultar el campo de atributo calculado resultante, se mostraría rápidamente el porcentaje de correos electrónicos totales abiertos por el individuo.
1. **[!UICONTROL Uso] de la aplicación:** Otro ejemplo incluye la capacidad de acumulado del número de veces que un usuario abre la aplicación. Al rastrear el número total de aperturas de aplicaciones, en función de eventos abiertos individuales, puede enviar ofertas o mensajes especiales a los usuarios en su 100° número de aperturas, lo que estimula un compromiso más profundo con su marca.
1. **[!UICONTROL Valores] de duración:** recopilar totales de ejecución, como un valor de compra de duración para un cliente, puede ser muy difícil. Esto requiere actualizar el total histórico cada vez que se produce un nuevo evento de compra. Un atributo calculado le permite hacerlo mucho más fácilmente manteniendo el valor de duración en un solo campo que se actualiza automáticamente después de cada evento de compra exitoso relacionado con el cliente.

## Limitaciones conocidas

### Disponibilidad retrasada de nuevos atributos calculados

La disponibilidad de nuevos atributos calculados puede retrasarse hasta 2 horas después de que se añada el atributo de esquema correspondiente al esquema de unión.

Este retraso se debe a la configuración actual del almacenamiento en caché. Después de alfa, la frecuencia de actualización de caché podría aumentar.

### Seguimiento de dependencia en segmentos

Los atributos de esquema que ya se han utilizado en una expresión de definición de segmento, pero que posteriormente se convirtieron en un atributo calculado, no se rastrearán como una dependencia de ese segmento.

Debido a que no se ha detectado ninguna dependencia, el Experience Platform no evaluará automáticamente el atributo calculado asociado cada vez que se evalúe la definición del segmento.

De forma alternativa, la creación de atributos calculados podría gestionarse mediante una combinación específica que agregue nuevos atributos calculados que no entren en conflicto con los atributos existentes. Otra alternativa es simplemente volver a crear el segmento con el seguimiento de dependencia correcto para los nuevos atributos calculados.