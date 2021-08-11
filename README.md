
# Radial Beam Span Tables API

Radial is developing a beam span tables API hosted on AWS to allow integration across different platforms in the design process (i.e. using Grasshopper).

The API exposes a single GET endpoint at: https://api.radialapp.com/get-lvl13, for the time being for the use with LVL13 beams. This will be expanded to all beam types taken from Cantilever's span tables in the future, with a separate GET endpoint for each beam type.

## Query parameters (Inputs)
The API expects query parameters to be appended to the url string. The required parameters depend on the type of beam being calculated.

### Rafters
1. beamType=rafters 
2. span= rafter span in mm
3. spacing = rafter spacing in mm

example url: https://api.radialapp.com/get-lvl13?beamType=rafters&spacing=600&span=4000


### Joists
1. beamType=joists
2. span= joist span in mm
3. spacing = joist spacing in mm

example url: https://api.radialapp.com/get-lvl13?beamType=joists&spacing=450&span=4000

## Headers
The API is protected by an API key which must be included in the request header as follows:

x-api-key: "YOUR_API_KEY_HERE"

Please get in touch with Radial to obtain a valid key.


## Response (Outputs)

The response is a JSON object of the following form:

```yaml
{
    "LVL": "150x45"
}
```

## Example Usage (Python)

```python
import rhinoscriptsyntax as rs
import urllib2
import json

 

def requestLvl(beamType, spacing, span):
    request = urllib2.Request("https://43srautc24.execute-api.ap-southeast-2.amazonaws.com/teststage/get-lvl13?beamType={0}&spacing={1}&span={2}".format(beamType, spacing, span))
    request.add_header("Content-type", "application/json")
    request.add_header("x-api-key", "qD3XZnW5TSJ4EZ9lBJvP2B57GI6GUD8kU5AsfKb0")
    response = urllib2.urlopen(request)
    resJSON = json.load(response)
    return(resJSON['LVL'])

print(requestLvl("joists", 450, 2000))

```

## TODOS
- [ ] Bearers
- [ ] Lintels
- [ ] Ridge/intermediate roof beam
- [ ] Verandah beam
- [ ] Hip rafter
- [ ] Underpurlin
- [ ] Hanging beam
- [ ] Counter beam
- [ ] Strutting beam
- [ ] Ceiling joist
- [x] Rafters @ 600ctrs with ceiling attached 
- [ ] Rafters @ 900ctrs with ceiling attached 
- [ ] Joists @ 300ctrs
- [x] Joists @ 450ctrs
- [ ] Joists @ 900ctrs

## License
[MIT](https://choosealicense.com/licenses/mit/)
