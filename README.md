![Test status](https://github.com/vinissimus/caddy-geoip/workflows/Test/badge.svg)

## Overview

**Caddy v2 compatible!**

`geoip` is a Caddy plugin that allow to determine
user Geolocation by IP address using a
[MaxMind database](https://www.maxmind.com/en/geoip2-services-and-databases).

## Placeholders

The following placeholders are available:

```
  geoip_country_code - Country ISO code, example CY for Cyprus
  geoip_country_geoname_id - GeoNameID of the city, example 146669
  geoip_latitude - Latitude, example 34.684100
  geoip_longitude - Longitude, example 33.037900
  geoip_time_zone - Time zone, example Asia/Nicosia
  geoip_country_eu - Return 'true' if country in Europen Union
  geoip_country_name - Full country name
  geoip_city_name - City name
  geoip_city_geoname_id - GeoNameID of the city, example 146384
  geoip_geohash - Geohash of latitude and longitude
```

## Missing geolocation data

If there is no geolocation data for an IP address most of the placeholders
listed above will be empty. The exceptions are `geoip_country_code`,
`geoip_country_name`, and `geoip_city_name`. If the request originated over
the system loopback interface (e.g., 127.0.0.1) those vars will be set
to `**`, `Loopback`, and `Loopback` respectively. For any other address,
including private addresses such as 192.168.0.1, the values will be `!!`,
`No Country`, and `No City` respectively.

## Examples

(1) Set database path and return country code header:

```
geoip /path/to/db/GeoLite2-City.mmdb
header Country-Code {geoip_country_code}
```

(2) Proxy pass headers to backend:

```
localhost
geoip /path/to/db/GeoLite2-City.mmdb
proxy / localhost:3000 {
  header_up Country-Name {geoip_country_name}
  header_up Country-Code {geoip_country_code}
  header_up Country-Eu {geoip_country_eu}
  header_up City-Name {geoip_city_name}
  header_up Latitude {geoip_latitude}
  header_up Longitude {geoip_longitude}
  header_up Time-Zone {geoip_time_zone}
  header_up Geohash {geoip_geohash}
}
```

## Contributing

1. [Fork it](https://github.com/vinissimus/caddy-geoip/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new [Pull Request](https://github.com/vinissimus/caddy-geoip/pulls)

## Contributors

- [aablinoov](https://github.com/aablinov) Andrey Blinov - creator, maintainer
- [masipcat](https://github.com/masipcat) Jordi Masip - contributor
