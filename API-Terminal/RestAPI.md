# REST API

***REST***: Representational state transfer.

***API*** Application program interface.

Set of rules to follow for creating APIs to get data from a server/resource

## Anatomy of REST request:
    1. Endpoint
    2. Method
    3. Headers
    4. Data/Body

### Imp things:

1. Endpoint -> The URL to get the data `https://api.github.com/users/rameshnavi/repos`
    Endpoint root. `api.github.com`
    Endpoint root `/users/rameshnavi/repos`
    Query parameters `val1=1&val2=2`

2. Testing endpoints with CURL
	Version-> `$curl --version`	
    Call -> `$curl https://api.github.com`

    escape sequences for `&` and `=` symbos -> `\?` and `\&`

    Option `-i` for detailed info

3. Json -> Javascript object notation
    Standerdised format for data tranfer through REST API

    eg: {
        "property1": "value1",
        "property2": "value2"
        ...
        }
4. Method -> Type of request
    GET -> reads the info
    POST -> Creates/Writes info
    PUT & PATCH -> updates info
    DELETE -> Deletes info.

    Option "X" to specify Method
        - No "X" then GET by default

    curl example: $curl -X POST https://api.github.com/users/repos
        -> error for no auth
    
5. Headers -> HTTP headers provide info about client and server or authorization info.

    Property value pairs in header:
    Eg: "Content-Type: application/json"

    curl eg: $curl -H "Content-Type: application/json" https://api.github.com
    in output ">" refers to request header and "<" refers to response headers.

6. Data / Body
    Option "-d" for data
    eg: $curl -X POST https://api.github.com/api/ -d property1=val1 \
        -d property2=val2 \
        -d propery3=val3

    eg: $ curl -X DELETE -H "Content-Type: application/json" https://requestb.in/prh1dspr -d '{"name":"ramesh",
        "fullname":"rameshnavi"
        }'

7. Authentication 2 types -> option "u"
    1. Basic authentication -> Username:Password
    2. Secret token -> oAuth

    1->
    Eg: $curl -X POST api.github.com/rameshnavi/repos

    curl -X DELETE -u rameshnavi:shssdsds -H "Content-Type: application/json" https://requestb.in/prh1dspr

    Base 64 decode will give rameshnavi:shssdsds back from Authorization parameters

8. Output
    Dump to file -> -D filename
