# factbook-readers - turn thee world factbook country profile pages into open structured data e.g JSON

* home  :: [github.com/factbook/factbook](https://github.com/factbook/factbook)
* bugs  :: [github.com/factbook/factbook/issues](https://github.com/factbook/factbook/issues)
* gem   :: [rubygems.org/gems/factbook-readers](https://rubygems.org/gems/factbook-readers)
* rdoc  :: [rubydoc.info/gems/factbook-readers](http://rubydoc.info/gems/factbook-readers)
* forum :: [groups.google.com/group/openmundi](https://groups.google.com/group/openmundi)


## What's the World Factbook?

See [factbook/factbook.json »](https://github.com/factbook/factbook.json)



## Usage

### Get country profile page as a hash (that is, structured data e.g. nested key/values)

```ruby
page = Factbook::Page.new( 'br' )   # br is the country code for Brazil
pp page.data                        # pretty print hash
```

resulting in:

```ruby
{"Introduction"=>
  {"Background"=>
    {"text"=>
      "Following more than three centuries under Portuguese rule,
       Brazil gained its independence in 1822, ..."}},
 "Geography"=>
  {"Location"=>{"text"=>"Eastern South America, bordering the Atlantic Ocean"},
   "Geographic coordinates"=>{"text"=>"10 00 S, 55 00 W"},
   "Map references"=>{"text"=>"South America"},
   "Area"=>
    {"total"=>{"text"=>"8,515,770 sq km"},
     "land"=>{"text"=>"8,358,140 sq km"},
     "water"=>{"text"=>"157,630 sq km"},
     "note"=> "includes Arquipelago de Fernando de Noronha, Atol das Rocas, ..."},
   "Area - comparative"=>
    {"text"=>"slightly smaller than the US"},
   "Land boundaries"=>
    {"total"=>{"text"=>"16,145 km"},
     "border countries"=>
      {"text"=>
        "Argentina 1,263 km, Bolivia 3,403 km, Colombia 1,790 km,
        French Guiana 649 km, Guyana 1,308 km, Paraguay 1,371 km, Peru 2,659 km,
        Suriname 515 km, Uruguay 1,050 km, Venezuela 2,137 km"}},
   "Climate"=>{"text"=>"mostly tropical, but temperate in south"},
   "Elevation"=>
    {"lowest point"=>{"text"=>"Atlantic Ocean 0 m"},
     "highest point"=>{"text"=>"Pico da Neblina 2,994 m"}},
   "Natural resources"=>
    {"text"=>
      "bauxite, gold, iron ore, manganese, nickel, phosphates, ..."},
    ...
```

### Use data attributes

```ruby
pp page['Introduction']['Background']['text']
# => "Following more than three centuries..."
pp page['Geography']['Area']['total']['text']
# => "8,515,770 sq km"
pp page['Geography']['Area']['land']['text']
# => "8,358,140 sq km"
pp page['Geography']['Area']['water']['text']
# => "157,630 sq km"
pp page['Geography']['Area']['note']
# => "includes Arquipelago de Fernando de Noronha, Atol das Rocas, ..."
pp page['Geography']['Area - comparative']['text']
# => "slightly smaller than the US"
pp page['Geography']['Climate']['text']
# => "mostly tropical, but temperate in south"
pp page['Geography']['Terrain']['text']
# => "mostly flat to rolling lowlands in north; ..."
pp page['Geography']['Elevation']['lowest point']['text']
# => "Atlantic Ocean 0 m"
pp page['Geography']['Elevation']['highest point']['text']
# => "Pico da Neblina 2,994 m"
pp page['Geography']['Natural resources']['text']
# => "bauxite, gold, iron ore, manganese, nickel, phosphates, ..."
...
```

See [Attributes](../ATTRIBUTES.md) for a quick reference listing.


### Save to disk as JSON

```ruby
page = Factbook::Page.new( 'br' )
File.open( 'br.json', 'w:utf-8') do |f|
  f.write page.to_json
end
```


### List all codes

```ruby
Factbook.codes.each do |code|
  pp code
end
```

resulting in:

```
#<struct Factbook::Codes::Code
 code    ="af",
 name    ="Afghanistan",
 category="Countries",
 region  ="South Asia">
#<struct Factbook::Codes::Code
 code    ="al",
 name    ="Albania",
 category="Countries",
 region  ="Europe">
#<struct Factbook::Codes::Code
 code    ="ag",
 name    ="Algeria",
 category="Countries",
 region  ="Africa">
#<struct Factbook::Codes::Code
 code    ="an",
 name    ="Andorra",
 category="Countries",
 region  ="Europe">
...
```

Note: You can filter codes by category e.g. Countries, Dependencies, Miscellaneous, Oceans, etc.
and/or by region e.g. Africa, Europe, South Asia, Central America and Caribbean, etc.


```ruby

assert_equal 261, Factbook.codes.size

## categories
assert_equal 195, Factbook.codes.countries.size
assert_equal  52, Factbook.codes.dependencies.size
assert_equal   5, Factbook.codes.oceans.size
assert_equal   1, Factbook.codes.world.size
assert_equal   2, Factbook.codes.others.size
assert_equal   6, Factbook.codes.misc.size

## regions
assert_equal  55, Factbook.codes.europe.size
assert_equal   9, Factbook.codes.south_asia.size
assert_equal   6, Factbook.codes.central_asia.size
assert_equal  22, Factbook.codes.east_n_souteast_asia.size
assert_equal  19, Factbook.codes.middle_east.size
assert_equal  56, Factbook.codes.africa.size
assert_equal   7, Factbook.codes.north_america.size
assert_equal  33, Factbook.codes.central_america_n_caribbean.size
assert_equal  14, Factbook.codes.south_america.size
assert_equal  30, Factbook.codes.australia_oceania.size
assert_equal   4, Factbook.codes.antartica.size
assert_equal   5, Factbook.codes.region('Oceans').size
assert_equal   1, Factbook.codes.region('World').size

## categories + regions
assert_equal  45, Factbook.codes.countries.europe.size
...
```

See [`data/codes.csv`](data/codes.csv) for the built-in listing of all codes with categories and regions.




## Ready-To-Use Public Domain (Free) Factbook Datasets

[factbook/factbook.json](https://github.com/factbook/factbook.json) - open (public domain)
factbook country profiles in JSON for all the world's countries (note: using the original
/ official two-letter GEC (formerly FIPS) codes and NOT the ISO codes - you might be used to for country codes e.g. Austria is `au.json` and NOT `at.json`,
Germany is `gm.json` and NOT `de.json` so on)



## Install

Use

    gem install factbook-readers

or add to your Gemfile

    gem 'factbook-readers'



## License

The `factbook` scripts are dedicated to the public domain.
Use it as you please with no restrictions whatsoever.


## Questions? Comments?

Send them along to the [Open Mundi (world.db) Database Forum/Mailing List](http://groups.google.com/group/openmundi).
Thanks!
