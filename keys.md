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
```javascript

## Checkin

This methods is used to tell the system the position (geo location) of a key.

```html
    POST http://<host>/rest/keys/checkin/<item_id>/<sequence_id>?key=<your_key>
```

Parameters are:
- item_id The ID of the accommodation
- sequence_id The sequence number of the key

Example:

```javascript
http://<host>/rest/keys/checkin/5/3?key=<your_key>
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
```javascript


