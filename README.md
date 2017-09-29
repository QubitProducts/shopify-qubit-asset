Qubit Event Templates
====================================
The code in this repository will take away 95% of the development work required in implementing Qubit on your Shopify store.

# Overview

When implementing Qubit, you need to do two things from a technical perspective:

1. Add the Smartserve container to the `<head>` of every page
2. Emit events based on user browsing behaviour

The code in this repository handles both of these for you via using Shopify templates. We also bundle the UV API, which sets up an API that acts as a conduit for events. Any script can emit events using the API, even before smartserve.js loads and those events can be read and subscribed to by any script using the API.

__Note__: This repository is not a Shopify App as such, it provides a series of sample logic that can be copied across to your [Shopify templates](http://docs.shopify.com/themes).


# Installation

## Smartserve Script

Update the Smartserve file at the top of `qubit-events.liquid` and `qubit-events-transaction.liquid` with your own unique id.

## Sitewide

To install, copy the `qubit-events.liquid` file from this repository to the `Snippets/` directory, found at "Themes > Template Editor > Snippets".

Then at the bottom of the `<head>` in `theme.liquid` in the `Layouts/` directory, add the following code:

```liquid
{% include 'qubit-events' %}
```

## Product Variations

If your products have multiple variants (size, color etc) then an additional produce event needs to be emitted when the variant is changed. Due to the way Shopify themes work, it is not possible to template this as each theme can override the switcher. Insert the following event code into the function which handles the variant change:
```
  uv.emit('ecProduct', {
    eventType: 'detail',
    product: {
    productId: "{{ product.id | json}}",
      sku: "{{ product.selected_or_first_available_variant.sku | default: product.selected_or_first_available_variant.id | json }}",
      name: {{ product.title | json }},
      manufacturer: {{ product.vendor | json }},
      stock: {{ product.selected_or_first_available_variant.inventory_quantity }},
      price: {
        currency: {{ shop.currency | json }},
        value: {{ product.price | money_without_currency }}
      },
      url: window.location.protocol + "//" + window.location.hostname + "{{ product.url }}",
      description: {{ product.description | strip_html | strip_newlines | truncate: 2048 | json }},
      categories: ["{{ product.type}}"],
      images: [ window.location.protocol + "{{ product | img_url: '400x' }}" ]
    }
  })
```
Liquid variables are included and assume product is the object of the new variant.

Note: If you have been given a namespace prefix for your property, prefix it to 'ecProduct'.

## Confirmation page

The Shopify template system does not allow code to be added to the confirmation page, but it does provide separate mechanism which achieves what is required.

Copy the code from `qubit-events-transaction.liquid` in this repository, and paste it into the textbox found at: "Settings > Checkout > Additional content & scripts".

Do not forget to update the Smartserve file name at the top of `qubit-events-transaction.liquid` with your own unique id.


# Useful notes

* There are a lot of inline JavaScript comments within the templates. If you do not want these to be publicly accessible, we recommend removing them.
* This code in this repository handles the vast majority of the implementation. However if you're looking to do something more custom, additional coding may be required.
* Any questions please contact [support@qubit.com](mailto:support@qubit.com), we'd be happy to help!


# Changelog

### 2.0.0
Converted to Qubit event format

### 0.0.3
Added Opentag container

### 0.0.2
Bugfix on `product` price.

### 0.0.1
Initial release
