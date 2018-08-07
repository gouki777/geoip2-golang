# GeoIP2 Reader for Go #


## Installation ##

```
go get -v -u -x github.com/oschwald/geoip2-golang
```

## Usage ##

[See GoDoc](http://godoc.org/github.com/oschwald/geoip2-golang) for
documentation and examples.

## download ##
```
下载geoip-db地址：http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz  
解压到本地目录

```
## Example ##

```go
package main

import (
    "fmt"
    "github.com/oschwald/geoip2-golang"
    "log"
    "net"
)

func main() {
    db, err := geoip2.Open("./GeoLite2-City_20180703/GeoLite2-City.mmdb")
    if err != nil {
            log.Fatal(err)
    }
    defer db.Close()
    // If you are using strings that may be invalid, check that ip is not nil
    ip := net.ParseIP("81.2.69.142")
    record, err := db.City(ip)
    if err != nil {
            log.Fatal(err)
    }
    fmt.Printf("Portuguese (BR) city name: %v\n", record.City.Names["pt-BR"])
    fmt.Printf("English subdivision name: %v\n", record.Subdivisions[0].Names["en"])
    fmt.Printf("Russian country name: %v\n", record.Country.Names["ru"])
    fmt.Printf("ISO country code: %v\n", record.Country.IsoCode)
    fmt.Printf("Time zone: %v\n", record.Location.TimeZone)
    fmt.Printf("Coordinates: %v, %v\n", record.Location.Latitude, record.Location.Longitude)
    // Output:
    // Portuguese (BR) city name: Londres
    // English subdivision name: England
    // Russian country name: Великобритания
    // ISO country code: GB
    // Time zone: Europe/London
    // Coordinates: 51.5142, -0.0931
}
```

## Testing ##

Make sure you checked out test data submodule:

```
git submodule init
git submodule update
```

Execute test suite:

```
[root@localhost ~]# go run ip.go 
Portuguese (BR) city name: 杭州
English subdivision name: Zhejiang
Russian country name: China
ISO country code: CN
Time zone: Asia/Shanghai
Coordinates: 30.2936, 120.1614
```

## Contributing ##

Contributions welcome! Please fork the repository and open a pull request
with your changes.

## License ##

This is free software, licensed under the ISC license.
