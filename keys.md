# FlatsWire API - User

This domain allows to manage keys in Beethoven.

## Table of Contents

* [Get](#get)
* [Checkin](#get)

## Get

This method returns the details of a specific key. A key is identified by the related accommodation (`item_id`) and a sequence number.


```html
    GET http://<host>/rest/keys/get/<item_id>/<sequence_id>?key=<your_key>
```

Parameters are:
- item_id: The ID of the accommodation
- sequence_id: The sequence number of the key

The method returns a checkin object:
- flat_id: The id of the accommodation (same as item_id)
- sequence: The sequence of the key
- color: the tag color of the key
- last_checkin_id: The ID of the last checkin operation. Use this ID with keys/get_checkin to get details of this operation
- notes Information about this key
- valid Boolean which tells weather the key is active or not. 
 

Example:

```javascript
  http://<host>/rest/keys/get/5/3?key=<your_key>
```

Result:
```javascript
{
  "flat_id": "5",
  "sequence": "3",
  "color": "#0433ff",
  "last_checkin_id": "10877",
  "notes": null,
  "valid": "1"
}
```

## Checkin

This methods is used to tell the system the position (geo location) of a key.

```html
    POST http://<host>/rest/keys/checkin/<item_id>/<sequence_id>?key=<your_key>
```

Parameters are:
- item_id The ID of the accommodation
- sequence_id The sequence number of the key

The required Post data are:
- action: The action to performed. You have to use the numerical value of the action. An invalid action value raised an exception. There is 3 different actions available:
    * PICK (value = 1) which means the user pick-up the key from its position
    * DROP (value = 2) which means the user drop the key in its position
    * CHECKIN (value = 3) which means the user record the position of the key (which is its position)
- lat: The actual latitude of the user
- lng: The actual longitude of the user
- user_id: The user ID who is performing the checkin

The methods returns a checkin object:
- id: The ID of the inserted checkin
- flat_id: The id of the accommodation (same as item_id)
- sequence: The sequence of the key
- action: The action done by the checkin operation
- latitude: The latitude where the operation occured
- longitude: The longitude where the operation occured
- user_id: The user ID of the user which performed the operation
- checkin_date: The timestamp when occured the operation

Example:

```javascript
http://<host>/rest/keys/checkin/5/3?key=<your_key>
lat=48.8635
lng=2.35911
user_id=486
action=2
```

Result:
```javascript
{
  "id": 27502,
  "flat_id": "5",
  "sequence": "3",
  "action": "2",
  "latitude": "48.8635",
  "longitude": "2.35911",
  "user_id": "486",
  "checkin_date": "2015-07-30 10:24:03"
}
```javascript


