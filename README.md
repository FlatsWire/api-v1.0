# FlatsWire API

This FlatsWire API allow you to connect to us from your own system.

## Table of Contents

* [FlatsWire API](#flatswire-api)
    * [Table of Contents](#table-of-contents)
    * [General](#general)
    * [Connection](#connection)
    * [Support](#support)
    * [Domains](#domains)
        * [Flat](#domain-flat)
            * [Get](#domain-flat-get)
            * [Description](#domain-flat-description)
        * [Booking](#domain-booking)
        * [Util](#domain-utils)


## General


## Connection

All API resources available are with this pattern:

```shell
http://<host>/rest/<domain>/<function>/<ID?>?key=<Your Key>
```

* `host` is the host to connect to. It will be given to you once your account will be created.
* `domain` is the domain of the function you want to call.
There is actually 3 differents domains:
    * `flat` which is related on all properties management;
    * `booking` which is related on all booking management;
    * `util` which is related on all function to help to know about Beethoven;
* `id` is an optional ID. It depends on the function called.
* `key` is your API key. It's required to authenticate you as a user of the API.

To obtain your key, you need to have an account registred on our system. Please contact sales@flatswire.com to get more information about this.

## Support

## Domains

### Flat

#### Get

#### Description

### Booking

### Util


