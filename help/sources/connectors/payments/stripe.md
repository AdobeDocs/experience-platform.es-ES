---
title: Stripe
description: Aprenda a introducir datos de pagos de su cuenta de Stripe en Adobe Experience Platform
badge: Beta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>El origen [!DNL Stripe] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Miles de empresas de todos los tamaños utilizan [!DNL Stripe] tanto en línea como en persona para aceptar pagos, generar nuevas fuentes de ingresos y expandirse globalmente con la ayuda de Adobe Experience Platform, Adobe Commerce y [!DNL Magento Open Source].

Utilice el origen [!DNL Stripe] en el Experience Platform para introducir los datos capturados por sus clientes durante el flujo de compra. Una vez introducidos, utilice estos datos para crear ofertas personalizadas y desbloquear perspectivas comerciales más enriquecidas.

>[!TIP]
>
>Si tiene alguna pregunta acerca del origen de [!DNL Stripe] en el Experience Platform, póngase en contacto con [!DNL Stripe] en adobe-partner<span>@stripe.com.

>[!BEGINSHADEBOX]

**Caso de uso de ejemplo para el origen [!DNL Stripe]**

Su empresa permite que sus clientes compren artículos en su tienda en línea con la opción de **comprar ahora** y **pagar más tarde** (con [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] o [!DNL Zip]).

Use la fuente de datos [!DNL Stripe] para analizar el uso de las opciones **comprar ahora** y **pagar más tarde**, y experimentar con ofertas personalizadas para estos clientes. Por ejemplo, considere la posibilidad de recomendar elementos adicionales para ampliar el número de elementos en su carro de compras antes del cierre de compra.

>[!ENDSHADEBOX]

Lea el siguiente documento para obtener información sobre cómo configurar su cuenta de origen de [!DNL Stripe], recuperar las credenciales necesarias y crear los esquemas.

## Requisitos previos {#prerequisites}

Las secciones siguientes proporcionan información sobre la configuración de requisitos previos que debe completar antes de conectar su cuenta de [!DNL Stripe] al Experience Platform.

### Recuperación del token de acceso

* Inicie sesión en [[!DNL Stripe] panel](https://dashboard.stripe.com/login) con su dirección de correo electrónico y contraseña de [!DNL Stripe].
* En el panel [!DNL Developers], seleccione **[!DNL API keys for developers]**.
* En la ficha **claves API**, seleccione **[!DNL Reveal test key]** para mostrar el token de acceso.
* Ahora puede usar este token como token de acceso al conectar su cuenta de [!DNL Stripe] al Experience Platform mediante la API de [!DNL Flow Service] o la interfaz de usuario del Experience Platform.

### Recopilar credenciales necesarias

Para conectar su cuenta de [!DNL Stripe] al Experience Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

>[!BEGINTABS]

>[!TAB API]

Debe proporcionar las siguientes credenciales al conectar su cuenta de [!DNL Stripe] mediante la API de [!DNL Flow Service].

| Credencial | Descripción |
| --- | --- |
| `accessToken` | Su token de autenticación de código de actualización de OAuth 2 de [!DNL Stripe]. |
| `connectionSpec.id` | Id. de especificación de conexión del origen [!DNL Stripe]. Este identificador se corrigió como: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB IU]

Debe proporcionar las siguientes credenciales al conectar su cuenta de [!DNL Stripe] mediante la interfaz de usuario de Experience Platform.

| Credencial | Descripción |
| --- | --- |
| Token de acceso | Su token de autenticación de código de actualización de OAuth 2 de [!DNL Stripe]. |

>[!ENDTABS]

Para obtener más información sobre el uso de las API [!DNL Stripe], lea la [[!DNL Stripe] documentación sobre las claves API](https://docs.stripe.com/keys).

### Creación de un esquema de modelo de datos de experiencia (XDM)

El origen [!DNL Stripe] admite la ingesta de datos desde las siguientes rutas de recursos:

* Cargos
* Suscripciones
* Reembolsos
* Transacciones de Saldo
* Clientes
* Precios

Debe crear un esquema XDM para describir un conjunto de datos, que puede almacenar los campos y tipos de datos que se enviarán de [!DNL Stripe] al Experience Platform.

>[!BEGINTABS]

>[!TAB Cargos]

En [!DNL Stripe], **cargos** representan intentos de mover dinero a tu [!DNL Stripe]. Lea la [[!DNL Stripe] guía de API sobre cargos](https://docs.stripe.com/api/charges) para obtener más información sobre atributos de cargos específicos.

+++Seleccione para ver el objeto Gastos de Stripe

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Suscripciones]

En [!DNL Stripe], puede usar **suscripciones** para cargar a un cliente de forma recurrente. Lea la [[!DNL Stripe] guía de API sobre suscripciones](https://docs.stripe.com/api/subscriptions) para obtener más información sobre atributos de suscripción específicos.

+++Seleccione para ver el objeto Suscripción de Stripe

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Reembolsos]

En [!DNL Stripe], puedes usar **reembolsos** para reembolsar un cargo creado anteriormente. Lee la [[!DNL Stripe] guía de API sobre reembolsos](https://docs.stripe.com/api/refunds) para obtener más información sobre atributos de reembolso específicos.

+++Seleccione esta opción para ver el objeto de reembolso del Stripe

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Transacciones de saldo]

En [!DNL Stripe], **transacciones de saldo** representan el movimiento de fondos entre sus cuentas de [!DNL Stripe]. Lea la [[!DNL Stripe] guía de API sobre transacciones de saldo](https://docs.stripe.com/api/balance_transactions) para obtener más información sobre atributos específicos de transacciones de saldo.

+++Seleccione esta opción para ver el objeto Transacción de saldo de Stripe

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Clientes]

En [!DNL Stripe], **clientes** representan a un cliente determinado de su negocio. Para obtener información sobre atributos específicos del cliente, lea la [[!DNL Stripe] Guía de API sobre clientes](https://docs.stripe.com/api/customers) para obtener más información sobre atributos específicos del cliente.

+++Seleccione esta opción para ver el objeto Cliente del Stripe

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Precios]

En [!DNL Stripe], **precios** representan el costo unitario, la moneda y el ciclo de facturación opcional para la compra recurrente y única de productos. Lea la [[!DNL Stripe] guía de API sobre precios](https://docs.stripe.com/api/prices) para obtener más información sobre atributos de precios específicos.

+++Seleccione para ver el objeto Precio de Stripe

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en el Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Stripe] al Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

## Pasos siguientes

Una vez que haya completado la configuración de requisitos previos, puede continuar con la conexión e ingerir los datos de [!DNL Stripe] en el Experience Platform. Lea las siguientes guías para aprender a ingerir datos de pagos de [!DNL Stripe] en el Experience Platform mediante API o la interfaz de usuario:

* [Ingresa datos de pagos de tu cuenta de Stripe en Experience Platform mediante la API de Flow Service](../../tutorials/api/create/payments/stripe.md).
* [Ingesta de datos de pagos de tu cuenta de Stripe al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/payments/stripe.md).
