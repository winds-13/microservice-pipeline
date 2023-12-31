### Customer Operations

| Endpoint          | Methods | Rule
| ---------------   | ------- | --------------------------
| create_customers  | POST    | ```/customers```
| get_customers     | GET     | ```/customers/{int:customer_id}```
| update_customers  | PUT     | ```/customers/{int:customer_id}```
| delete_a_customer | DELETE  | ```/customers/{int:customer_id}```
| list_customers    | GET     | ```/customers```

## APIs Usage

### Create a Customer
URL : `http://127.0.0.1:8000/customers`

Method : POST

Auth required : No

Permissions required : No

Create a customer using a JSON file that includes the customers's name, address, email, phone_number and password.

Example:

Request Body (JSON)
```
{
  "name": "John Doe",
  "address": "5th Fifth Ave, NY",
  "email": "john@gmail.com",
  "phone_number": "12345678",
  "password": "password"
}


```

Success Response : `HTTP_200_CREATED`
```
[
  {
    "id":1,
    "name": "John Doe",
    "address": "5th Fifth Ave, NY",
    "email": "john@gmail.com",
    "phone_number": "12345678",
    "password": "password"
}
]
```

### Read a Customer 

URL : `http://127.0.0.1:8000/customers/{int:customer_id}`

Method : GET

Auth required : No

Permissions required : No

Read all information of a customer with given id

Example:

Success Response : `HTTP_200_OK`
```
[
  {
    "id":1,
    "name": "John Doe",
    "address": "5th Fifth Ave, NY",
    "email": "john@gmail.com",
    "phone_number": "12345678",
    "password": "password"
}
]
```

Failure Response : `HTTP_404_NOT_FOUND`
```
{
  "error": "Not Found",
  "message": "404 Not Found: Customer with id '3' was not found.",
  "status": 404
}

```

### Update a Customer 


URL : `http://127.0.0.1:8000/customers/{int:customer_id}`

Method : PUT

Auth required : No

Permissions required : No

Updates a customer with id provided in the URL according to the updated fields provided in the body

Example:

Request Body (JSON)
```
  {
    "name": "John Foo",
    "address": "5th Fifth Ave, NY",
    "email": "john@gmail.com",
    "phone_number": "12345678",
    "password": "password"
}
```


Success Response : `HTTP_200_OK`
```
[
  {
    "id":1,
    "name": "John Foo",
    "address": "5th Fifth Ave, NY",
    "email": "john@gmail.com",
    "phone_number": "12345678",
    "password": "password"
}
]

```

Failure Response : `HTTP_404_NOT_FOUND`
```
{
  "error": "Not Found",
  "message": "404 Not Found: Customer with id '2' was not found.",
  "status": 404
}

```

### Delete a Customer

URL : `http://127.0.0.1:8000/customers/{int:customer_id}`

Method : DELETE

Auth required : No

Permissions required : No

Deletes a Customer with id

Example:

Success Response : `204 NO CONTENT`


### List Customers

This is the planned version of listing customers. Currently the listing part still have some errors

URL : `http://127.0.0.1:8000/customers` 

Method: GET

Auth required : No

Permissions required : No

List All Customers

Example:

Success Response : `HTTP_200_OK`

```
[
  {
    "id":1,
    "name": "John Foo",
    "address": "5th Fifth Ave, NY",
    "email": "john@gmail.com",
    "phone_number": "12345678",
    "password": "password"
}
]
```

## Contents

The project contains the following:

```text
.gitignore          - this will ignore vagrant and other metadata files
.flaskenv           - Environment variables to configure Flask
.gitattributes      - File to gix Windows CRLF issues
.devcontainers/     - Folder with support for VSCode Remote Containers
dot-env-example     - copy to .env to use environment variables
requirements.txt    - list if Python libraries required by your code
config.py           - configuration parameters

service/                   - service python package
├── __init__.py            - package initializer
├── models.py              - module with business models
├── routes.py              - module with service routes
└── common                 - common code package
    ├── error_handlers.py  - HTTP error handling code
    ├── log_handlers.py    - logging setup code
    └── status.py          - HTTP status constants

tests/              - test cases package
├── __init__.py     - package initializer
├── test_models.py  - test suite for business models
└── test_routes.py  - test suite for service routes
```

## Running the service

The project uses *honcho* which gets it's commands from the `Procfile`. To start the service:

```shell
$ honcho start
```

You could reach the service at: http://localhost:8000 as defined in the `.flaskenv` file, which Flask uses to load it's configuration from the environment by default.

To test and check the coverage: 
```shell
$ green
```

Later this semester, github actions will be added to allow the auto testing. Currently we manually list the result: 

```
Name                               Stmts   Miss  Cover   Missing
----------------------------------------------------------------
service/__init__.py                   17      2    88%   31-32
service/common/cli_commands.py         7      0   100%
service/common/error_handlers.py      38      6    84%   77-79, 107-109
service/common/log_handlers.py        11      1    91%   35
service/common/status.py              45      0   100%
service/config.py                      5      0   100%
service/models.py                     59      0   100%
service/routes.py                     55      2    96%   117-118
----------------------------------------------------------------
TOTAL                                237     11    95%
```

Currently the listing api is still missing, once its work finishes, the pull request will be merged. Thus, the actual coverage of routes is expected to be higher.

