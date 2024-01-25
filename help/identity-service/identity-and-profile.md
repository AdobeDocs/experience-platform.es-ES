---
title: Servicio de identidad y perfil del cliente en tiempo real
description: Obtenga información acerca de la relación entre el servicio de identidad y el perfil del cliente en tiempo real
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 1%

---

# Explicación de la relación entre el servicio de identidad y el perfil del cliente en tiempo real

>[!IMPORTANT]
>
>En esta página se da por hecho que la política de combinación utiliza el gráfico de identidad. Para obtener más información sobre las políticas de combinación en el Perfil del cliente en tiempo real, lea la documentación sobre [políticas de combinación y vinculación de identidad](../profile/merge-policies/overview.md#identity-stitching).

Aunque puede utilizar el servicio de identidad y el perfil del cliente en tiempo real juntos, las dos funciones de Adobe Experience Platform no son inherentemente iguales.

* Puede utilizar el servicio de identidad para generar y mantener el gráfico de identidad que reúne las distintas identidades de un cliente individual.
* Puede utilizar el Perfil del cliente en tiempo real para reunir fragmentos de perfil dispares y crear un perfil combinado. Este proceso requiere el uso del gráfico de identidad.

Este documento describe las similitudes, diferencias y relaciones entre el servicio de identidad y el perfil del cliente en tiempo real.

## Servicio de identidad frente a Perfil del cliente en tiempo real

Las principales diferencias entre el servicio de identidad y el perfil del cliente en tiempo real son las siguientes:

| | Servicio de identidad | Perfil del cliente en tiempo real |
| --- | --- |--- |
| **Finalidad** | <ul><li>Puede utilizar el servicio de identidad para crear y administrar gráficos de identidad.</li></ul> | Puede utilizar el Perfil del cliente en tiempo real para lo siguiente: <ul><li>Cree una vista de 360 grados de un perfil de cliente.</li><li>Ver y administrar perfiles.</li></ul> |
| **Entrada** | <ul><li>Para utilizar el servicio de identidad, debe introducir datos de registro o eventos de series temporales que tengan al menos dos campos marcados como identidad. Los campos que marca como identidad se incorporan al servicio de identidad.</li></ul> | <ul><li>Fragmentos de perfil: representan una identidad principal única y los datos de registro o evento correspondientes para ese ID dentro de un conjunto de datos determinado.</li><li>Gráficos de identidad: el perfil hace referencia al gráfico de identidad de un perfil de cliente determinado para identificar todos los fragmentos de perfil con las mismas identidades principales.</li></ul> |
| **Proceso** | <ul><li>Una vez que haya introducido al menos dos identidades, el servicio de identidad las vinculará.</li></ul> | <ul><li>El perfil del cliente en tiempo real combina fragmentos de perfil al tiempo que hace referencia a sus gráficos de identidad correspondientes.</li></ul> |
| **Output** | <ul><li>El resultado es un gráfico de identidad, que es un conjunto de identidades relacionadas con un individuo.</li></ul> | <ul><li>El resultado es un perfil combinado, que es una vista única y completa de un cliente determinado. Este perfil puede cumplir los requisitos para un segmento.</li></ul> |

{style="table-layout:auto"}

## Proceso de creación de perfiles combinados

Lea los pasos siguientes para comprender mejor el proceso de creación de un perfil combinado:

* En primer lugar, el Perfil del cliente en tiempo real hace referencia a un gráfico de identidades y recupera todas las identidades.
* A continuación, Perfil recupera fragmentos de perfil con identidades principales en el gráfico de identidades.
* Una vez realizada la acción correctamente, Profile than combina todos los eventos y atributos existentes.
   * Si hay información de atributos en conflicto, los atributos se eligen según el método de combinación. Para obtener más información, lea la [resumen de políticas de combinación](../profile/merge-policies/overview.md).

![Diagrama de flujo que detalla el funcionamiento del servicio de identidad y la combinación de perfiles.](./images/merge-profile-process.png)

## Designación de un campo como identidad

En el modelo de datos de experiencia (XDM), marcar o designar un campo como identidad es una instrucción para que el Experience Platform introduzca ese campo en particular en el servicio de identidad. A continuación, esta designación permite combinar fragmentos de perfil en el Perfil del cliente en tiempo real. Si no hay fragmentos de perfil asociados a la identidad, no la designe como identidad.

### Explicación de las identidades principales y secundarias

Una vez marcados los campos como identidades, se pueden definir como identidades principales o secundarias. Las identidades principales y secundarias son conceptos que forman parte del Perfil del cliente en tiempo real.

* La identidad principal (a veces denominada &quot;clave principal&quot;) es la identidad en la que se almacenan los fragmentos de perfil.
* Si solo hay una identidad en una fila de datos determinada, esa identidad única se designa como principal.
* Si hay dos o más identidades, una se designará como principal y la otra como secundaria.

El servicio de identidad establecerá vínculos entre identidades siempre que haya al menos dos campos marcados como identidad. El servicio de identidad no almacena información sobre si una identidad es principal o secundaria.

