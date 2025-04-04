---
title: Información confidencial y personal en XDM
description: Obtenga información acerca de las consideraciones clave relacionadas con la información personal confidencial (SPI) y la información de identificación personal (PII) en el Experience Data Model (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Información confidencial y personal en XDM

El modelo de datos de experiencia (XDM) proporciona estructuras de datos estándar para su uso en Adobe Experience Platform, lo que le permite recopilar datos sobre las experiencias de los clientes. Estos datos pueden incluir información personal confidencial (SPI) e información de identificación personal (PII), como la dirección de correo electrónico, el nombre, el ID de cuenta y otros campos de datos de un cliente.

Las reglas organizativas y las regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD), aplican restricciones sobre cómo se pueden recopilar, almacenar, utilizar y compartir los SPI y PII. Por lo tanto, es importante tener en cuenta qué campos representan información confidencial o personal en el modelo de datos y asegurarse de que las operaciones se ajusten a las directrices organizativas y legales.

Este documento cubre las consideraciones clave relacionadas con los datos confidenciales y personales en XDM.

## Determinar qué campos contienen datos confidenciales o personales

Lo que constituye SPI y PII es muy específico del contexto y, por lo tanto, depende de usted comprender el modelo de datos, las operaciones comerciales y las regulaciones aplicables para determinar qué campos de esquema representan datos confidenciales o personales.

Por ejemplo, la jurisdicción legal de sus clientes tiene un efecto directo sobre qué información se considera confidencial. El RGPD proporciona definiciones sólidas para SPI y PII, pero los clientes fuera del Espacio Económico Europeo (EEE) pueden estar sujetos a definiciones y restricciones diferentes.

## Tratamiento de datos confidenciales y personales

Al igual que las definiciones de datos confidenciales y personales, las restricciones para el tratamiento de estos datos también son específicas del contexto.

El consentimiento del cliente suele ser un factor crítico en términos de qué datos se pueden recopilar y procesar y con qué fines. En función de la jurisdicción legal bajo la que se encuentren sus clientes, es posible que se requiera un consentimiento explícito para que se recopilen sus datos personales y confidenciales. Incluso en casos en los que no se requiere un consentimiento explícito, las restricciones de manejo de datos siguen siendo aplicables según lo que indique el aviso de privacidad al cliente.

Consulte con su equipo legal para determinar cómo se deben gestionar los datos confidenciales y personales para sus casos de uso empresarial.

## Restricción del uso de datos confidenciales y personales

XDM proporciona una variedad de grupos de campos y tipos de datos estándar para describir estructuras de datos relevantes y comúnmente utilizadas para potenciar las experiencias de los clientes. Sin embargo, si un recurso estándar recomendado contiene campos restringidos que no desea incluir en los esquemas, no tiene que utilizar ese recurso.

Experience Platform le permite definir sus propios grupos de campos personalizados y tipos de datos, lo que le proporciona un control total sobre cómo se estructuran los datos si algún recurso estándar disponible no satisface sus necesidades. Consulte la siguiente documentación para obtener más información sobre cómo definir estos recursos personalizados:

* [Crear un grupo de campos personalizados](../ui/resources/field-groups.md#create)
* [Creación de un tipo de datos personalizado](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI y PII solo deben guardarse en las clases [XDM Individual Profile](../classes/individual-profile.md) y [XDM ExperienceEvent](../classes/experienceevent.md). Como práctica recomendada para la eliminación de datos y con fines de privacidad y gobernanza, no guarde SPI y PII en ninguna otra clase XDM personalizada o estándar.

## Pasos siguientes

Este documento abarcaba consideraciones clave relacionadas con los datos confidenciales y personales en XDM. Para obtener más información sobre cómo modelar los esquemas para que se ajusten mejor a los casos de uso empresariales, consulte la guía de [prácticas recomendadas para el modelado de datos](./best-practices.md).

Para obtener más información sobre las funciones de privacidad y control de datos en Experience Platform, consulte la descripción general de [gobernanza, privacidad y seguridad](../../landing/governance-privacy-security/overview.md).
