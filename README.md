Qubit Event Templates
====================================
The code in this repository will take away 95% of the development work required in implementing Qubit on your Shopify store.

#Overview

When implementing Qubit, you need to do two things from a technical perspective:

1. Add the Smartserve container to the `<head>` of every page
2. Emit emits based on user browsing behaviour

The code in this repository handles both of these for you via using Shopify templates. We also bundle the UV API, which executes in a fraction of a millisecond (1 microsecond) and sets up an API that acts as a conduit for events. Any script can emit events using the API, even before smartserve.js loads and those events can be read and subscribed to by any script using the API.

__Note__: This repository is not a Shopify App as such, it provides a series of sample logic that can be copied across to your [Shopify templates](http://docs.shopify.com/themes).


#Installation

##Smartserve Script

Update the Smartserve file at the top of `qubit-events.liquid` and `qubit-events-transaction.liquid` with your own unique id.

##Sitewide

To install, copy the `qubit-events.liquid` file from this repository to the `Snippets/` directory, found at "Themes > Template Editor > Snippets".

Then at the bottom of the `<head>` in `theme.liquid` in the `Layouts/` directory, add the following code:

```liquid
{% include 'qubit-events' %}
```


##Confirmation page

The Shopify template system does now allow codes to be added to the confirmation page (after a purchase has been made), but it does provide separate functionality to what's required.

Copy the code from `qubit-events-transaction.liquid` in this repository, and paste it into the textbox found at: "Settings > Checkout > Additional content & scripts".



#Useful notes

* There are a lot of inline JavaScript comments within the templates. If you do not want these to be publicly accessible, we recommend removing them.
* This code in this repository handles the vast majority of the implementation. However if you're looking to do something more custom, additioanl coding may be required.
* Any questions please contact [support@qubit.com](mailto:support@qubit.com), we'd be happy to help!



#Changelog

###2.0.0
Converted to Qubit event format

###0.0.3
Added Opentag container

###0.0.2
Bugfix on `product` price.

###0.0.1
Initial release
