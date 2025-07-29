![Icon](./src/icon.svg)

# Schema plugin for Craft CMS 5.x

A fluent builder of Schema.org types and ld+json generator based on Spatie's schema-org package which makes for a fast and easy way to add structured data to your Twig templates.

## Requirements

This plugin requires Craft CMS 5.0.0 or later and PHP 8.2+

## Installation

To install the plugin follow these instructions.

1. Open your terminal and go to your Craft project:

        cd /path/to/project

2. Then tell Composer to load and install the plugin:

        composer require jamesmacwhite/craft-schema && php craft plugin/install schema

   If using DDEV for your local development environment, run the following command to do the same:

        ddev composer require "jamesmacwhite/craft-schema:^2.0" -w && ddev craft plugin/install schema

## Schema Overview

Schema provides a fluent builder for all Schema.org types and their properties. For more information and the available methods, check out [spatie/schema-org](https://github.com/spatie/schema-org).  

## Using Schema

Once Schema is installed, it's accessible through the `craft` variable in your templates. 

For the best experience, set the schema to a variable and typehint it to Spatie's model. In combination with the [Symfony plugin](https://plugins.jetbrains.com/plugin/7219-symfony-plugin) for PHPStorm, you get autocompletion for all the Schema's and their properties.

For example:
```twig
{# @var schema \Spatie\SchemaOrg\Schema #}
{% set schema = craft.schema %}
{{ schema
    .person
      .name("James White")
      .email("contact@jmwhite.co.uk")
      .company(
        schema.localBusiness
          .name("My organisation")
          .address(schema.postalAddress
            .addressCountry("United Kingdom")
            .addressLocality("Nottingham")
            .addressRegion("Nottinghamshire")
            .postalCode(NG1 1AA)
            .streetAddress("Example street")
          )
      ) | raw
}}
```

Generates the following output:

```html
<script type="application/ld+json">
{  
   "@context":"http:\/\/schema.org",
   "@type": "Person",
   "name": "James White",
   "email": "contact@jmwhite.co.uk",
   "company":{  
      "@type": "LocalBusiness",
      "name": "My organisation",
      "address":{  
         "@type": "PostalAddress",
         "addressCountry": "United Kingdom",
         "addressLocality": "Nottingham",
         "addressRegion": "Nottinghamshire",
         "postalCode": "NG1 1AA,
         "streetAddress": "Example Street"
      }
   }
}
</script>
```

## Licence

This plugin is licensed under a MIT license, which means that it's completely free open source software, and you can use it for whatever and however you wish.

## Credits

Brought to you by [Rias](https://rias.be) and [James White](https://www.jmwhite.co.uk)
