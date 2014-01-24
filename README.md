# FlatsWire API

FlatsWire API is a [DSL](http://en.wikipedia.org/wiki/Domain-specific_language) for
quickly creating web applications in Ruby with minimal effort:

``` json
# myapp.rb
require 'sinatra'

get '/' do
  'Hello world!'
end
```

Install the gem:

``` shell
gem install sinatra
```

And run with:

``` shell
ruby myapp.rb
```

View at: http://localhost:4567

It is recommended to also run `gem install thin`, which Sinatra will
pick up if available.

## Table of Contents

* [Sinatra](#sinatra)
    * [Table of Contents](#table-of-contents)
    * [Routes](#routes)
    * [Conditions](#conditions)
    * [Return Values](#return-values)
    * [Custom Route Matchers](#custom-route-matchers)
    * [Static Files](#static-files)
    * [Views / Templates](#views--templates)
        * [Literal Templates](#literal-templates)
        * [Available Template Languages](#available-template-languages)
            * [Haml Templates](#haml-templates)
            * [Erb Templates](#erb-templates)
            * [Builder Templates](#builder-templates)
            * [Nokogiri Templates](#nokogiri-templates)
            * [Sass Templates](#sass-templates)
            * [SCSS Templates](#scss-templates)
            * [Less Templates](#less-templates)
            * [Liquid Templates](#liquid-templates)
            * [Markdown Templates](#markdown-templates)
            * [Textile Templates](#textile-templates)
            * [RDoc Templates](#rdoc-templates)
            * [Radius Templates](#radius-templates)
            * [Markaby Templates](#markaby-templates)
            * [RABL Templates](#rabl-templates)
            * [Slim Templates](#slim-templates)
            * [Creole Templates](#creole-templates)
            * [CoffeeScript Templates](#coffeescript-templates)
            * [Stylus Templates](#stylus-templates)
            * [Yajl Templates](#yajl-templates)
            * [WLang Templates](#wlang-templates)
        * [Accessing Variables in Templates](#accessing-variables-in-templates)
        * [Templates with `yield` and nested layouts](#templates-with-yield-and-nested-layouts)
        * [Inline Templates](#inline-templates)
        * [Named Templates](#named-templates)
        * [Associating File Extensions](#associating-file-extensions)
        * [Adding Your Own Template Engine](#adding-your-own-template-engine)
    * [Filters](#filters)
    * [Helpers](#helpers)
        * [Using Sessions](#using-sessions)
        * [Halting](#halting)
        * [Passing](#passing)
        * [Triggering Another Route](#triggering-another-route)
        * [Setting Body, Status Code and Headers](#setting-body-status-code-and-headers)
        * [Streaming Responses](#streaming-responses)
        * [Logging](#logging)
        * [Mime Types](#mime-types)
        * [Generating URLs](#generating-urls)
        * [Browser Redirect](#browser-redirect)
        * [Cache Control](#cache-control)
        * [Sending Files](#sending-files)
        * [Accessing the Request Object](#accessing-the-request-object)
        * [Attachments](#attachments)
        * [Dealing with Date and Time](#dealing-with-date-and-time)
        * [Looking Up Template Files](#looking-up-template-files)
    * [Configuration](#configuration)
        * [Configuring attack protection](#configuring-attack-protection)
        * [Available Settings](#available-settings)
    * [Environments](#environments)
    * [Error Handling](#error-handling)
        * [Not Found](#not-found)
        * [Error](#error)
    * [Rack Middleware](#rack-middleware)
    * [Testing](#testing)
    * [Sinatra::Base - Middleware, Libraries, and Modular Apps](#sinatrabase---middleware-libraries-and-modular-apps)
        * [Modular vs. Classic Style](#modular-vs-classic-style)
        * [Serving a Modular Application](#serving-a-modular-application)
        * [Using a Classic Style Application with a config.ru](#using-a-classic-style-application-with-a-configru)
        * [When to use a config.ru?](#when-to-use-a-configru)
        * [Using Sinatra as Middleware](#using-sinatra-as-middleware)
        * [Dynamic Application Creation](#dynamic-application-creation)
    * [Scopes and Binding](#scopes-and-binding)
        * [Application/Class Scope](#applicationclass-scope)
        * [Request/Instance Scope](#requestinstance-scope)
        * [Delegation Scope](#delegation-scope)
    * [Command Line](#command-line)
    * [Requirement](#requirement)
    * [The Bleeding Edge](#the-bleeding-edge)
        * [With Bundler](#with-bundler)
        * [Roll Your Own](#roll-your-own)
        * [Install Globally](#install-globally)
    * [Versioning](#versioning)
    * [Further Reading](#further-reading)

## Routes

In Sinatra, a route is an HTTP method paired with a URL-matching pattern.
Each route is associated with a block:

``` ruby
get '/' do
  .. show something ..
end

post '/' do
  .. create something ..
end

put '/' do
  .. replace something ..
end

patch '/' do
  .. modify something ..
end

delete '/' do
  .. annihilate something ..
end

options '/' do
  .. appease something ..
end

link '/' do
  .. affiliate something ..
end

unlink '/' do
  .. separate something ..
end
```