**This is a new feature not yet deployed on the production server**

#### Booking Update

This function updates a booking with specific data. The updatable fields are retricted by the booking status.
The fields with their data have to be sent by `POST`.


Example:

```shell
	http://<host>/rest/booking/update/101992?key=<your_key>

	with in the POST:
	adults=2
```

Result:

```json
{
    "updated": {
        "adults": "2"
    }
}
```

This request set the number of adults of the booking to 2.

The response contains up to 3 fields:

* updated: which is the list of key/values actually updated.
* rejected: the list of field/property rejected by the update. A field or property is rejected when it is not allowed to be updated according to the booking status.
* same_value: the list of field/property not used for the update because the value is already the same in the booking.

> The system does not update a value if the value to set is the same.

If you try to update again the number of adult with 2, you will get this response:

```json
{
    "success": false,
    "message": "Nothing to update.",
    "rejected": [],
    "same_value": [
        "adults"
    ]
}
```

And if you try to update this value for a FIRM booking:

```json
{
    "success": false,
    "message": "Nothing to update.",
    "rejected": [
        "adults"
    ],
    "same_value": []
}
```

There is two kind of data for a booking:

* Booking data
* Booking properties


##### Booking data

These data are information contains in the booking like number of adults, number of children, etc.
Here the liste of available fields for an update:

| Name | Description | Restrictions |
|------|-------------|--------------|
| adults | Number of adult | status<CONFIRMED, Integer |
| children | Number of children | status<CONFIRMED, Integer |
| comments | Comments of the customer | |


To update a booking data, you have to use as parameter the name of the field:

```shell
    adults=2
    children=3
```

##### Booking properties

These properties consist of information defined by a key and a value.
They may refer to a lot of different kind of data.

These properties can be updated from booking status CONFIRMED. Except for the property: `99:cleaning.requested` which required a booking status LOCK.

When a value is updated in the system, a timestamp and the user (here the API) are recorded as well whitin property. These data are available from the backoffice.

There is no type for a property. All is text value. If the property except to be considered as a boolean (i.e.: `bkg.arr.taxi.requested`), you must set 1 (true) or 0 (false).

> Any other values will be considered as 0 (false).

To update a booking property you have to use the property ID as parameter name:

```shell
    41=CDG - Charles De Gaulles Airport
    59=1
    69=5  
```

##### List of properties

###### Arrival information


| ID | Name | Description | Restrictions |
|----|------|-------------|--------------|
|43  | bkg.arr.date | Arrival date<br/>(may be different from the actual booking arrival date) |  | 
| 150  |  bkg.arr.flight.arr_date | Arrival date at destination of the arrival flight |  | 
| 146  |  bkg.arr.flight.arr_time | Arrival time at destination of the arrival flight |  | 
| 149  |  bkg.arr.flight.dep_date | Departure date of the flight from origin | 
| 145  |  bkg.arr.flight.dep_time | Departure time of the flight from origin | 
| 41   |  bkg.arr.flight.from | Airport origin of the arrival flight | 
| 40   |  bkg.arr.flight.number | Arrival flight number | 2 letters airline IATA code and up to 4 digits, i.e.: AF0007, EK1 | 
| 44   |  bkg.arr.location | Location of arrival for the transport (airport, train station, etc.) | 
| 69   |  bkg.arr.taxi.persons | Number of persons for the taxi | 
| 59   |  bkg.arr.taxi.requested | Tells whether customers resquested a taxi upon the arrival | 1=taxi requested, 0=taxi not requested | 
| 42   |  bkg.arr.time | Time of arrival | 
| 138  |  bkg.arr.transport | Type of transport used | Available values: |  

###### Departure information

| ID | Name | Description | Restrictions |
|----|------|-------------|--------------|
| 48  | bkg.dep.date | Departure date | |
| 54  | bkg.dep.flat.time | Departure time from the flat | |
| 152 | bkg.dep.flight.arr_date | Arrival date at destination of the departure flight | |
| 148 | bkg.dep.flight.arr_time | Arrival time at destination of the departure flight | |
| 151 | bkg.dep.flight.dep_date | Departure date from origin of the departure flight | |
| 147 | bkg.dep.flight.dep_time | Departure time from origin of the departure flight | |
| 45  | bkg.dep.flight.number | Departure flight number | 2 letters airline IATA code and up to 4 digits, i.e.: AF0007, EK1 |
| 46  | bkg.dep.flight.to | Airport destination of the departure flight | |
| 49  | bkg.dep.location | Location of departure for the transport (airport, train station, etc.) | |
| 60  | bkg.dep.taxi.requested | Tells whether customers resquested a taxi upon the departure | 1=taxi requested, 0=taxi not requested | 
| 47  | bkg.dep.time | Time of the derparture | |
| 139 | bkg.dep.transport | Type of transport used for the departure | Available values: | 

###### Customer information

| ID  | Name | Description | Restrictions |
|-----|------|-------------|--------------|
| 51  | bkg.customer.phone1 | 1st customer phone available at the place of the location, wihtout country code and area code | |
| 52  | bkg.customer.phone2 | 1st customer phone available at the place of the location, wihtout country code and area code | |
| 155 | bkg.customer.prefix_phone1 | Phone prefix to use with the customer phone #1 (i.e: +33, +1, +44, etc.) | |
| 156 | bkg.customer.prefix_phone2 | Phone prefix to use with the customer phone #2 (i.e: +33, +1, +44, etc.) | |
| 157 | bkg.customer.country_phone1 | The ISO 2 letters country code of the customer #1 phone number (i.e.: FR, US, UK) | |
| 158 | bkg.customer.country_phone2 | The ISO 2 letters country code of the customer #2 phone number (i.e.: FR, US, UK) | |


Beethoven system can store per booking up to 10 differents customer name and passport combinations.

These information are:

* First name
* Last name
* Passport number

Index goes from 1 to 10.

> If the customer who did the booking is a part of the trip, it is required to set his information here too. As convention these information should be set on customer #1.

| ID | Name |
|----|------------------------|
|101 | customer.1.first_name |
|115 | customer.1.last_name |
|125 | customer.1.passport |
|102 | customer.2.first_name |
|116 | customer.2.last_name |
|126 | customer.2.passport |
|103 | customer.3.first_name |
|117 | customer.3.last_name |
|127 | customer.3.passport |
|104 | customer.4.first_name |
|118 | customer.4.last_name |
|128 | customer.4.passport |
|105 | customer.5.first_name |
|119 | customer.5.last_name |
|129 | customer.5.passport |
|106 | customer.6.first_name |
|120 | customer.6.last_name |
|130 | customer.6.passport |
|107 | customer.7.first_name |
|121 | customer.7.last_name |
|131 | customer.7.passport |
|108 | customer.8.first_name |
|122 | customer.8.last_name |
|132 | customer.8.passport |
|109 | customer.9.first_name |
|123 | customer.9.last_name |
|133 | customer.9.passport |
|110 | customer.10.first_name |
|124 | customer.10.last_name |
|134 | customer.10.passport |

###### Extra information

| ID | Name | Description | Restrictions |
|----|------|-------------|--------------|
| 99 | cleaning.requested | Tells whether a cleaning is requested at the end of the booking|1=Cleaning requested<br/>0=Cleaning not requested |

