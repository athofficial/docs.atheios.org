# The portal

The portal offers a REST API. Aim of this API is to provide data about some of 
the properties managed by the  portal. Thise are:

* Games related data
* Games statistic related data

The REST API supports currently the following calls:

* https://portal.atheios.org/rest 
* https://portal.atheios.org/rest/games
* https://portal.atheios.org/rest/stats

## /rest
Returns a json with supported rest functions
```
bla
```  

## /rest/stats
### Description
Returns a json with statistics
### Return
```
{
  "nrofgameassets": 11,
  "nrofgamesnotready": 8,
  "scheme_50": 0,
  "scheme_60": 0,
  "scheme_70": 0,
  "scheme_80": 3,
  "scheme_90": 0,
  "scheme_100": 0,
  "periode_1": 0,
  "periode_3": 0,
  "periode_6": 0,
  "periode_12": 0,
  "periode_24": 0,
  "periode_48": 0,
  "periode_72": 0,
  "periode_96": 0,
  "periode_148": 3,
  "periode_296": 0,
  "wage_1": 2,
  "wage_5": 0,
  "wage_10": 0,
  "wage_25": 0,
  "wage_50": 0,
  "wage_100": 0,
  "nrofgameplays": 184
}
```  
### Syntax


