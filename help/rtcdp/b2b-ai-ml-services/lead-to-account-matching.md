---
title: Coincidencia de clientes potenciales con cuentas en Real-Time CDP B2B
type: Documentation
description: Información general y más detalles sobre la función de coincidencia de clientes potenciales con cuentas de Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 3%

---

# Coincidencia de clientes potenciales con cuentas en Real-Time CDP B2B

## Información general {#overview}

El marketing basado en cuentas es una estrategia cada vez más importante para el marketing B2B. El marketing basado en cuentas ofrece las siguientes ventajas clave para adquirir clientes de alto valor específicos:

- Borrar ROI
- Alineación de ventas y marketing
- Un enfoque personalizado
- Menos recursos desperdiciados
- Un ciclo de ventas más corto

El marketing basado en cuentas permite vincular personas conocidas y visitantes web anónimos a cuentas de ventas. Esto permite a los equipos de marketing interactuar con posibles clientes potenciales de las cuentas de Target al principio del recorrido del cliente para aumentar sus posibilidades de conversión. Un registro de persona conocida suele incluir parte o la totalidad de la siguiente información:

- Nombre de la persona
- Dirección de correo electrónico
- Número de contacto
- Nombre de la compañía
- Sitio web de empresa
- Cargo
- Ubicación

La coincidencia de cliente potencial con cuenta permite unir perfiles de personas conocidas a perfiles de cuenta. A continuación, puede segmentar y segmentar los datos en un contexto B2B como cuentas, oportunidades, etc. Los perfiles de las personas se pueden clasificar en las tres categorías siguientes:

- **Perfil de persona de la cuenta:** El perfil de persona ya está asociado al menos a un perfil de cuenta a través de la relación de una fuente de datos. Esto implica que hay al menos un fragmento de contacto.

>[!NOTE]
>
> Los perfiles de persona de cuenta no coinciden al ejecutar los trabajos de coincidencia de clientes potenciales con cuentas.

- **Perfil de persona conocido:** El perfil de persona NO está asociado a ningún perfil de cuenta y al menos uno de los siguientes atributos de perfil de persona tiene un valor:

   - Dirección de correo electrónico
   - Nombre de la compañía
   - Sitio web de empresa

- **Perfil de persona anónima:** El perfil de persona NO está asociado a ningún perfil de cuenta y ninguno de los siguientes atributos de perfil de persona tiene un valor:

   - Dirección de correo electrónico
   - Nombre de la compañía
   - Sitio web de empresa

>[!NOTE]
>
> Un perfil de persona puede estar relacionado con varios perfiles de cuenta. Sin embargo, el proceso de coincidencia de cliente potencial con cuenta solo coincidirá con la mejor coincidencia. Si se requiere un conjunto más amplio de coincidencias, asocie el posible cliente a la coincidencia de cuenta con la función de cuentas relacionada.

## Funcionamiento {#how-it-works}

Los trabajos de ejecución diaria utilizan factores determinísticos y probabilísticos para hacer coincidir perfiles de posibles clientes conocidos sin asociaciones de cuenta existentes. Los perfiles de posibles clientes conocidos tendrán uno de los siguientes atributos disponibles:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> El atributo b2b.personKey.sourceKey debe existir.

Los atributos b2b.companyName, b2b.companyWebsite y b2b.personKey.sourceKey se pueden encontrar en el grupo de campos b2b del esquema person B2B.

![Esquema de persona B2B que muestra atributos](/help/rtcdp/accounts/images/b2b-person-schema.png)

El atributo workEmail se puede encontrar como un grupo de campos de nivel superior en el esquema person B2B.

![Esquema de persona B2B que muestra el correo electrónico de trabajo](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Los perfiles obtendrán mejores coincidencias solo si la puntuación de la coincidencia supera un umbral de confianza interna. Los resultados se guardan en un nuevo conjunto de datos del sistema de la relación de persona de la cuenta existente XDM.

El servicio de coincidencia de cliente potencial con cuenta se ejecuta cuando está disponible una nueva instantánea de perfil de persona que se registra una vez cada 24 horas. Consulte la documentación para obtener más información sobre la [configuración del posible cliente para la coincidencia de cuentas](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Cómo ver el resultado de coincidencia de cliente potencial con cuenta {#how-to-view}

Después de la ejecución del trabajo, los resultados se guardan en un nuevo conjunto de datos del XDM de relación de persona de cuenta existente.

Para obtener una vista previa del conjunto de datos, seleccione **[!UICONTROL Vista previa del conjunto de datos]** en la parte superior derecha.

![Nuevo conjunto de datos](/help/rtcdp/accounts/images/b2b-dataset-output.png)

El conjunto de datos incluye la información de la cuenta coincidente, así como la puntuación de coincidencia del conjunto de datos elegido. El campo **[!UICONTROL Source de relación]** indica si procede del proceso de coincidencia de cliente potencial con cuenta.

![Previsualizar resultados y puntuaciones de confianza del conjunto de datos](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## La monitorización lleva a trabajos de coincidencia de cuentas {#monitoring-jobs}

A través del panel de control, puede monitorizar el estado del trabajo y las métricas asociadas de cualquier posible cliente que coincida con los trabajos de la cuenta.

Consulte la documentación para obtener más información sobre los [trabajos de supervisión para la coincidencia de clientes potenciales con cuentas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
