# Addresses

Address objects are often **nested into other objects** that you retrieve, e.g. locations or customers.

## The Address object

| Attribute    | Type |       |
| ------------- |:----:| -----|  
| `line1`          | string |  First address line, e.g. street and number |
| `line2`          | string |  Additional address line |
| `zip`          | string | Zip code |
| `city`          | string | City |
| `country`          | string |  Uppercase ISO country code: **DE** for germany |

```json
// example address
{
  "line1": "Danziger Str. 36",
  "line2": null,
  "zip": "20099",
  "city": "Hamburg",
  "country": "DE"
}
```