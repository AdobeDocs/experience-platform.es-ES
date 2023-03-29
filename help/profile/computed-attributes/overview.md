---
keywords: Experience Platform;perfil;perfil del cliente en tiempo real;solución de problemas;API
title: Introducción a los atributos calculados
type: Documentation
description: Los atributos calculados son funciones para agregar datos de nivel de evento a atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Alpha) Resumen de los atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo computado está actualmente en alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización.

Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con elementos como el valor de compra de por vida, el tiempo entre compras o el número de aperturas de aplicaciones, sin que sea necesario realizar cálculos complejos manualmente cada vez que se necesite la información. Estos valores de atributo calculados se pueden ver en un perfil, utilizarse para crear un segmento o acceder a ellos a través de una serie de patrones de acceso diferentes.

Esta guía le ayudará a comprender mejor la función de los atributos calculados dentro de Adobe Experience Platform.

## Explicación de los atributos calculados

Adobe Experience Platform permite importar y combinar fácilmente datos de múltiples fuentes para generar [!DNL Real-Time Customer Profiles]. Cada perfil contiene información importante relacionada con un individuo, como su información de contacto, preferencias e historial de compras, lo que proporciona una vista de 360 grados del cliente.

Parte de la información recopilada en el perfil se entiende fácilmente al leer los campos de datos directamente (por ejemplo, &quot;nombre&quot;), mientras que otros datos requieren realizar varios cálculos o basarse en otros campos y valores para generar la información (por ejemplo, &quot;total de compra de por vida&quot;). Para facilitar la comprensión de estos datos de un vistazo, [!DNL Platform] permite crear atributos calculados que realizan automáticamente estas referencias y cálculos, devolviendo el valor en el campo correspondiente.

Los atributos calculados incluyen la creación de una expresión, o &quot;regla&quot;, que funcione con los datos entrantes y almacene el valor resultante en un atributo de perfil. Las expresiones se pueden definir de varias formas diferentes, lo que permite especificar que una regla evalúe solo los eventos entrantes, un evento y datos de perfil entrantes o un evento entrante, datos de perfil y eventos históricos.

### Casos de uso

Los casos de uso para atributos calculados pueden abarcar desde cálculos simples a referencias muy complejas. Estos son algunos ejemplos de casos de uso para atributos calculados:

1. **[!UICONTROL Porcentajes]:** Un atributo simple calculado podría incluir la toma de dos campos numéricos en un registro y su división para crear un porcentaje. Por ejemplo, puede tomar el número total de correos electrónicos enviados a un individuo y dividirlo por el número de correos electrónicos que el individuo abre. Si consulta el campo de atributo calculado resultante, se mostraría rápidamente el porcentaje de correos electrónicos totales abiertos por el individuo.
1. **[!UICONTROL Uso de aplicaciones]:** Otro ejemplo incluye la capacidad de agregar el número de veces que un usuario abre la aplicación. Al rastrear el número total de aperturas de aplicaciones, según los eventos abiertos individuales, puede enviar ofertas o mensajes especiales a los usuarios en su centésima apertura, lo que fomenta una mayor participación en su marca.
1. **[!UICONTROL Valores de duración]:** Recopilar totales en ejecución, como un valor de compra de por vida para un cliente, puede ser muy difícil. Esto requiere actualizar el total histórico cada vez que se produce un nuevo evento de compra. Un atributo calculado permite hacerlo con mucha más facilidad al mantener el valor de duración en un único campo que se actualiza automáticamente después de cada evento de compra exitoso relacionado con el cliente.

## Limitaciones conocidas

### Disponibilidad retrasada de los nuevos atributos calculados

La disponibilidad de los nuevos atributos calculados puede retrasarse hasta 2 horas después de añadir el atributo de esquema correspondiente al esquema de unión.

Este retraso se debe a la configuración actual del almacenamiento en caché. Después de Alpha, se podría aumentar la frecuencia de actualización de la caché.

### Seguimiento de dependencias en segmentos

Los atributos de esquema que ya se han utilizado en una expresión de definición de segmento, pero que posteriormente se convirtieron en un atributo calculado, no se rastrearán como una dependencia de ese segmento.

Debido al hecho de que no se ha detectado ninguna dependencia, el Experience Platform no evaluará automáticamente el atributo calculado asociado cada vez que se evalúe la definición del segmento.

Alternativamente, la creación de atributos calculados se puede administrar a través de un grupo de campos de esquema específico que agregue nuevos atributos calculados que no entren en conflicto con los atributos existentes. Otra alternativa es simplemente volver a crear el segmento con el seguimiento de dependencia correcto para los nuevos atributos calculados.
