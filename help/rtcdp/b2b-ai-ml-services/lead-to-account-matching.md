---
title: Concordancia de posibles clientes con cuentas en tiempo real CDP B2B
type: Documentation
description: Información general y más información sobre la función de coincidencia de cuentas del posible cliente en CDP B2B del Experience Platform.
source-git-commit: 827bd1b930478c3c0b553a9485f98545771a9062
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Concordancia de posibles clientes con cuentas en tiempo real CDP B2B

## Información general {#overview}

El marketing basado en cuentas es una estrategia cada vez más importante para el marketing B2B. El marketing basado en cuentas ofrece las siguientes ventajas clave para adquirir clientes específicos de alto valor:

- Borrar ROI
- Alineación de ventas y marketing
- Un enfoque personalizado
- Menos recursos desperdiciados
- Un ciclo de ventas más corto

El marketing basado en cuentas permite vincular a cuentas de ventas a personas conocidas y visitantes web anónimos. Esto permite que los equipos de marketing interactúen con posibles clientes de las cuentas de destino al principio del recorrido del cliente para aumentar sus posibilidades de conversión. Un registro de persona conocido suele incluir parte o la totalidad de la siguiente información:

- Nombre de la persona
- Correo electrónico Dirección
- Número de contacto
- El nombre de su empresa
- Sitio web de la empresa
- Puesto de trabajo
- Ubicación

La coincidencia de posibles clientes con cuentas le permite unir perfiles de personas conocidas con perfiles de cuenta. A continuación, puede segmentar y segmentar los datos en un contexto B2B, como cuentas, oportunidades, etc. Los perfiles de persona se pueden clasificar en las tres categorías siguientes:

- **Perfil de la persona de la cuenta:** El perfil de persona ya está asociado a al menos un perfil de cuenta a través de la relación de un origen de datos. Esto implica que hay al menos un fragmento de contacto.

>[!NOTE]
>
> Los perfiles de las personas de la cuenta no coinciden al ejecutar trabajos coincidentes de cuentas.

- **Perfil de persona conocida:** El perfil de persona NO está asociado a ningún perfil de cuenta y al menos uno de los siguientes atributos de perfil de persona tiene un valor:

   - Correo electrónico Dirección
   - El nombre de su empresa
   - Sitio web de la empresa

- **Perfil de persona anónima:** El perfil de persona NO está asociado a ningún perfil de cuenta y ninguno de los siguientes atributos de perfil de persona tiene un valor:

   - Correo electrónico Dirección
   - El nombre de su empresa
   - Sitio web de la empresa

>[!NOTE]
>
> Un perfil de persona puede estar relacionado con varios perfiles de cuenta. Sin embargo, el proceso de coincidencia de cuentas de posibles clientes solo coincidirá con la mejor coincidencia. Si se requiere un conjunto más amplio de coincidencias, combine el posible cliente con la función de cuentas relacionadas.

## Funcionamiento {#how-it-works}

Los trabajos de ejecución diaria utilizan factores determinísticos y probabilísticos para hacer coincidir perfiles de posibles clientes conocidos sin asociaciones de cuentas existentes. Los perfiles de posible cliente conocidos tendrán uno de los siguientes atributos disponibles:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> El atributo b2b.personKey.sourceKey debe existir.

Los atributos b2b.companyName, b2b.companyWebsite y b2b.personKey.sourceKey se pueden ubicar en el grupo de campos b2b del esquema de personas B2B.

![Esquema de persona B2B que muestra atributos](/help/rtcdp/accounts/images/b2b-person-schema.png)

El atributo workEmail se puede encontrar como un grupo de campos de nivel superior en el esquema de persona B2B.

![Esquema de persona B2B que muestra workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

La mejor coincidencia para los perfiles es si la puntuación de coincidencia supera un umbral de confianza interna. Los resultados se guardan en un nuevo conjunto de datos del sistema de la relación de persona de cuenta existente XDM.

El servicio de coincidencia de cuentas de posibles clientes se ejecuta cuando hay disponible una nueva instantánea de perfil de persona que es una vez cada 24 horas. Consulte la documentación para obtener más información sobre la variable [configuración de la coincidencia de posibles clientes con cuentas](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Ver el resultado de coincidencia de cuentas de posibles clientes {#how-to-view}

Después de ejecutar el trabajo, los resultados se guardan en un nuevo conjunto de datos de la relación de persona de cuenta existente XDM.

Para obtener una vista previa del conjunto de datos, seleccione **[!UICONTROL Vista previa del conjunto de datos]** en la parte superior derecha.

![Nuevo conjunto de datos](/help/rtcdp/accounts/images/b2b-dataset-output.png)

El conjunto de datos incluye la información de cuenta coincidente, así como la puntuación de coincidencia para el conjunto de datos seleccionado. La variable **[!UICONTROL Fuente de relación]** El campo indica si procede del proceso de coincidencia de posibles clientes con cuentas.

![Obtener una vista previa de las puntuaciones de confianza del conjunto de datos y los resultados](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## La supervisión lleva a que los trabajos coincidan con la cuenta {#monitoring-jobs}

Puede controlar el estado del trabajo y las métricas asociadas de cualquier posible cliente para los trabajos coincidentes de la cuenta a través del panel.

Consulte la documentación para obtener más información sobre la variable [monitorización de trabajos para coincidencia de cuentas de posibles clientes](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
