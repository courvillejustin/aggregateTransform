# aggregateransform

A Node.js module for converting arrays of objects into aggregated, complex objects.


## Install
```
$ npm install --save aggregatetransform
```

## Example use
```js
var t = require('aggregateTransform');

var template = {
  "{{accountNumber}}": {
    'revenueYearMonth': {
      '{{revenueYearMonth}}': {
        'utilities': {
          '{{utilityCode}}': {
            'sockets': {
              '{{serviceId}}': {
                'meters': {
                  '{{meter}}': {
                    'startDate': '{{startDate}}',
                    'endDate': '{{endDate}}',
                    'rate': '{{rate}}',
                    'utility': '{{utilityCode}}',
                    'account': '{{accountNumber}}',
                    'billPeriod': '{{revenueYearMonth}}',
                    'lineItems': {
                      '{{typeCode}}': {
                        'codes': {
                          '{{adjustmentCode}}': ['{{amount}}']
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
};

var obj = {};
var data = require('./input.js');

data.forEach(function (row) {
  t.transform(template, row, obj);
});

console.log(obj);
```

## Result:

```js
{
  "1000002": {
    "revenueYearMonth": {
      "201411": {
        "utilities": {
          "E": {
            "sockets": {
              "1393": {
                "meters": {
                  "ME65374": {
                    "startDate": "20141013",
                    "endDate": "20141112",
                    "rate": "E110",
                    "utility": "E",
                    "account": "1000002",
                    "billPeriod": "201411",
                    "lineItems": {
                      "R": {
                        "codes": {
                          "000088676": ["0", "9.25"]
                        }
                      },
                      "@": {
                        "codes": {
                          "DDMD1": ["80.86"],
                          "DIST3": ["20.16"]
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "100METER000009": {
    "revenueYearMonth": {
      "201411": {
        "utilities": {
          "E": {
            "sockets": {
              "5678": {
                "meters": {
                  "METER000009": {
                    "startDate": "20141007",
                    "endDate": "20141106",
                    "rate": "E110",
                    "utility": "E",
                    "account": "100METER000009",
                    "billPeriod": "201411",
                    "lineItems": {
                      "R": {
                        "codes": {
                          "000088676": ["0", "9.25"]
                        }
                      },
                      "@": {
                        "codes": {
                          "DDMD1": ["36.67"],
                          "DIST3": ["5.28"],
                          "EGSD2": ["5.75"],
                          "EGSP2": ["13.15", "52.97"],
                          "GCTC2": ["3.56"],
                          "TDMD2": ["17.99"],
                          "USBC6": ["1.22"]
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}

```
