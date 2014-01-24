*************
FlatsWire API
*************

This FlatsWire API allow you to connect to us from your own system.

## Table of Contents

* [FlatsWire API](#flatswire-api)
    * [Table of Contents](#table-of-contents)
    * [General](#general)
    * [Connection](#connection)
    * [Support](#support)
    * [Domains](#domains)
        * [Flat](#flat)
            * [Flat Get](#flat-get)
            * [Flat Description](#flat-description)
        * [Booking](#booking)
        * [Util](#utils)


## General


## Connection

All API resources available are with this pattern:

```shell
    http://<host>/rest/<domain>/<function>/<ID?>?key=<Your Key>
```

* `host` is the host to connect to. It will be given to you once your account will be created.
* `domain` is the domain of the function you want to call.
There is actually 3 differents domains:
    * [Flat](#domain-flat) which is related on all properties management;
    * [Booking](#domain-booking) which is related on all booking management;
    * [Util](#domain-util) which is related on all function to help to know about Beethoven;
* `id` is an optional ID. It depends on the function called.
* `key is your API key. It's required to authenticate you as a user of the API.

To obtain your key, you need to have an account registred on our system. Please contact sales@flatswire.com to get more information about this.

## Support

## Domains

### Flat

#### Flat Get

This function will return you an exhaustive description of an apartment in our system.
Some details on some sub-objects you can find in the response:

* Geo

    Represents a localisation on earth with lat/lon. You will have a tag which represents the internal codification and label which is the translated tag in human language.
    The zoom indicates the best zoom to use in google map and category which is the category of the geo object. 
    Fields district, city, country, geo are in this type. 

* Properties

    Are the amenities of the apartment.
    The field `property_type_id` is the kind of amenity:
    * 3 means text value, like area which is the area of the apartment
    * 2 means boolean value, like flat_lift which tells whether the apartment has a lift or not
    The key field is the internal codification of the amenities. It's a language free representation. But all written in english so most of them are self-explained.


Example: 

```shell
    http://bs.flatswire.com/rest/flat/get/595?key=53ccd11e-df4d-4cef-98ec-84b474cb5121
```

Result:

```javascript
{
    flat_id: "595",
    min_stay: "3",
    max_stay: "95",
    nb_person: "6",
    nb_sleep: "3",
    nb_dbed: "2",
    nb_sbed: "0",
    nb_sofabed: "1",
    nb_bedroom: "2",
    nb_bathroom: "1",
    nb_toilette: "1",
    floor: "7",
    photo_count: "60",
    customer_deal: "1",
    nb_room: "4",
    reference: "A-VIEW99",
    creation_date: "2011-03-18 11:24:13",
    modification_date: "2012-12-11 09:39:44",
    deletion_date: null,
    deleted: "0",
    enabled: "1",
    shared: "1",
    district: {
        geo_id: "20",
        latitude: "48.867326",
        longitude: "2.364378",
        zoom: "12",
        tag: "republique",
        category: "district",
        parent_geo_id: "904",
        label: null
    },
    city: {
        geo_id: "904",
        latitude: "48.856614",
        longitude: "2.3522219",
        zoom: "14",
        tag: "fr.paris",
        category: "city",
        parent_geo_id: "903",
        label: "Paris"
    },
    country: {
        geo_id: "903",
        latitude: "46.227638",
        longitude: "2.213749",
        zoom: "12",
        tag: "fr",
        category: "country",
        parent_geo_id: "904",
        label: null
    },
    manager: {
        account_id: "41",
        reference: "PA-Location",
        creation_date: "2010-04-29 14:00:39",
        modification_date: "2013-05-14 08:14:24",
        description: null
    },
    address: {
        address_id: "577",
        unit: "",
        number: "99",
        street1: "Avenue de la RÃ©publique",
        street2: "",
        street3: "",
        zip_code: "75011",
        state: null,
        city: "Paris",
        country_id: "74",
        latitude: "48.8636296",
        longitude: "2.383233399",
        creation_date: null,
        modification_date: null,
        tag: null,
        formatted_address: null
    },
    currency: {
        currency_id: "45",
        code: "EUR",
        name: "Euro",
        symbol: "&euro;",
        unicode_symbol: "&#12"
    },
    geo: {
        geo_id: "720",
        latitude: "48.8636296",
        longitude: "2.383233399",
        zoom: "0",
        tag: "fr.par.a-view99",
        category: null,
        parent_geo_id: "904",
        label: null
    },
    properties: [
        {
        property_id: "1",
        value: "93",
        property_type_id: "3",
        key: "flat_area",
        category: "flat"
        },
        ...
        {
            property_id: "154",
            value: "0",
            property_type_id: "2",
            key: "flat_au_nz_free_call",
            category: "flat"
        }
    ]
}
```

#### Flat Description

### Booking

### Util



