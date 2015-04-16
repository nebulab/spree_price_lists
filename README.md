SpreePriceLists
===============

Multiple price lists support for Spree.

You can have multiple price lists for each Variant, and assign a different one
to each session via some logic.

Installation
------------

Add spree_price_lists to your Gemfile:

```ruby
gem 'spree_price_lists', github: 'freego/spree_price_lists', branch: 'X-X-stable'
```

Bundle your dependencies and run the installation generator:

```shell
bundle
bundle exec rails g spree_price_lists:install
```

This will create a default price list.

Usage
-----

This extension is pretty generic and needs some manual intervention to be useful.
You must, at least:

* add a custom logic for price list (see below)
* updater all cache keys with `current_price_list` instead of `current_currency`

Price List Logic
----------------

By default, the default (or first) price list is used. This should not break
existing behaviour.
You can add your own logic like this:

```ruby
module Spree
  BaseController.class_eval do
    private

    def get_price_list
      # your logic here, will use default price list if nil
    end
  end
end
```

For example, your logic may be country-based or user-based.

Testing
-------

First bundle your dependencies, then run `rake`. `rake` will default to building the dummy app if it does not exist, then it will run specs. The dummy app can be regenerated by using `rake test_app`.

```shell
bundle
bundle exec rake
```

When testing your applications integration with this extension you may use it's factories.
Simply add this require statement to your spec_helper:

```ruby
require 'spree_price_lists/factories'
```

Copyright (c) 2015 Alessandro Lepore, released under the New BSD License
