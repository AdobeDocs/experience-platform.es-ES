---
title: Información confidencial y personal en XDM
description: Obtenga información sobre las consideraciones clave relativas a la información personal confidencial (SPI) y la información de identificación personal (PII) en el Modelo de datos de experiencia (XDM).
source-git-commit: 76815389a1c87fbf908e499c50594a4b356a11a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Información confidencial y personal en XDM

El Modelo de datos de experiencia (XDM) proporciona estructuras de datos estándar para su uso en Adobe Experience Platform, lo que le permite recopilar datos sobre las experiencias de los clientes. Estos datos pueden incluir información personal confidencial (SPI) e información de identificación personal (PII), como la dirección de correo electrónico, el nombre, el ID de cuenta y otros campos de datos de un cliente.

Las reglas organizativas y las regulaciones legales de privacidad, como el Reglamento General de Protección de Datos (RGPD), aplican restricciones sobre cómo se pueden recopilar, almacenar, usar y compartir SPI y PII. Como tal, es importante tener en cuenta qué campos representan información personal o confidencial en el modelo de datos y asegurarse de que sus operaciones se ajustan a las directrices legales y organizativas.

Este documento cubre consideraciones clave con respecto a los datos personales y confidenciales en XDM.

## Determinación de qué campos contienen datos confidenciales o personales

Lo que constituye SPI y PII es muy específico para cada contexto y, por lo tanto, le corresponde comprender su modelo de datos, sus operaciones comerciales y las normativas aplicables para determinar qué campos de esquema representan datos confidenciales o personales.

Por ejemplo, la jurisdicción legal de sus clientes tiene un efecto directo en la información que se considera confidencial. El RGPD ofrece definiciones sólidas para las SPI y PII, pero los clientes fuera del Espacio Económico Europeo (EEE) pueden estar sujetos a distintas definiciones y restricciones.

## Gestión de datos personales y confidenciales

Al igual que las definiciones de datos confidenciales y personales, las restricciones para el manejo de estos datos también son específicas del contexto.

El consentimiento de los clientes es a menudo un factor crítico en términos de qué datos se pueden recopilar y procesar, y para qué fines. Dependiendo de la jurisdicción legal en la que se encuentren sus clientes, puede ser necesario un consentimiento explícito para que se recopilen sus datos personales y confidenciales. Incluso en casos en los que no se requiere consentimiento explícito, las restricciones de gestión de datos siguen siendo aplicables en función de lo que el aviso de privacidad indique al cliente.

Consulte a su equipo legal para determinar cómo se deben gestionar los datos personales y confidenciales para sus casos de uso empresarial.

## Restricción del uso de datos confidenciales y personales

XDM proporciona una variedad de grupos de campos estándar y tipos de datos para describir estructuras de datos relevantes y usadas comúnmente para impulsar las experiencias de los clientes. Sin embargo, si un recurso estándar recomendado contiene campos restringidos que no desea incluir en los esquemas, no tiene que utilizar ese recurso.

Platform le permite definir sus propios grupos de campos y tipos de datos personalizados, lo que le proporciona control total sobre cómo se estructuran los datos si algún recurso estándar disponible no se adapta a sus necesidades. Consulte la siguiente documentación para obtener más información sobre cómo definir estos recursos personalizados:

* [Crear un grupo de campos personalizado](../ui/resources/field-groups.md#create)
* [Crear un tipo de datos personalizado](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## Pasos siguientes

Este documento abarcaba consideraciones clave relativas a los datos personales y confidenciales en XDM. Para obtener más información sobre cómo modelar los esquemas para que se ajusten mejor a los casos de uso empresariales, consulte la guía de [prácticas recomendadas para el modelado de datos](./best-practices.md).

Para obtener más información sobre la administración de datos y las funcionalidades de privacidad en Experience Platform, consulte la descripción general de [administración, privacidad y seguridad](../../landing/governance-privacy-security/overview.md).
