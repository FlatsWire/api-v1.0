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
            * [Flat Media](#flat-media)
            * [Flat Availability](#flat-availability)
            * [Flat References](#flat-references)
            * [Flat Prices](#flat-prices)
            * [Flat Check](#flat-check)
            * [Flat Push](#flat-push)
            * [Flat Update](#flat-update)
        * [Booking](#booking)
            * [Booking Get](#booking-get)
            * [Booking Push](#booking-push)
            * [Booking Update Status](#booking-update-status)
            * [Booking All](#booking-all)
        * [Customer](#customer)
            * [Customer Get](#customer-get)
        * [Account](#account)
       	    * [Account Managers](#account-managers)

## General


## Connection

All API resources available are with this pattern:

```html
    http://<host>/rest/<domain>/<function>/<id>?key=<your_key>
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

```html
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

```html
    http://<host>/rest/flat/description/595?key=<your_key>
```

Result:

```javascript
"<h5>Location<\/h5>\n<p>This short term Paris apartment rental is located in the 11th district, two steps away from the famous P&egrave;re Lachaise cemetery where Edith Piaf, Jim Morrison, Alexandre Dumas and many more are buried. You will love this lively area, already beloved by its residents, where you will find many shops, supermarkets, restaurants, caf&eacute;s and venues, particularly in the nearby Oberkampf Street. The Pere Lachaise open air market takes place twice a week (on Tuesdays and Fridays). This is a very nice market with fresh products : fruits, vegetables, cheese etc.The closest metro stations are St Maur (line 3) and P&egrave;re Lachaise (line 2 and 3). Line 3 is very convenient : Republique is 2 stops away, Arts et M&eacute;tiers is 4 stops away and Opera is 8 stops away. Count 2 minutes per stop : hence you will be close to many different parts of the city.<\/p>\n<h5>Standing<\/h5>\n<p>This Paris apartment is located on the 7th floor (top floor) of a very good standard building equipped with a lift. Access is secured by a door code and a very careful building keeper. The lift will lead you to the 6th floor and you will have to climb the stairs to reach your Paris apartment on the 7th floor. The 11 windows are double glazed and offer an extraordinary view on Paris.<\/p>\n<h5>Layout<\/h5>\n<p>This 93sqm apartment in Paris is a pure jewel. It used to be seven maids' room which have been transformed into a large apartment. It is organized around a small courtyard in the middle of the apartment (there is no particular view on this courtyard but it adds three more windows with more light coming through). The aparment is bright all day long and it is a real pleasure to live here.<\/p>\n<p>The entrance hall of this apartment in Paris is spacious with storage space and opens on the left hand side onto the dining area (with a dining table where six guests can sit) and on the right hand side onto the first bedroom, also quiet and spacious. A lovely room divider from a famous designer gives more intimacy to the people sleeping in this bedroom, even if the bed is on the opposite side of the bedroom. The bedroom features a double bed (140x200) and a very large wardrobe (with room for around 25 hangers, plus drawers and shelves). The apartment also has a lovely north-facing balcony, from where you will have the pleasure to watch the beautiful light of the sunset reflecting on the building in front of you.<\/p>\n<p>This first bedroom leads into the kitchen. It is a modern well equipped kitchen with a small dining table. It has a sky light, which adds even more to the light already filling the apartment.<\/p>\n<p>The kitchen opens onto the living-room which can also be reached from the other side.The living-room faces South, which will give you an astonishing light all day. It also has two balconies with an unobstructed view on Paris, the roof tops or the Eiffel Tower guaranteed. The living-room has a sofabed (queen size mattress 160x205), armchairs and a flatscreen TV set. You will find a desk right next to the living-room, in a small room open on the main room, where you will have a chance to comfortably settle down to work with your computer.<\/p>\n<p>The corridor that goes from the entrance door to the main room also leads to the second bedroom, next to the living-room. It features a double bed (140x200) and a cabinet with storage space. You will also find drawers under the base of the bed. This bedroom is so charming, as is the whole of this amazing Paris apartment. It is facing south as well, so this room will be flooded with light all day.<\/p>\n<p>The bathroom is next to the second bedroom. It features a walk-in shower and a toilet.<\/p>\n<p>To sum up, if you walk straight from the entrance door, you will reach the dining area first, then the bathroom, a bedroom, the little office room, the dining room, the kitchen, another bedroom and the entrance hall.<\/p>\n<p>This wonderful short term Paris apartment can accomodate up to six guests. The choice of the colors, the furniture, the decoration and everything else has been made and chosen to offer you an unforgettable stay in Paris, comfortably installed in a very good standing apartment where you will always have a ray of light coming in from one of the many windows. Your only concern will be to determine which part of the apartment has the best light and at what time. What a pleasure when the night comes to see the Eiffel Tower sparkling for a few minutes from your new home sweet home. This breathtaking view of the city, and your stay in this Paris rental apartment, will be engraved on your memory forever!<\/p>"
```

#### Flat Photos

**Deprecated**: You must use now flat/media. This method is still working but only for accomodation added into FlatsWire up to June 2014. After this date, you'll get an empty list as result.

This function gives you all the URLs of all photos available for an apartment.

Example:

```html
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

#### Flat Media

Note: Photos storage has been changed and you need to change your implementation to follow the new way described in this method.

This method returns all media available for this accomodation. The result is composed of a list of media object with the following fields:
- `media_id` is the internal ID
- `url` is the URL from where you can get the media
- `creadtion_date` is the date of the first upload on the server
- `modification_date` is the date of last modification, which can be a new upload or a text change
- `deletion_date` is the date of deletion from the server of this media.
- `text` is a text to describe the media. By default this field gets the file name of the uploaded media

The 
Example:

```html
    http://<host>/rest/flat/media/1353?key=<your_key>
```

Result:

```javascript
[
	{
		media_id: "30266",
		url: "http://flatswire.s3.amazonaws.com/items/1353/larges/30266.jpg",
		creation_date: "2014-10-25 05:47:23",
		modification_date: "2014-10-25 05:47:23",
		deletion_date: null,
		text: "1-AMBROISE-sl3.jpg"
	},
	...
	{
		media_id: "30284",
		url: "http://flatswire.s3.amazonaws.com/items/1353/larges/30284.jpg",
		creation_date: "2014-10-25 05:49:08",
		modification_date: "2014-10-25 05:49:08",
		deletion_date: null,
		text: "21-AMBROISE-cz4.jpg"
	}
]
```

#### Flat Availability

This function will return all the blocking periods for the apartment.
It accepts the following parameters:
- `ts`, which is not mandatory. By default it equals to date of the day.
This parameter allow you to start from another time. It's a UNIX timestamp, the elapsed sec from Epoc.
- `id`, which is mandatory if you don't provide any id in the URL. It's a comma separated list of ID.

The result is composed of an array of periods which are not available for the apartment or an array of array if you provided a list of ids.
If a period started before the `ts`parameter and finished at the day of the request or later, you will get it.
Status indicates more fine information why the apartment is not available. 
Here the list of statuses returned for a booking:
* 4, means apartment in hold. 
* 5, means apartment booking for the given period has been confirmed.
* 6, means apartment has been fully booked.
* 10, means the apartment is not available at all. Could be due to the owner, to heavy works, etc.

When you provide a list of IDs you mustn't set the ID in the URL. The result is an array of array keyed by the flat ID.
If a flat has been de-activated or deleted, the response won't have it.
If you are not authorized to use this apartment, the request failed with the appropriate error message and related flat ID.

> If a blocked period is due to your booking, you will get its ID on the field called: booking_id.

##### Example #1

```html
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
        checkout_date: "2014-04-22",
        booking_id: "123456"
    }
]
```

##### Example #2: With a ts set to 01/09/2013

```html
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
        checkout_date: "2013-12-04",
        booking_id: "123456"
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

##### Example #3

With a list of IDs.

```html
    http://<host>/rest/flat/availability?key=<your_key>&id=595,320,821
```

Result:

```javascript
{
    "595": [
        {
            "status": "10",
            "checkin_date": "2014-06-27",
            "checkout_date": "2014-07-03"
        },
        {
            "status": "10",
            "checkin_date": "2014-07-04",
            "checkout_date": "2014-12-31"
        },
        {
            "status": "5",
            "checkin_date": "2016-06-16",
            "checkout_date": "2016-06-21"
        }
    ],
    "821": [
        {
            "status": "10",
            "checkin_date": "2014-07-01",
            "checkout_date": "2014-07-12"
        },
        {
            "status": "10",
            "checkin_date": "2014-07-13",
            "checkout_date": "2014-07-30"
        },
        {
            "status": "6",
            "checkin_date": "2014-08-01",
            "checkout_date": "2015-07-31"
        }
    ]
}
```
#### Flat References

This function will return the full active list of apartments available for your account. 

This method takes an optional parameter `date`. The format has to be in Y-m-d. Example: 2015-09-01.
If this parameter is provided. The method will return only accommodations created or modified from this date.

```html
    http://<host>/rest/flat/references/<Y-m-d>?key=<your_key>
```

Two additionals parameters can be set:
- manager, when set, result are filtered by manager. The value to set is an int which represents the ID of the manager.
- enabled, when set, result are filtered by activated or desactivated or both status of accommodations. Values are :
	+ all : returns activated and desactivated accommodations. This is the default value if not set;
	+ 0: returns only desactivated accommodations;
	+ 1: returns only activated accommodations.

The following query returns all desactivated accommodations for the manager ID 41, since the 1st of June 2017:

```html
    http://<host>/rest/flat/references/2017-06-01?key=<your_key>&manager=41&enabled=0
```


The result is an array composed of:
* `id`, ID of the accommodation.
* `reference`, your reference if you set it in our system (via the back-office).
* `manager_reference`, the reference used by the manager of this accommodation.
* `creation_date`, The date of creation of the accommodation.
* `modification_date`, The last date of modification of the accommodation.

If you didn't manage to rename on our system apartments, reference will be the same as the manager reference.

Example:

```html
    http://<host>/rest/flat/references?key=<your_key>
```

Result:

```javascript
[
    {
        id: "5",
        reference: "ALBERT1",
        manager_reference: "ALBERT1",
    	creation_date: "2014-08-19 12:22:55",
    	modification_date: "2015-09-01 11:12:56"
    },
    ...
    {
        id: "1002",
        reference: "APSARA",
        manager_reference: "APSARA",
    	creation_date: "2013-09-24 16:07:34",
    	modification_date: "2015-09-02 18:44:47"
    }
]
```

#### Flat Prices

This function will return the matrix of prices for this apartment.
The result is composed of two sections:
* `season weights`
* `prices`

All prices are in the apartment currency.

```html
	http://<host>/rest/flat/prices/<accommodation_id>?key=<your_key>
```

* The season weights array

This array is composed of period with a rate. This indicates the rate applied to the price for the given period represented by start_date and end_date.

* The prices

This array is the price you can get for each different stay duration by all the season weights.

You can use the parameter called `net` to select between net prices or retail prices. If the `net` parameter is equal to 1, prices are net. If the parameter is equal to 0, the prices included your margin.
This parameter is optional and by default the method returns net prices.

Example:

```html
    http://<host>/rest/flat/prices/595?key=<your_key>
```

Result:

```javascript
{
	season_weights: [
	{
		start_date: "01/01/2014",
		end_date: "04/01/2014",
		rate: "1.15"
	},
	{
		start_date: "05/01/2014",
		end_date: "15/03/2014",
		rate: "0.85"
	},
	{
		start_date: "16/03/2014",
		end_date: "18/07/2014",
		rate: "1.1"
	},
	{
		start_date: "19/07/2014",
		end_date: "31/08/2014",
		rate: "1"
	},
	{
		start_date: "01/09/2014",
		end_date: "20/10/2014",
		rate: "1.1"
	},
	{
		start_date: "21/10/2014",
		end_date: "18/12/2014",
		rate: "0.85"
	},
	{
		start_date: "19/12/2014",
		end_date: "31/12/2014",
		rate: "1.15"
	}
	],
	prices: {
		1: {
			1: 43700,
			1.15: 46300,
			0.85: 41200,
			1.1: 45400
		},
		3: {
			1: 77800,
			1.15: 85300,
			0.85: 70100,
			1.1: 82800
		},
		5: {
			1: 111600,
			1.15: 124500,
			0.85: 98900,
			1.1: 120100
		},
		7: {
			1: 130400,
			1.15: 146000,
			0.85: 114800,
			1.1: 140900
		},
		14: {
			1: 242800,
			1.15: 275300,
			0.85: 210400,
			1.1: 264500
		},
		21: {
			1: 301600,
			1.15: 342700,
			0.85: 260300,
			1.1: 329000
		},
		30: {
			1: 349700,
			1.15: 398100,
			0.85: 301200,
			1.1: 382000
		},
		60: {
			1: 629700,
			1.15: 720100,
			0.85: 539200,
			1.1: 690000
		},
		90: {
			1: 915900,
			1.15: 1049200,
			0.85: 782500,
			1.1: 1004900
		},
		180: {
			1: 1805100,
			1.15: 2071800,
			0.85: 1538300,
			1.1: 1983000
		},
		360: {
			1: 3583500,
			1.15: 4117000,
			0.85: 3050000,
			1.1: 3939300
		}
	}
}
```

To get the final price, you must implement the following calculations:

```shell
            Dci          
P = SUM  --------- x Pci
            Dtot 
```

Where: 
- Dtot is the total duration of your stay
- Dci is the number of days spend in a season weight period
- Pci is the price of the ci season weight period

Here some examples:

A) If your booking is from the 20/07/2014 to the 25/07/2014, it spread only over one season weight: 
```javascript
{
   start_date: "19/07/2014",
   end_date: "31/08/2014",
   rate: "1"
},
```

With a rate at 1. The duration is 5 days so the price for 5 days at rate 1 is 1116 EUR. This is the price of your stay is 1116 EUR. This one is the easiest case.

B) If your booking is from the 28/08/2014 to the 04/09/2014. This one spread over two season weights:
```javascript
{
   start_date: "19/07/2014",
   end_date: "31/08/2014",
   rate: "1"
},
{
   start_date: "01/09/2014",
   end_date: "20/10/2014",
   rate: "1.1"
},
```

It will spend 3 days at rate 1 and 4 days at rate 1.1. The duration is 7 days, so at 7 days price for rate 1 is 1304 EUR and price for rate 1.1 is 1409 EUR.
So the calculation will be in this case:

```shell
P = ((7 - 3) / 7) x 1304 + ((7 - 4) / 7) x 1409 = 746 + 604 = 1350 EUR
```
Notes:

- You must all the time round to next closest integer value. In PHP is the ceil() function.
- If the total duration is not in the duration vector (ie: 6 days) you must interpolate the price before applying the calculation:

```shell
	y = (((xb - x) / (xb - xa)) x ya) + (((x - xa) / (xb -xa)) x yb
```

a et b will be the closest durations of your total duration.

Example for 6 days booking: the duration before 6 is 5 days and after is 7 days:
```javascript
5: {
   1: 111600,
   1.15: 124500,
   0.85: 98900,
   1.1: 120100
},
7: {
   1: 130400,
   1.15: 146000,
   0.85: 114800,
   1.1: 140900
},
```

To make it simple le's say we search the price for a rate 1, so the result is:

```shell
	y = (((7 - 6) / (7 - 5)) x 1116) + (((6 - 5) / (7 - 5)) x 1303) = 558 + 652 = 1210 EUR
```

#### Flat Check

This function checks the price and the availability of the apartment between two dates.

Required parameters:
* start_date, The start date of your period to check, in YYYY-mm-dd format (i.e. 2014-08-01)
* end_date, The end date of you period to check, in YYYY-mm-dd format (i.e. 2014-08-01)

Optional parameter:
* net, A boolean which indicate to the method if it must return net prices or prices with your margin. By default the method returns net prices.
* adults, An integer which tell how many adults will be there for this booking
* children, An integer which tell how many children will be there for this booking

**Notice**
> Parameters `adults` and `children` are required to get the correct amount of the city apply which may be applied for the booking

The method returns the price in cents in the apartment currency and the availability.
The availability field is a boolean where true means the apartment is available for booking between your dates, false means is not available.
The `deposit` field is the amount required to pay to secure the accomodation.

Example:

```html
    http://<host>/rest/flat/check/4093?key=<your_key>&start_date=2017-08-05&end_date=2017-08-012&adults=1&children=4
```

Result:

```javascript
{
    "available": true,
    "currency": "EUR",
    "deposit": 15848,
    "discounts": [],
    "error": false,
    "id": "4093",
    "message": false,
    "original_price": 50900,
    "price": 52825,
    "pricer": "V2",
    "success": true,
    "taxes": [
        {
            "amount": 1925,
            "code": "Taxe de Séjour",
            "conf": {
                "perimeter": {
                    "ids": [
                        "3578",
                        "3652"
                    ],
                    "type": "2"
                },
                "price": {
                    "adult": "0.55",
                    "child": "0.55",
                    "max_stay": "999"
                }
            },
            "currency": "EUR",
            "name": "TOURIST_TAX",
            "service_id": "213",
            "service_type_id": "10"
        }
    ],
    "total_price": 52825
}
```

#### Flat Push

This function creates a new accommodation.

Required parameters:
* reference, The unique reference for the accommodation.
* end_date, The end date of you period to check, in YYYY-mm-dd format (i.e. 2014-08-01).
* item_type, The type of the accommodation (Flat, Villa, Riad, House, Hostel, Hotel, Castle, Boat, Room, Bungalow, Condo).
* owner/first_name, The first name of the owner.
* owner/last_name, The last name of the owner.
* owner/email, The email of the owner.
* address/zip_code, The zip code of the accommodation.
* address/city, The city of the accommodation.
* address/country, The country of the accommodation.
* address/formatted_address, The formatted address of the accommodation.
* currency, The currency code to price the accommodation.
* district, The district in which is located the accommodation.
* nb_room, The number of rooms.

Optional parameters:
* type, The category of the accommodation (Building, Category or Flat (default)).
* parent_id, The id of the linked accommodation.
* creation_date, The creation date of the accommodation.
* external_id, The reference or id of the accommodation in your system.
* owner/phone, The phone number of the owner.
* owner/login, The login of the owner.
* owner/password, The password of the owner.
* owner/external_id, The id of the owner in your system.
* owner/iban, The IBAN of the owner.
* owner/bic, The BIC code of the owner.
* owner/use_iban, If the owner use SEPA for transfer.
* address/number, The number of the street of the accommodation.
* address/street1, The first part of the address.
* address/street2, The second part of the address.
* address/street3, The third part of the address.
* address/state, The state of the accommodation.
* address/longitude, The longitude of the accommodation.
* address/latitude, The latitude of the accommodation.
* min_stay, The minimum duration for a booking.
* max_stay, The maximum duration for a booking.
* nb_single_bed, The number of single beds.
* nb_double_bed, The number of double beds.
* nb_sofabed_1pers, The number of 1 person sofabeds.
* nb_sofabed_2pers, The number of 2 persons sofabeds.
* nb_sofabed_3pers, The number of 3 persons sofabeds.
* nb_bedroom, The number of bedrooms.
* nb_bathroom, The number of bathrooms.
* nb_separated_toilets, The number of separated toilets.
* nb_stories, The number of stories in the accommodation.
* floor, The floor on which the accommodation is located.
* american_floor_numbering, If the ground 0 is skipped in the numbering.
* note, Notes about the accommodation.
* code1, The first code of the accommodation.
* code2, The second code of the accommodation.
* phone, The phone number of the accommodation.
* wifi_ssid, The wifi name.
* wifi_password, The password of the wifi.
* virtual_tour, The link of a virtual tour.
* area, The area of the accommodation.
* area_in_sqm, If the area is mesured in square meters.
* iban, The IBAN of the accommodation.
* bic, The BIC code of the accommodation.
* amenities, A list of amenities.
* texts, A list of description of the accommodation.
* create_event_checkin, Creates a checkin event in the agenda when a booking is made.
* create_event_checkout, Creates a checkout event in the agenda when a booking is made.
* create_event_cleaning, Creates a cleaning event in the agenda when a booking is made.
* inventory_at_checkin, Makes the apartment inventory required at checkin
* inventory_at_checkout, Makes the apartment inventory required at checkout
* inventory_at_cleaning, Makes the apartment inventory required at cleaning



The method returns a list of messages showing if the accommodations have been created, or the error messages if some could not be created.

Example:

```html
    http://<host>/rest/flat/push?key=<your_key>
```
```javascript
[{		
        "reference":"TOTO",		
        "type":"",	
        "parent_id",
        "item_type":"Flat",		
        "creation_date":"2017-02-15",		
        "external_id":"TOTO1234",		
        "owner":{		
            "first_name":"John",		
            "last_name":"Doe",		
            "email":"john@doe.com",		
            "phone":"+123456789",		
            "login":"johndoe",		
            "password":"password",		
            "external_id":"JohnDoe123",		
            "iban":"12345678949654656",		
            "bic":"AA123BB",		
            "use_iban":"1"		
        },		
        "address":{		
            "number":"1",		
            "street1":"rue de paris",		
            "street2":"batiment A",		
            "street3":"3è étage",		
            "zip_code":"75001",		
            "state":"Ile De France",		
            "city":"Paris",		
            "country":"France",		
            "longitude":"2",		
            "latitude":"35",		
            "formatted_address":"1 rue de paris, 75001, Paris"		
        },		
        "min_stay":"3",		
        "max_stay":"365",		
        "nb_single_bed":"2",		
        "nb_double_bed":"1",		
        "nb_sofabed_1pers":"0",		
        "nb_sofabed_2pers":"0",		
        "nb_sofabed_3pers":"2",		
        "nb_bedrooms":"2",		
        "nb_bathrooms":"1",		
        "nb_separated_toilets":"1",		
        "currency":"EUR",		
        "nb_stories":"1",		
        "floor":"4",		
        "american_floor_numbering":"0",		
        "note":"some stuff about the accommodation",		
        "district":"Chatelet",		
        "code1":"1234",		
        "code2":"9876",		
        "phone":"+123456789",		
        "wifi_ssid":"toto_ssid",		
        "wifi_password":"password",		
        "nb_room":"4",		
        "virtual_tour":"http://somelink.com/virtualtour",		
        "area":"80",		
        "area_in_sqm":"0",		
        "iban":"16887743489468",		
        "bic":"CC546GG",		
        "amenities":{		
            "flat_wifi":"1",		
            "flat_pool":"0"		
        },		
        "texts":{		
            "fr":{		
                "description":"Une description longue de l'appartement",		
                "short_description":"une description rapide"		
            }			
            "en":{		
                "description":"A really long description of the accommodation",		
                "short_description":"a short description"		
            }		
        }		
    }]
```

Result:

```javascript
{
  "errors": [],
  "warnings": {
    "TOTO": [
      "No item type was provided, flat assumed."
    ]
  },
  "success": {
    "TOTO": [
      "The accommodation TOTO has been created."
    ]
  }
}
```

#### Flat Update

This function updates an accommodation.

Required parameters:
* flat_id, The id of the accommodation in our system.
* reference, The unique reference for the accommodation.
* end_date, The end date of you period to check, in YYYY-mm-dd format (i.e. 2014-08-01).
* item_type, The type of the accommodation (Flat, Villa, Riad, House, Hostel, Hotel, Castle, Boat, Room, Bungalow, Condo).
* owner/first_name, The first name of the owner.
* owner/last_name, The last name of the owner.
* owner/email, The email of the owner.
* address/zip_code, The zip code of the accommodation.
* address/city, The city of the accommodation.
* address/country, The country of the accommodation.
* address/formatted_address, The formatted address of the accommodation.
* currency, The currency code to price the accommodation.
* district, The district in which is located the accommodation.
* nb_room, The number of rooms.

Optional parameter:
* type, The category of the accommodation (Building, Category or Flat (default)).
* parent_id, The id of the linked accommodation.
* creation_date, The creation date of the accommodation.
* external_id, The reference or id of the accommodation in your system.
* owner/phone, The phone number of the owner.
* owner/login, The login of the owner.
* owner/password, The password of the owner.
* owner/external_id, The id of the owner in your system.
* owner/iban, The IBAN of the owner.
* owner/bic, The BIC code of the owner.
* owner/use_iban, If the owner use SEPA for transfer.
* address/number, The number of the street of the accommodation.
* address/street1, The first part of the address.
* address/street2, The second part of the address.
* address/street3, The third part of the address.
* address/state, The state of the accommodation.
* address/longitude, The longitude of the accommodation.
* address/latitude, The latitude of the accommodation.
* min_stay, The minimum duration for a booking.
* max_stay, The maximum duration for a booking.
* nb_single_bed, The number of single beds.
* nb_double_bed, The number of double beds.
* nb_sofabed_1pers, The number of 1 person sofabeds.
* nb_sofabed_2pers, The number of 2 persons sofabeds.
* nb_sofabed_3pers, The number of 3 persons sofabeds.
* nb_bedroom, The number of bedrooms.
* nb_bathroom, The number of bathrooms.
* nb_separated_toilets, The number of separated toilets.
* nb_stories, The number of stories in the accommodation.
* floor, The floor on which the accommodation is located.
* american_floor_numbering, If the ground 0 is skipped in the numbering.
* note, Notes about the accommodation.
* code1, The first code of the accommodation.
* code2, The second code of the accommodation.
* phone, The phone number of the accommodation.
* wifi_ssid, The wifi name.
* wifi_password, The password of the wifi.
* virtual_tour, The link of a virtual tour.
* area, The area of the accommodation.
* area_in_sqm, If the area is mesured in square meters.
* iban, The IBAN of the accommodation.
* bic, The BIC code of the accommodation.
* amenities, A list of amenities.
* texts, A list of description of the accommodation.
* create_event_checkin, Creates a checkin event in the agenda when a booking is made.
* create_event_checkout, Creates a checkout event in the agenda when a booking is made.
* create_event_cleaning, Creates a cleaning event in the agenda when a booking is made.
* inventory_at_checkin, Makes the apartment inventory required at checkin
* inventory_at_checkout, Makes the apartment inventory required at checkout
* inventory_at_cleaning, Makes the apartment inventory required at cleaning



The method returns a list of messages showing if the accommodations have been created, or the error messages if some could not be created.

Example:

```html
    http://<host>/rest/flat/update?key=<your_key>
```
```javascript
[{		
	"flat_id":123,
        "reference":"TOTO",		
        "type":"",	
        "parent_id",
        "item_type":"Flat",		
        "creation_date":"2017-02-15",		
        "external_id":"TOTO1234",		
        "owner":{		
            "first_name":"John",		
            "last_name":"Doe",		
            "email":"john@doe.com",		
            "phone":"+123456789",		
            "login":"johndoe",		
            "password":"password",		
            "external_id":"JohnDoe123",		
            "iban":"12345678949654656",		
            "bic":"AA123BB",		
            "use_iban":"1"		
        },		
        "address":{		
            "number":"1",		
            "street1":"rue de paris",		
            "street2":"batiment A",		
            "street3":"3è étage",		
            "zip_code":"75001",		
            "state":"Ile De France",		
            "city":"Paris",		
            "country":"France",		
            "longitude":"2",		
            "latitude":"35",		
            "formatted_address":"1 rue de paris, 75001, Paris"		
        },		
        "min_stay":"3",		
        "max_stay":"365",		
        "nb_single_bed":"2",		
        "nb_double_bed":"1",		
        "nb_sofabed_1pers":"0",		
        "nb_sofabed_2pers":"0",		
        "nb_sofabed_3pers":"2",		
        "nb_bedrooms":"2",		
        "nb_bathrooms":"1",		
        "nb_separated_toilets":"1",		
        "currency":"EUR",		
        "nb_stories":"1",		
        "floor":"4",		
        "american_floor_numbering":"0",		
        "note":"some stuff about the accommodation",		
        "district":"Chatelet",		
        "code1":"1234",		
        "code2":"9876",		
        "phone":"+123456789",		
        "wifi_ssid":"toto_ssid",		
        "wifi_password":"password",		
        "nb_room":"4",		
        "virtual_tour":"http://somelink.com/virtualtour",		
        "area":"80",		
        "area_in_sqm":"0",		
        "iban":"16887743489468",		
        "bic":"CC546GG",		
        "amenities":{		
            "flat_wifi":"1",		
            "flat_pool":"0"		
        },		
        "texts":{		
            "fr":{		
                "description":"Une description longue de l'appartement",		
                "short_description":"une description rapide"		
            }			
            "en":{		
                "description":"A really long description of the accommodation",		
                "short_description":"a short description"		
            }		
        }		
    }]
```

Result:

```javascript
{
  "errors": [],
  "warnings": {
    "TOTO": [
      "No item type was provided, flat assumed."
    ]
  },
  "success": {
    "TOTO": [
      "The accommodation TOTO has been created."
    ]
  }
}
```

### Booking

#### Booking Get

This function will return a booking from its ID.

Example:

```html
    http://<host>/rest/booking/get/101992?key=<your_key>
```

Result:

```javascript


    {
       "booking_id": "101992",
       "external_id": null,
       "reference": "EWASATHR",
       "status": "3",
       "checkin_date": "2014-05-01",
       "checkout_date": "2014-05-10",
       "creation_date": "2014-06-03 11:59:16",
       "modification_date": "2014-06-03 11:59:16",
       "adults": "2",
       "children": "0",
       "comments": "",
       "user_id": "478",
       "duration": "9",
       "sleeps": "0",
       "infants": "0",
       "is_long_term": "0",
       "selected_item_id": "595",
       "channel_id": 6,
       "channel": "FlatsWire",
       "channel_com": 0,
       "channel_booking_id":null,
       "channel_item_id": null,
       "channel_ignore": "0",
       "airbnb_id": null,
       "ha_id": null,
       "ha_source": null,
       "ha_source_url": null,
       "order_id": 123456,
       "ical_source": null,
       "ical_event_uid": null,
       "ical_event_description": null,
       "ical_event_summary": null,
       "reminder_counter": 1,
       "inventory_required": 0,
       "inventory_ko": 0,
       "customer":
       {
           "customer_id": "52510",
	   "external_id": null,
	   "gender": 0,
           "first_name": "John",
           "mid_name": null,
           "last_name": "Doe",
           "email": "john.doe@somewhere.net",
           "address_id": null,
           "account_id": "36",
           "creation_date": "2014-06-03 11:59:16",
           "modification_date": "2014-06-03 11:59:16",
           "uuid": null,
	   "number": null,
	   "street1": null,
	   "street2": null,
	   "zip_code": null,
	   "city": null,
	   "country_id": 74,
	   "latitude": 0,
	   "longitude": 0,
       },
       "properties": [
       		{
			"property_id": 0,
			"key: "property_key",
			"value": "value"
		}
       ],
       "selected_item":
       {
           "total_price": "211200",
           "partner_price": "211200",
           "partner_margin": "20",
           "partner_split": "30",
           "partner_service": "0",
           "customer_service": "0",
	   "customer_currency_rate": 1,
	   "order_id": 123456,
           "item":
           {
               "flat_id": "595",
               "customer_deal": "1",
               "min_stay": "3",
               "max_stay": "95",
               "nb_room": "4",
               "nb_person": "6",
               "nb_sleep": "3",
               "nb_dbed": "2",
               "nb_sbed": "0",
	       "nb_sofa1bed": 0,
               "nb_sofabed": "1",
	       "nb_sofa3bed": 0,
               "nb_bedroom": "2",
               "nb_bathroom": "1",
               "nb_toilette": "1",
               "floor": "7",
	       "nb_floor": "1",
	       "area": 50,
	       "area_is_metric": 1,
               "photo_count": "60",
               "enabled": "1",
               "reference": "A-VIEW99",
               "creation_date": "2011-03-18 11:24:13",
               "modification_date": "2014-06-02 17:20:43",
               "partner_reference": "REPUB06",
	       "note": "something about the apartment"
           }
       },
       payments: [
		{
			payment_id: "408650",
			from_id: null,
			to_id: false,
			user_id: null,
			customer_id: "54168",
			account_id: null,
			link_id: null,
			category: "CUSTOMER",
			code: "DEPOSIT",
			mode: "1",
			amount: "84000",
			currency: "EUR",
			currency_symbol: "&euro;",
			payment_date: "2014-06-27 05:08:55",
			creation_date: "2014-06-26 17:24:30",
			modification_date: "2014-06-27 05:08:55",
			deletion_date: null,
			deleted: "0",
			enabled: "1",
			designation: "Deposit",
			booking_id: "104240",
			status: "2",
			due_date: "2014-06-26",
			service_id: null,
			item_id: null,
			event_id: null
		},
		{},
		{},
		{},
		{},
		{}
	]	
    }
```

#### Booking Push

This function will create a booking in FlatsWire.

It is required to post this fields:
* `checkin`, The arrival date in YYYY-mm-dd format (i.e.: 2014-05-12).
* `checkout`, The departure date in YYYY-mm-dd format (i.e.: 2014-05-12).
* `selection`, The selected properties ID# list. It's a comma separated values list (i.e.: '595,13').
* `first_name`, The first name of the customer.
* `last_name`, The last name of the customer.
* `email`, The emails of the customer.
* `nb_adult`, The number of adult for this booking.

This fields are optionnel:
* `nb_children`, The number of children for this booking.
* `comments`, The customer comments.
* `status`, The status to set immediately for this booking. You are allowed to set a status between REQUEST (1) and CONFIRMED (5). If the requested status cannot be satisfied, you will get back an error message with the booking ID and booking reference. This is because the booking will be created anyway but it will stay in REQUEST (1) status.

If the post succeed, you will get back the booking if all the information. Else an error message will tell you what is wrong.


Example:

```html
    http://<host>/rest/booking/push?key=<your_key>
```

Result:

```javascript
    {
       "booking_id": 102030,
       "reference": "VUDZRZZZ",
       "status": 3,
       "checkin_date": "2014-05-01",
       "checkout_date": "2014-05-10",
       "creation_date": "2014-06-03 15:40:55",
       "modification_date": "2014-06-03 15:40:55",
       "adults": 2,
       "children": 0,
       "comments": "",
       "user_id": "478",
       "duration": "9",
       "customer":
       {
           "customer_id": 52548,
           "first_name": "John",
           "mid_name": null,
           "last_name": "Doe",
           "email": "john.doe@somewhere.net",
           "address_id": null,
           "account_id": "36",
           "creation_date": "2014-06-03 15:40:55",
           "modification_date": "2014-06-03 15:40:55",
           "uuid": null
       },
       "selected_item":
       {
           "total_price": 211200,
           "partner_price": 211200,
           "partner_margin": 20,
           "partner_split": "30",
           "partner_service": 0,
           "customer_service": 0,
           "item":
           {
               "flat_id": "595",
               "customer_deal": "1",
               "min_stay": "3",
               "max_stay": "95",
               "nb_room": "4",
               "nb_person": "6",
               "nb_sleep": "3",
               "nb_dbed": "2",
               "nb_sbed": "0",
               "nb_sofabed": "1",
               "nb_bedroom": "2",
               "nb_bathroom": "1",
               "nb_toilette": "1",
               "floor": "7",
               "photo_count": "60",
               "enabled": "1",
               "reference": "A-VIEW99",
               "creation_date": "2011-03-18 11:24:13",
               "modification_date": "2014-06-02 17:20:43",
               "currency":
               {
                   "currency_id": "45",
                   "code": "EUR",
                   "name": "Euro",
                   "symbol": "€",
                   "unicode_symbol": ""
               },
               "partner_reference": "REPUB06"
           }
       },
       "account":
       {
           "account_id": "36",
           "reference": "parisbynumbers",
           "creation_date": "2010-04-29 14:00:39",
           "modification_date": "2013-06-05 08:35:34",
           "description": null
       }
    }
```

#### Booking Update Status

This function will update the status of a booking in FlatsWire.
Two parameters are required in the URL:
* `booking_id`, The ID of the booking to update.
* `new_status`, The new status value to apply to this booking.

The status can be one value between these:
* 1 - Request
* 2 - Pending
* 3 - Option
* 4 - Hold
* 5 - Confirmed
* 6 - Firm
* 7 - Closed
* 8 - Cancelled
* 9 - Refused 
* 10 - Lock

According to the new status you try to apply, you may not authorized to do it.
Here the rules:
- An agency cannot update a status greater than 5 - Confirmed
- A manager cannot update a status lower than 3 - Option
- You can't update a booking with the same status

Example:

```html
    http://<host>/rest/booking/update_status/<booking_id>/<new_status>?key=<your_key>
```

Result:

  The result is the same as the get booking function, with the new status value as status.

```javascript
    {
       "booking_id": 102030,
       "reference": "VUDZRZZZ",
       "status": 3,
       "checkin_date": "2014-05-01",
       "checkout_date": "2014-05-10",
       "creation_date": "2014-06-03 15:40:55",
       "modification_date": "2014-06-03 15:40:55",
       "adults": 2,
       "children": 0,
       "comments": "",
       ...
       "account":
       {
           "account_id": "36",
           "reference": "parisbynumbers",
           "creation_date": "2010-04-29 14:00:39",
           "modification_date": "2013-06-05 08:35:34",
           "description": null
       }
    }

```

#### Booking All

This function will return all bookings modified from a specified date.

The `date` parameter is required. The date as to be a Y-m-d date format. Example: 2015-09-01.

The result is an array composed of 2 fields:
- `count` which is the total number of bookings.
- `bookings` which is the list of bookings.

The booking list has a maximum of 1000 entries. If the `count` is greater than 1000, this means you have to call this method with the extra parameter `page`. The number of pages available is `count` DIV 1000.

Example:

```html
    http://<host>/rest/booking/all/<date>?key=<your_key>
```

Result:

```javascript
{
  "count": 464,
  "bookings": [
    {
      "booking_id": "181964",
      "reference": "AZZZERTT",
      "checkin_date": "2015-11-27",
      "checkout_date": "2015-12-03",
      "status": "6",
      "creation_date": "2015-07-10 07:05:39",
      "modification_date": "2015-09-01 06:46:15"
    },
    ...
    {
      "booking_id": "195070",
      "reference": "ABCDEFGH",
      "checkin_date": "2015-12-06",
      "checkout_date": "2015-12-11",
      "status": "8",
      "creation_date": "2015-09-23 16:50:05",
      "modification_date": "2015-09-23 18:55:52"
    }
  ]
}
```

### Customer

#### Customer Get

This function will return you a customer record.

Example:

```html
    http://<host>/rest/customer/get/<customer_id>?key=<your_key>
```

Result:

  The result will return customer information and all the bookings he did on the platform.

```javascript
{
	customer_id: "55102",
	first_name: "John",
	mid_name: null,
	last_name: "Doe",
	email: "john.doe@somewhere.net",
	address_id: null,
	creation_date: "2014-07-21 15:34:34",
	modification_date: "2014-07-21 15:34:34",
	uuid: null,
	bookings: [
		{
		booking_id: "105940",
		reference: "ZRCILPUI",
		status: "8",
		checkin_date: "2014-09-06",
		checkout_date: "2014-09-13",
		creation_date: "2014-07-21 15:34:34",
		modification_date: "2014-07-21 15:35:27",
		adults: "2",
		children: "0",
		comments: "test",
		duration: "7",
		sleeps: "0",
		infants: "0"
		}
	]
}
```

### Account

#### Account Managers

This function will return all manager you are connected to. This function is only available if your are an account of type of "Partner".

Example:

```html
    http://<host>/rest/account/managers?key=<your_key>
```

Result:

  The result will return the list of manager with contact information, like his name and his email address.

```javascript
[
  {
    "account_id": "1298",
    "reference": "Manager A",
    "creation_date": "2010-04-29 14:00:39",
    "modification_date": "2015-09-22 12:14:07",
    "contact_email": "contact@managera.com"
  },
  ...
  {
    "account_id": "2345",
    "reference": "ManagerF",
    "creation_date": "2015-09-25 15:49:38",
    "modification_date": "2015-09-25 16:51:58",
    "contact_email": "contact@managerf.com"
  }
]
```

