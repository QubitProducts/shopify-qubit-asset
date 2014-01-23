shopify-universal-variable-asset
================================

#Overview

When implementing [Universal Variable](http://tools.qubitproducts.com/uv) and [Opentag](http://www.qubitproducts.com/tag-management), you need to do two things from a technical perspective:

1. Add the Opentag container to the `<head>` of every page
2. Add the Universal Variable (UV) directly before the Opentag container on every page.

The code in this repository handles both of these for you, using Shopify templates.

__Note__: This repository is not a Shopify App as such, it provides a series of sample logic that can be copied across to your Shopify templates.


#Installation

##Sitewide

To install the bulk of the Universal Variable code, copy the `uv.liquid` file from this repository to the `snippets` directory, found at "Themes > Template Editor > Snippets".

Then at the bottom of the `<head>` in `theme.liquid` in the `Layouts` directory, add the following code: 

```liquid
{% include 'universal-variable' %}
```


##Confirmation page

The Shopify template system does now allow codes to be added to the confirmation page (after a purchase has been made), but it does provide separate functionality to what's required.

Copy the code from `uv-transaction.liquid` in this repository, and paste it into the textbox found at: "Settings > Checkout > Additional content & scripts".
