# Morphism PHP

[![Build Status][travis-image]][travis-url]
> Helps you to transform any object structure to another.

This library refers to Yann Renaudin's [Morphism library](https://github.com/emyann/morphism)

## Contribution 

- Twitter: [@renaudin_yann][twitter-account]
- Pull requests and stars are always welcome 🙏🏽 For bugs and feature requests, [please create an issue](https://github.com/Gmulti/morphism-php/issues)


## Getting started 🚀 

Install `morphism-php` using composer (soon).

```php
use Morphism\Morphism;
```

## What does it do? 🤔

Morphism uses a semantic configuration to go through the collection of graph objects you have to process. Then it extracts and computes the value from the specified path(s). Finally, it sets this value to the destination property from the schema.

## Usage 🍔
Morphism is curried function that allows a partial application with a semantic configuration. You can use it in many ways:

### Example
```php
// Target type you want to have
class User {
    public function __construct($firstName, $lastName, $phoneNumber){
        $this->firstName   = $firstName;
        $this->lastName    = $lastName;
        $this->phoneNumber = $phoneNumber;
        $this->city = null;
   }
}

// Data source you want to map
$data = array(
    "name"      => "Iron Man",
    "firstName" => "Tony",
    "lastName"  => "Stark",
    "address" => array(
        "city"    => "New York City",
        "country" => "USA"
    ),
    "phoneNumber" => array(
        array(
            "type"   => "home",
            "number" => "212 555-1234"
        ),
        array(
            "type"   => "mobile",
            "number" => "646 555-4567"
        )
    )
);

// Mapping Schema ( see more examples below )
$schema = array(
    "city" => "address.city",
    "name" => function($data){
        return strtoupper($data["name"]);
    }
);

Morphism::setMapper("User", $schema);

// Map using the registered type and the registry
$result = Morphism::map("User", $data);

/// *** OUTPUT *** ///

class User {
    public $city // string(13) "New York City"
    public $name  // string(8) "iron man"
}
```

## License

MIT © [Thomas Deneulin][twitter-account]

[twitter-account]: https://twitter.com/TDeneulin
[travis-image]: https://travis-ci.org/Gmulti/morphism-php.svg?branch=master
[travis-url]: https://travis-ci.org/Gmulti/morphism-php
