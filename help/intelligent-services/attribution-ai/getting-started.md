---
keywords: Experience Platform;getting started;attribution ai;popular topics
solution: Experience Platform
title: Introducción a la API de atribución
topic: Getting started
translation-type: tm+mt
source-git-commit: 14d47f99f1edd7734245b25b7c39f3a71e7aac50

---


# Introducción a la API de atribución

Las siguientes guías requieren conocer los distintos servicios de Adobe Experience Platform relacionados con el uso de la API de atribución. Antes de comenzar los tutoriales, revise los siguientes documentos:

- [Descripción general](../../xdm/home.md)del sistema del modelo de datos de experiencia (XDM): XDM es el marco de base que permite a Adobe Experience Cloud, con la tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto y en el momento preciso. La metodología en la que se basa la plataforma de experiencia, el sistema XDM, hace operativos los esquemas del modelo de datos de experiencia para que los utilicen los servicios de plataforma.
- [Conceptos básicos de la composición](../../xdm/schema/composition.md)de esquemas: Este documento proporciona una introducción a los esquemas del Modelo de datos de experiencia (XDM) y a los componentes, principios y prácticas recomendadas para la composición de esquemas que se utilizarán en la plataforma de Adobe Experience.
- [esquemas](../../xdm/tutorials/create-schema-ui.md)de creación: En este tutorial se explican los pasos para crear un esquema con el Editor de Esquemas en la plataforma de experiencia.

La API de atribución requiere que los conjuntos de datos se ajusten al esquema de Eventos de experiencias del consumidor (CEE), que es una mezcla en el Modelo [de datos de](../../xdm/home.md) experiencia (XDM). Póngase en contacto con el servicio de asistencia de Adobe en attributionai-support@adobe.com para implementar o realizar cambios en estos datos. Si los datos de inversión de medios están presentes, puede realizar más análisis, como por ejemplo ingresos incrementales y retorno de la inversión. Si los datos de perfil del cliente están disponibles, puede atribuir créditos adicionales al nivel de perfil del cliente.

## Terminología

- **evento de conversión:** Cualquier evento digital o interacción digital que los clientes realicen para indicar un hito hacia un objetivo, como los registros de conferencias. Algunos ejemplos adicionales son: conversiones de pago, suscripciones a cuentas gratuitas o requisitos para una característica.

- **Touchpoint:** Cualquier evento digital o interacción digital que los clientes realicen en el camino hacia un objetivo. Algunos ejemplos son los esfuerzos de mercadotecnia antes de la compra, las impresiones de publicidad de visualización vistas y los clics de búsqueda paga.

## Acceso a las puntuaciones y consultas

>[!NOTE] Si no necesita consulta o acceder a puntuaciones sin procesar, puede omitir este paso y continuar con la guía [de la interfaz de](./user-guide.md)usuario.

El acceso y consulta de puntuaciones para la Atribución de IA se realiza a través de Snowflake. En este momento, debe enviar por correo electrónico a la asistencia de Adobe a attributionai-support@adobe.com para configurar y recibir las credenciales en la cuenta de lectura de Snowflake o para exportar datos sin procesar de forma masiva.

Una vez que la asistencia de Adobe haya procesado su solicitud, se le proporcionará una dirección URL para la cuenta de lector en Snowflake y las credenciales correspondientes a continuación:

- URL del copo de nieve
- Nombre de usuario
- Contraseña

## Pasos siguientes

Una vez que esté listo y tenga todas sus credenciales y esquemas en su lugar, inicio siguiendo la guía de la interfaz de usuario de [Atribución de archivos AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia y enviarla para capacitación y puntuación.