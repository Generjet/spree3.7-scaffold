SpreeScaffold
=============

An advanced admin scaffold generator for Spree.
This gem is inherited from https://github.com/freego/spree_scaffold

Creates a ready to use CRUD interface for your models inside Spree admin.
Attachments, sorting and translations are supported.

This gem is now compatible with spree-3.7.13 and runs rails 5.2.0, ruby-2.6.4 normally.

Installation
============

Add this line to your application's Gemfile:
```ruby
group :development do
  gem 'spree_scaffold', github: 'freego/spree_scaffold', branch: 'X-X-stable'
end
```

And then execute:

    $ bundle

Usage
=====

Generate a scaffold for the new `Brand` model:

    $ rails generate spree_scaffold:scaffold Brand name:string description:text position:integer ... [--i18n name description]

And adjust the [glyphicons](http://glyphicons.com/) icon name on the `app/overrides/spree/admin/add_spree_...` file.

It's better if the first attribute is the "main" text one (name, title etc.)

Some more magic:
* The admin index list will be sortable with drag&drop if you create a `position:integer` field
* `paperclip` image and file attachments are supported: e.g. `picture:image attachment:file`
* Will use `friendly_id` for slugs if a `slug:string` field is present

Example output:

    create  app/models/spree/brand.rb
    create  app/controllers/spree/admin/brands_controller.rb
    create  app/views/spree/admin/brands/index.html.erb
    create  app/views/spree/admin/brands/new.html.erb
    create  app/views/spree/admin/brands/edit.html.erb
    create  app/views/spree/admin/brands/_form.html.erb
    create  db/migrate/20140412175904_create_spree_brands.rb
    create  config/locales/en_brands.yml
    create  config/locales/it_brands.yml
    create  app/overrides/spree/admin/add_spree_brands_to_admin_menu.rb
    append  config/routes.rb


Before migration
======
Before migration edit db/migrate/xxxxxx.rb file, and add rails version number like ActiveRecord::Migration[5.2].

For example:

class CreateSpreeFinanceAccounts < ActiveRecord::Migration[5.2]
  def up
    create_table :spree_finance_accounts do |t|
      t.string :name
      t.integer :head_code
      t.integer :code
      t.integer :account_type
      t.text :detail
      t.timestamps
    end
  end

  def down
    drop_table :spree_finance_accounts
  end
end

Then run the migration:

    $ rake db:migrate

To rollback:

    $ rake db:rollback
    $ rails destroy spree_scaffold:scaffold Brand name:string description:text position:integer ...

Copyright (c) 2015 sebastyuiop, alepore, released under the New BSD License
