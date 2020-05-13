---
title: Destino de Amazon Kinesis
seo-title: Destino de Amazon Kinesis
description: Cree una conexión saliente en tiempo real con el almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
seo-description: Cree una conexión saliente en tiempo real con el almacenamiento de Amazon Kinesis para transmitir datos desde Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---


# Destino de Amazon Kinesis

## Información general {#overview}

El [!DNL Kinesis Data Streams] servicio de Amazon Web Services le permite recopilar y procesar grandes flujos de registros de datos en tiempo real.

Puede crear una conexión saliente en tiempo real con su [!DNL Amazon Kinesis] almacenamiento para transmitir datos desde Adobe Experience Platform.

* Para obtener más información sobre [!DNL Amazon Kinesis], consulte la documentación [de](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)Amazon.
* Para conectarse a [!DNL Amazon Kinesis] través de llamadas de API, consulte el tutorial [de API de destinos de]flujo continuo.
* Para conectarse a [!DNL Amazon Kinesis] mediante la interfaz de usuario de CDP en tiempo real de Adobe, consulte las secciones siguientes.

![Amazon Kinesis en la interfaz de usuario](/help/rtcdp/destinations/assets/aws-kinesis-destination.png)


## Casos de uso {#use-cases}

Al utilizar destinos de flujo continuo como Amazon Kinesis, puede suministrar fácilmente eventos de segmentación de alto valor y atributos de perfil asociados a sus sistemas de elección.

Por ejemplo, un cliente potencial descargó un documento técnico que los califica en un segmento de &quot;alta propensión a convertir&quot;. Al asignar el segmento en el que se encuentra el cliente potencial al destino de Amazon Kinesis, recibirá este evento en Amazon Kinesis. Allí puede emplear un enfoque de &quot;hágalo usted mismo&quot; y describir la lógica empresarial sobre el evento, como piensa que funcionaría mejor con sus sistemas de TI empresariales.

## Destino de Connect {#connect-destination}

Consulte Flujo de trabajo de destinos de almacenamiento de [Cloud ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)para obtener instrucciones sobre cómo conectarse a los destinos de almacenamiento de nube, incluidos los admitidos por [!DNL Amazon].

Para [!DNL Amazon Kinesis] destinos, introduzca la siguiente información en el flujo de trabajo de creación de destinos:

### En el paso Cuenta {#account-step}

* **Clave de acceso y clave** secreta de Amazon Web Services: En [!DNL Amazon Web Services], genere una clave de acceso: par de claves de acceso secreto para otorgar acceso CDP en tiempo real de Adobe a su [!DNL Amazon Kinesis] cuenta. Obtenga más información en la documentación [de](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)Amazon Web Services.
* **región**: Indicar a qué [!DNL Amazon Web Services] región se transmitirán los datos.

![Campos de entrada en el paso de cuenta](/help/rtcdp/destinations/assets/aws-kinesis-account-step.png)

### En el paso Autenticación {#authentication-step}

* **Nombre**: Proporcione un nombre para la conexión a [!DNL Amazon Kinesis]
* **Descripción**: Proporcione una descripción de la conexión a [!DNL Amazon Kinesis].
* **stream**: Proporcione el nombre del flujo de datos existente en la [!DNL Amazon Kinesis] cuenta. CDP en tiempo real de Adobe exportará datos a este flujo.

![Campos de entrada en el paso de autenticación](/help/rtcdp/destinations/assets/aws-kinesis-authentication-step.png)

<!--

>[!IMPORTANT]
>
>Adobe Real-time CDP needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Activar segmentos {#activate-segments}

Consulte [Activar perfiles y segmentos en un destino](/help/rtcdp/destinations/activate-destinations.md) para obtener información sobre el flujo de trabajo de activación de segmentos.

## Datos exportados {#exported-data}

Los datos exportados de la plataforma de experiencias llegan [!DNL Amazon Kinesis] en formato JSON. Por ejemplo, un evento que contenga la identidad de correo electrónico con hash de una audiencia que haya salido de un determinado segmento podría tener este aspecto:

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* Vínculo al tutorial de la API de Amazon Kinesis
>* [Destino de los centros de Evento de Azure](/help/rtcdp/destinations/azure-event-hubs-destination.md)
>* [Tipos y categorías de destino](/help/rtcdp/destinations/destination-types.md)

