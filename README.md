# GeoNuclearData

This repository contains a database with information about Nuclear Power Plants worldwide.

### Version
Database version: **0.17.0** (**2020/04/19**)  
Dataset last updated in version: **0.17.1** (**2020/06/06**)

### Data formats

Data is available in multiple formats (MySQL, JSON, and CSV).

### Quick database summary (by reactor status)

|**Status**            |**Count**|
|----------------------|--------:|
|Unknown               |        1|
|Planned               |       88|
|Under Construction    |       54|
|Operational           |      441|
|Shutdown              |      188|
|Suspended Construction|        2|
|Cancelled Construction|        2|
|**Total**             |  **776**|

## Tables structure

### countries
- `code` - ISO 3166-1 alpha-2 country code
- `name` - country name in English
 
### nuclear_power_plant_status_type
- `id` - numeric id key
- `type` - nuclear power plant status

### nuclear_reactor_type
- `id` - numeric id key
- `type` - nuclear reactor type acronym
- `description` - nuclear reactor type long form
 
### nuclear_power_plants
- `id` - numeric id key
- `name` - nuclear power plant name
- `latitude` - latitude in decimal format
- `longitude` - longitude in decimal format
- `country_code` - ISO 3166-1 alpha-2 country code
- `status_id` - nuclear power plant status id
- `reactor_type_id` - nuclear reactor type id
- `reactor_model` - nuclear reactor model
- `construction_start_at` - date when nuclear power plant construction was started
- `operational_from` - date when nuclear power plant became operational (also known as commercial operation date)
- `operational_to` - date when nuclear power plant was shutdown (also known as permanent shutdown date)
- `capacity` - nuclear power plant capacity (design net capacity in MWe)
- `source` - source of the information
- `last_updated_at` - date and time when information was last updated
- `iaea_id` - IAEA PRIS reactor id
 
## Notes
Data from `source`, `last_updated_at`, and `iaea_id` columns is for maintenance purposes only and is not recommended to be used.
 
## Usage
    SELECT npp.`id`
        , npp.`name`
        , npp.latitude
        , npp.longitude
        , c.`name` 'country'
        , s.type 'status'
        , r.type 'reactor_type'
        , npp.reactor_model
        , npp.construction_start_at
        , npp.operational_from
        , npp.operational_to
    FROM nuclear_power_plants npp
    INNER JOIN countries AS c ON npp.country_code = c.`code`
    INNER JOIN nuclear_power_plant_status_type AS s ON npp.status_id = s.id
    LEFT OUTER JOIN nuclear_reactor_type AS r ON npp.reactor_type_id = r.id
    ORDER BY npp.`id`

## License
The GeoNuclearData database is made available under the Open Database License whose full text can be found at https://opendatacommons.org/licenses/odbl/1.0/.
 
Any rights in individual contents of the database are licensed under the Database Contents License whose full text can be found at https://opendatacommons.org/licenses/dbcl/1.0/.
 
## Sources
Countries data is taken from [Unicode Common Locale Data Repository](https://github.com/unicode-cldr/cldr-localenames-full/blob/master/main/en/territories.json).

Nuclear power plants data is taken from [WNA](http://www.world-nuclear.org/information-library/facts-and-figures/reactor-database.aspx)/[IAEA](https://www.iaea.org/pris/), but some other sources are used, e.g., [Wikipedia](https://en.wikipedia.org/wiki/List_of_nuclear_power_stations).
 
## Showcase
- [uRADMonitor - Global Environmental Monitoring Network](http://www.uradmonitor.com).
