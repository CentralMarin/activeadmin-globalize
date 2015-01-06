# ActiveAdmin::Globalize
Makes it easy to translate your resource fields.

## Installation

```ruby
gem "activeadmin-globalize", github: 'CentralMarin/activeadmin-globalize',
branch: 'master'
```
We still need to use GitHub because ActiveAdmin is still in active development
and there's no released gem compatible with Rails 4.

## Your model

```ruby
active_admin_translates :title, :description do
  validates_presence_of :title
end
```
## Editor configuration

```ruby
# if you are using Rails 4 or Strong Parameters:
permit_params translations_attributes: [:locale, :title, :content]


index do
  # ...
  translation_status
  # ...
  default_actions
end

form do |f|
  f.inputs do # Must have at least one
    # ...
    f.translated_inputs "Translated fields", switch_locale: false do |t|
      t.input :title
      t.input :content
    end
  end
  # ...
end
```
If `switch_locale` is set, each tab will be rendered switching locale.

## Hints

To use the dashed locale keys as 'pt-BR' or 'pt-PT' you need to convert a string
to symbol (in application.rb)

  config.i18n.available_locales = [:en, :it, :de, :es, :"pt-BR"]

## Troubleshooting
If only one of your input fields is showing up, you're missing a f.inputs around your f.translated_inputs
