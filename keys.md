# FlatsWire API - User

This domain allows to manage keys in Beethoven.

## Table of Contents

* [Get](#get)
* [Checkin](#get)

## Get

Use this method to get the details of a key.


```html
    http://<host>/rest/keys/get/<item_id>/<sequence_id>?key=<your_key>
```

Parameters are:
- item_id The ID of the accommodation
- sequence_id The sequence number of the key

Example:

```javascript
  GET http://<host>/rest/keys/get/5/3?key=<your_key>
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


