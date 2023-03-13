---
title: Atributos derivados
description: Los atributos derivados proporcionan un medio cómodo para generar atributos de su elección que se pueden actualizar en cualquier cadencia normal y, opcionalmente, publicar en los datos de Perfil del cliente en tiempo real. Este documento proporciona información general sobre cómo utilizar el servicio de consulta para crear atributos derivados para utilizarlos con los datos del perfil.
exl-id: 5d52b268-e2a3-411c-8242-3aa32e759937
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Atributos derivados

La función de atributos derivados proporciona un medio cómodo para generar atributos de su elección a partir de otra información disponible en el lago de datos. Estos atributos se pueden actualizar en cualquier cadencia normal y, opcionalmente, publicar en los datos del perfil del cliente en tiempo real. Los atributos derivados abordan la necesidad de crear atributos complejos como decil, percentil y cuartil sobre otros más sencillos, como máximo, recuento y media. Estos atributos se pueden calcular específicamente para un usuario individual o para una entidad empresarial. Esto permite derivar atributos que se pueden acreditar directamente a un identificador, como direcciones de correo electrónico, ID de dispositivo y números de teléfono, y también derivar atributos que se asocian indirectamente con ese perfil de usuario o empresarial.

Los atributos derivados son necesarios para una variedad de casos de uso cuando los datos se analizan en el lago de datos. Estos datos se pueden marcar para su uso en el Perfil del cliente en tiempo real y utilizar en casos de uso descendente, como la creación de audiencias específicas. Algunos casos de uso potenciales de esta función pueden incluir:

* Identificación del 10 % más bajo de suscriptores según el público por canal. Esto permite a los especialistas en marketing dirigirse a una audiencia concreta y vender un nuevo paquete de suscriptores.
* Identificación de una audiencia que está en el 10 % de los mejores volantes en función de sus millas totales recorridas y que tiene el estado &quot;Volante&quot;. Esta audiencia podría utilizarse para segmentar selectivamente la venta de una nueva oferta de tarjeta de crédito.
* Determine la tasa de pérdida en función de la suscripción.
* Identificar el 1% superior del ingreso familiar en una provincia o estado, y proporcionar una medida del número de individuos que se mudan de ese grupo colectivo en los últimos &quot;n&quot; meses.

## Atributos derivados complejos

Para crear una clasificación basada en una o más métricas (como ingresos, duración de la audiencia, etc.) de una dimensión (categoría) concreta, se requieren atributos derivados complejos. Los deciles, cuartiles y percentiles permiten flexibilidad y precisión al clasificar datos con atributos derivados.

Un decilo es un método para dividir un conjunto de datos clasificados en 10 partes iguales. Cuando los datos se dividen en deciles, se asigna un rango de deciles a cada fila del conjunto de datos. Esto permite ordenar los datos en orden descendente o ascendente.

Una clasificación de decilos organiza los datos en orden de menor a mayor y se realiza en una escala de 1 a 10, donde cada número sucesivo corresponde a un aumento de 10 puntos porcentuales.

Los cubos de decilos representan el número de grupos clasificados y se utilizan para asignar una clasificación a una dimensión (categoría) en el conjunto de datos. El bloque puede ser un número o una expresión que se evalúe como un valor entero positivo para cada partición. Los contenedores no deben tener un valor nulo.

Los cuartiles se utilizan para dividir la distribución por cuatro y los percentiles por 100.

## Atributos derivados analíticos

El servicio de consulta proporciona funciones integradas, como la sesionización y el último contacto, entre otras, que se pueden aplicar a cualquier dato de serie temporal para generar atributos derivados relacionados con el negocio. Tiene la opción de basar estos atributos derivados analíticos en una o más identidades y, opcionalmente, publicar los datos en el perfil del cliente en tiempo real si es necesario.

Algunos casos de uso potenciales para este tipo de atributo derivado pueden incluir:

* Seguimiento de productos analizados durante una sesión de usuario que estaban agotados.
* Seguimiento de métricas populares, como tamaño, color o categoría de producto de los productos que se están explorando o comprando.
* Seguimiento del origen de la plataforma que llevó a una compra o navegación del producto.
* Seguimiento del elemento explorado más recientemente por una identidad.
* Métricas de seguimiento, como el número promedio de elementos en un carro de compras, el abandono del carro de compras o la frecuencia promedio de compra.

## Otros atributos derivados

También puede calcular métricas empresariales como un atributo derivado y utilizarlas junto con atributos simples como código postal o una métrica agregada como recuento total. Por ejemplo, un recuento total basado en una ciudad o provincia, o un recuento total basado en una categoría empresarial y una ciudad o provincia.

## Pasos siguientes y casos de uso

Al leer este documento, tiene una mejor comprensión de cómo los atributos derivados del servicio de consultas facilitan casos de uso complejos para maximizar la utilidad de los datos. A continuación, debería leer la [caso de uso de atributo derivado basado en decilos](../../use-cases/deciles-use-case.md) para ver cómo se aplica esta función en un escenario real.
