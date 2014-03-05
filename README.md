Shopify Universal Variable Templates
====================================

Universal Variable provides a standardised JSON structure for data relating to the user journey of your visitors, such user details, products viewed and transactions. Data contained in Universal Variable are pushed automatically to Qubit’s platform and Opentag scripts.

The code in this repository will take away 95% of the development work required in implementing Universal Variable on your Shopify store.

#Overview

When implementing [Universal Variable](http://tools.qubitproducts.com/uv) and [Opentag](http://www.qubitproducts.com/tag-management), you need to do two things from a technical perspective:

1. Add the Opentag container to the `<head>` of every page
2. Add the Universal Variable (UV) directly before the Opentag container on every page.

The code in this repository handles both of these for you, using Shopify templates.

__Note__: This repository is not a Shopify App as such, it provides a series of sample logic that can be copied across to your [Shopify templates](http://docs.shopify.com/themes).


#Installation

##Opentag container

Update the Opentag container at the bottom of `uv.liquid` and `uv-transaction.liquid` with your own unique id.


##Sitewide

To install the bulk of the Universal Variable code, copy the `uv.liquid` file from this repository to the `Snippets/` directory, found at "Themes > Template Editor > Snippets".

Then at the bottom of the `<head>` in `theme.liquid` in the `Layouts/` directory, add the following code: 

```liquid
{% include 'universal-variable' %}
```


##Confirmation page

The Shopify template system does now allow codes to be added to the confirmation page (after a purchase has been made), but it does provide separate functionality to what's required.

Copy the code from `uv-transaction.liquid` in this repository, and paste it into the textbox found at: "Settings > Checkout > Additional content & scripts".



#Useful notes

* There are a lot of inline JavaScript comments within the templates. If you do not want these to be publicly accessible, we recommend removing them.
* This code in this repository handles the vast majority of the Universal Variable implementation. However if you're looking to do something more custom, additioanl coding may be required.
* Any questions please contact [support@qubitproducts.com](mailto:support@qubitproducts.com), we'd be happy to help!



#Changelog

###0.0.4
No longer using the `| json` filter in liquid templates - populating the variables directly

###0.0.3
Added Opentag container

###0.0.2
Bugfix on `product` price.

###0.0.1 
Initial release
