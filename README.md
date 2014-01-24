# FlatsWire API

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
            * [Flat Photos](#flat-photos)
            * [Flat Availability](#flat-availability)
            * [Flat References](#flat-references)
            * [Flat Prices](#flat-prices)
        * [Booking](#booking)
        * [Util](#utils)


## General


## Connection

All API resources available are with this pattern:

```shell
    http://<host>/rest/<domain>/<function>/<ID?>?key=<your_key>
```

* `host` is the host to connect to. It will be given to you once your account will be created.
* `domain` is the domain of the function you want to call.
There is actually 3 differents domains:
    * [Flat](#domain-flat) which is related on all properties management;
    * [Booking](#domain-booking) which is related on all booking management;
    * [Util](#domain-util) which is related on all function to help to know about Beethoven;
* `id` is an optional ID. It depends on the function called.
*  `your_key` is your API key. It's required to authenticate you as a user of the API.

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
    Fields `district`, `city`, `country`, `geo` are in this type. 

* Properties

    Are the amenities of the apartment.
    The field `property_type_id` is the kind of amenity:
    * 3 means text value, like area which is the area of the apartment
    * 2 means boolean value, like flat_lift which tells whether the apartment has a lift or not
    The key field is the internal codification of the amenities. It's a language free representation. But all written in english so most of them are self-explained.


Example: 

```shell
    http://<host>/rest/flat/get/595?key=<your_key>
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

This function will return you the English text description of an apartment. 

Example:

```shell
    http://<host>/rest/flat/description/595?key=<your_key>
```

Result:

```javascript
"<h5>Location<\/h5>\n<p>This short term Paris apartment rental is located in the 11th district, two steps away from the famous P&egrave;re Lachaise cemetery where Edith Piaf, Jim Morrison, Alexandre Dumas and many more are buried. You will love this lively area, already beloved by its residents, where you will find many shops, supermarkets, restaurants, caf&eacute;s and venues, particularly in the nearby Oberkampf Street. The Pere Lachaise open air market takes place twice a week (on Tuesdays and Fridays). This is a very nice market with fresh products : fruits, vegetables, cheese etc.The closest metro stations are St Maur (line 3) and P&egrave;re Lachaise (line 2 and 3). Line 3 is very convenient : Republique is 2 stops away, Arts et M&eacute;tiers is 4 stops away and Opera is 8 stops away. Count 2 minutes per stop : hence you will be close to many different parts of the city.<\/p>\n<h5>Standing<\/h5>\n<p>This Paris apartment is located on the 7th floor (top floor) of a very good standard building equipped with a lift. Access is secured by a door code and a very careful building keeper. The lift will lead you to the 6th floor and you will have to climb the stairs to reach your Paris apartment on the 7th floor. The 11 windows are double glazed and offer an extraordinary view on Paris.<\/p>\n<h5>Layout<\/h5>\n<p>This 93sqm apartment in Paris is a pure jewel. It used to be seven maids' room which have been transformed into a large apartment. It is organized around a small courtyard in the middle of the apartment (there is no particular view on this courtyard but it adds three more windows with more light coming through). The aparment is bright all day long and it is a real pleasure to live here.<\/p>\n<p>The entrance hall of this apartment in Paris is spacious with storage space and opens on the left hand side onto the dining area (with a dining table where six guests can sit) and on the right hand side onto the first bedroom, also quiet and spacious. A lovely room divider from a famous designer gives more intimacy to the people sleeping in this bedroom, even if the bed is on the opposite side of the bedroom. The bedroom features a double bed (140x200) and a very large wardrobe (with room for around 25 hangers, plus drawers and shelves). The apartment also has a lovely north-facing balcony, from where you will have the pleasure to watch the beautiful light of the sunset reflecting on the building in front of you.<\/p>\n<p>This first bedroom leads into the kitchen. It is a modern well equipped kitchen with a small dining table. It has a sky light, which adds even more to the light already filling the apartment.<\/p>\n<p>The kitchen opens onto the living-room which can also be reached from the other side.The living-room faces South, which will give you an astonishing light all day. It also has two balconies with an unobstructed view on Paris, the roof tops or the Eiffel Tower guaranteed. The living-room has a sofabed (queen size mattress 160x205), armchairs and a flatscreen TV set. You will find a desk right next to the living-room, in a small room open on the main room, where you will have a chance to comfortably settle down to work with your computer.<\/p>\n<p>The corridor that goes from the entrance door to the main room also leads to the second bedroom, next to the living-room. It features a double bed (140x200) and a cabinet with storage space. You will also find drawers under the base of the bed. This bedroom is so charming, as is the whole of this amazing Paris apartment. It is facing south as well, so this room will be flooded with light all day.<\/p>\n<p>The bathroom is next to the second bedroom. It features a walk-in shower and a toilet.<\/p>\n<p>To sum up, if you walk straight from the entrance door, you will reach the dining area first, then the bathroom, a bedroom, the little office room, the dining room, the kitchen, another bedroom and the entrance hall.<\/p>\n<p>This wonderful short term Paris apartment can accomodate up to six guests. The choice of the colors, the furniture, the decoration and everything else has been made and chosen to offer you an unforgettable stay in Paris, comfortably installed in a very good standing apartment where you will always have a ray of light coming in from one of the many windows. Your only concern will be to determine which part of the apartment has the best light and at what time. What a pleasure when the night comes to see the Eiffel Tower sparkling for a few minutes from your new home sweet home. This breathtaking view of the city, and your stay in this Paris rental apartment, will be engraved on your memory forever!<\/p>"
```

#### Flat Photos

This function gives you all the URLs of all photos available for an apartment.

Example:

```shell
    http://<host>/rest/flat/photos/595?key=<your_key>
```

Result:

```javascript
{
    count: "60",
    urls: [
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/1.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/2.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/3.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/4.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/5.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/6.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/7.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/8.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/9.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/10.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/11.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/12.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/13.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/14.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/15.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/16.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/17.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/18.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/19.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/20.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/21.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/22.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/23.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/24.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/25.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/26.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/27.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/28.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/29.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/30.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/31.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/32.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/33.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/34.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/35.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/36.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/37.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/38.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/39.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/40.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/41.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/42.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/43.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/44.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/45.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/46.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/47.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/48.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/49.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/50.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/51.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/52.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/53.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/54.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/55.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/56.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/57.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/58.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/59.jpg",
        "http://s3.amazonaws.com/bee-static/france/paris/A-VIEW99/larges/60.jpg"
    ]
}
```

#### Flat Availability

This function will return all the blocking periods for the apartment. It accepts a parameter called `ts`, which is not mandatory. By default it equals to date of the day.
This parameter allow you to start from another time. It's a UNIX timestamp, the elapsed sec from Epoc.

The result is composed of an array of periods which are not available for the apartment.
If a period started before the `ts`parameter and finished at the day of the request or later, you will get it.
Status indicates more fine information why the apartment is not available. I'm not sure you need this now, but here the list of statuses you are able to get in case of:
* 4, means apartment in hold. 
* 5, means apartment booking for the given period has been confirmed.
* 6, means apartment has been fully booked.
* 10, means the apartment is not available at all. Could be due to the owner, to heavy works, etc.

##### Example #1

```shell
    http://<host>/rest/flat/availability/595?key=<your_key>
```

Result:

```javascript
[
    {
        status: "6",
        checkin_date: "2013-12-23",
        checkout_date: "2013-12-29"
    },
    {
        status: "6",
        checkin_date: "2013-12-30",
        checkout_date: "2014-01-03"
    },
    {
        status: "6",
        checkin_date: "2014-01-03",
        checkout_date: "2014-01-08"
    },
    {
        status: "6",
        checkin_date: "2014-01-12",
        checkout_date: "2014-01-18"
    },
    {
        status: "6",
        checkin_date: "2014-04-15",
        checkout_date: "2014-04-22"
    }
]
```

##### Example #2: With a ts set to 01/09/2013

```javascript
    http://<host>/rest/flat/availability/595?key=<your_key>&ts=1377993600
```

Result:

```javascript
[
    {
        status: "6",
        checkin_date: "2013-08-02",
        checkout_date: "2013-10-27"
    },
    {
        status: "6",
        checkin_date: "2013-10-27",
        checkout_date: "2013-11-11"
    },
    {
        status: "6",
        checkin_date: "2013-11-27",
        checkout_date: "2013-12-04"
    },
    {
        status: "6",
        checkin_date: "2013-12-23",
        checkout_date: "2013-12-29"
    },
    {
        status: "6",
        checkin_date: "2013-12-30",
        checkout_date: "2014-01-03"
    },
    {
        status: "6",
        checkin_date: "2014-01-03",
        checkout_date: "2014-01-08"
    },
    {
        status: "6",
        checkin_date: "2014-01-12",
        checkout_date: "2014-01-18"
    },
    {
        status: "6",
        checkin_date: "2014-04-15",
        checkout_date: "2014-04-22"
    }
]
```

#### Flat References

This function will return the full active list of apartments available for your account. The result is an array composed of:
* `id`, ID of the apartment
* `reference`, your reference if you set it in our system (via the back-office)
* `manager_reference`, the reference used by the manager of this apartment.

If you didn't manage to rename on our system apartments, reference will be the same as the manager reference.

Example:

```shell
    http://<host>/rest/flat/references?key=<your_key>
```

Result:

```javascript
[
    {
        id: "5",
        reference: "ALBERT1",
        manager_reference: "ALBERT1"
    },
    {
        id: "8",
        reference: "ALGER3",
        manager_reference: "ALGER3"
    },
    {
        id: "10",
        reference: "AMEL108",
        manager_reference: "AMEL108"
    },
    {
        id: "17",
        reference: "ASSAS",
        manager_reference: "ASSAS"
    },
    ...
    {
        id: "997",
        reference: "ARANCIOS",
        manager_reference: "ARANCIOS"
    },
    {
        id: "1000",
        reference: "AMARIA",
        manager_reference: "AMARIA"
    },
    {
        id: "1002",
        reference: "APSARA",
        manager_reference: "APSARA"
    }
]
```

#### Flat Prices
This function will return the matrix of prices for this apartment.
The result is composed of two sections:
* `season weights`
* `prices`

All prices are in the currency fixed with the apartment.

* The season weights array

This array is composed of period with a rate. This indicates the rate applied to the price for the given period represented by start_date and end_date.

* The prices

This array is the price you can get for each different stay duration. You will get the lower price and higher price possible for this duration and the 'flat' price (with no season weight applied).

Example:

```shell
    http://<host>/rest/flat/prices/595?key=<your_key>
```

Result:

```javascript
{
    season_weights: [
        {
            start_date: "1/1/2013",
            end_date: "4/1/2013",
            rate: "1.15"
        },
        {
            start_date: "5/1/2013",
            end_date: "15/3/2013",
            rate: "0.85"
        },
        {
            start_date: "16/3/2013",
            end_date: "18/7/2013",
            rate: "1.1"
        },
        {
            start_date: "19/7/2013",
            end_date: "31/8/2013",
            rate: "1"
        },
        {
            start_date: "1/9/2013",
            end_date: "20/10/2013",
            rate: "1.1"
        },
        {
            start_date: "21/10/2013",
            end_date: "18/12/2013",
            rate: "0.85"
        },
        {
            start_date: "19/12/2013",
            end_date: "31/12/2013",
            rate: "1.15"
        }
    ],
    prices: [
        {
            duration: "1",
            lower_price: 412,
            price: 436,
            higher_price: 462
        },
        {
            duration: "3",
            lower_price: 701,
            price: 776,
            higher_price: 853
        },
        {
            duration: "5",
            lower_price: 989,
            price: 1116,
            higher_price: 1244
        },
        {
            duration: "7",
            lower_price: 1148,
            price: 1303,
            higher_price: 1459
        },
        {
            duration: "14",
            lower_price: 2104,
            price: 2427,
            higher_price: 2752
        },
        {
            duration: "21",
            lower_price: 2603,
            price: 3014,
            higher_price: 3426
        },
        {
            duration: "30",
            lower_price: 3011,
            price: 3496,
            higher_price: 3981
        },
        {
            duration: "60",
            lower_price: 5391,
            price: 6295,
            higher_price: 7201
        },
        {
            duration: "90",
            lower_price: 7824,
            price: 9158,
            higher_price: 10492
        },
        {
            duration: "180",
            lower_price: 15383,
            price: 18050,
            higher_price: 20718
        },
        {
            duration: "360",
            lower_price: 30499,
            price: 35834,
            higher_price: 41170
        }
    ]
}
```

### Booking

```
    Not yet avaialble
```

### Util

```
    Not yet avaialble
```

