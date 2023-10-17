---
title: Servicio de identidad y perfil del cliente en tiempo real
description: Obtenga información acerca de la relación entre el servicio de identidad y el perfil del cliente en tiempo real
hide: true
hidefromtoc: true
source-git-commit: 03228eef47100096e98666966c4e5065eb7f478a
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Explicación de la relación entre el servicio de identidad y el perfil del cliente en tiempo real

>[!IMPORTANT]
>
>En esta página se da por hecho que la política de combinación utiliza el gráfico de identidad. Para obtener más información sobre las políticas de combinación en el Perfil del cliente en tiempo real, lea la documentación sobre [políticas de combinación y vinculación de identidad].

Aunque puede utilizar el servicio de identidad y el perfil del cliente en tiempo real juntos, las dos funciones de Adobe Experience Platform no son inherentemente iguales.

* Puede utilizar el servicio de identidad para generar y mantener el gráfico de identidad que reúne las distintas identidades de un cliente individual.
* Puede utilizar el Perfil del cliente en tiempo real para reunir fragmentos de perfil dispares y crear un perfil combinado. Este proceso requiere el uso del gráfico de identidad.

Este documento describe las similitudes, diferencias y relaciones entre el servicio de identidad y el perfil del cliente en tiempo real.

## Servicio de identidad frente a Perfil del cliente en tiempo real

Las principales diferencias entre el servicio de identidad y el perfil del cliente en tiempo real son las siguientes:

| | Servicio de identidad | Perfil del cliente en tiempo real |
| --- | --- |--- |
| **Finalidad** | <ul><li>Puede utilizar el servicio de identidad para crear y administrar gráficos de identidad.</li></ul> | Puede utilizar el Perfil del cliente en tiempo real para lo siguiente: <ul><li>Cree una vista de 360 grados de un perfil de cliente.</li><li>Visualización y administración de perfiles</li><li>Perfiles de segmentos para crear audiencias.</li></ul> |
| **Entrada** | <ul><li>Para utilizar el servicio de identidad, debe introducir datos de registro o eventos de series temporales que tengan al menos dos campos marcados como identidad. Los campos que marca como identidad se incorporan al servicio de identidad.</li></ul> | **Para combinar perfiles, debe proporcionar**: <ul><li>Fragmentos de perfil: representan una identidad principal única y los datos de registro o evento correspondientes para ese ID dentro de un conjunto de datos determinado.</li><li>Gráficos de identidad: el perfil hace referencia al gráfico de identidad de un perfil de cliente determinado para identificar todos los fragmentos de perfil con las mismas identidades principales.</li></ul> **Para la calificación de segmentos, debe proporcionar**: <ul><li>Perfiles combinados: un perfil combinado es una vista única de un cliente, donde se recopilan identidades y fragmentos de perfil dispares en una vista completa.</li></ul> |
| **Proceso** | <ul><li>Una vez que haya introducido al menos dos identidades, el servicio de identidad las vinculará.</li></ul> | <ul><li>El perfil del cliente en tiempo real combina fragmentos de perfil al tiempo que hace referencia a sus gráficos de identidad correspondientes.</li><li>Calificar perfiles para segmentos en función de criterios de segmentación</li></ul> |
| **Output** | <ul><li>El resultado es un gráfico de identidad, que es un conjunto de identidades relacionadas con un individuo.</li></ul> | <ul><li>El resultado es un perfil combinado, que es una vista única y completa de un cliente determinado.</li><li>Perfiles con suscripciones a segmentos definidas</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## ¿Cómo se crea un perfil combinado?

Lea los pasos siguientes para comprender mejor el proceso de creación de un perfil combinado:

* En primer lugar, el Perfil del cliente en tiempo real hace referencia a un gráfico de identidades y recupera todas las identidades.
* A continuación, Perfil recupera todos los fragmentos de perfil relacionados con cada identidad.
* Una vez realizada la acción correctamente, Profile than combina todos los eventos y atributos existentes.
   * Si es necesario, aplique reglas de prioridad para determinar qué atributo o evento utilizar

![Diagrama de flujo que detalla el funcionamiento del servicio de identidad y la combinación de perfiles.](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### ¿Qué significa marcar un campo como identidad?

Marcar o designar un campo como identidad es una instrucción para que el Experience Platform introduzca ese campo en particular en el servicio de identidad. A continuación, esta designación permite combinar fragmentos de perfil en el Perfil del cliente en tiempo real. Si no hay fragmentos de perfil asociados a la identidad, no la designe como identidad.

#### Explicación de las identidades principales y secundarias

Una vez marcados los campos como identidades, se pueden definir como identidades principales o secundarias. Las identidades principales y secundarias son conceptos que forman parte del Perfil del cliente en tiempo real.

* La identidad principal (a veces denominada &quot;clave principal&quot;) es la identidad en la que se almacenan los fragmentos de perfil.
* Si solo hay una identidad en una fila de datos determinada, esa identidad única se designa como principal.
* Si hay dos o más identidades, una se designará como principal y la otra como secundaria.

El servicio de identidad solo ingiere campos designados como identidad. El servicio de identidad no almacena información sobre si una identidad es principal o secundaria.

## Pasos siguientes

Para obtener más información sobre las reglas de vinculación de gráficos de identidad, lea la siguiente documentación:

* [Resumen de reglas de vinculación de gráficos de identidad](./overview.md)
* [Casos de ejemplo para configurar reglas de vinculación de gráficos de identidad](./example-scenarios.md)
* [Lógica de vinculación de identidad](./identity-linking-logic.md)