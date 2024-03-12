# API_Reqres_Testing

Hi! this is the documentation created by myself for the API Reqres.in. Here you'll find the documentation for each endpoint as well as the test cases and the code for the automation test using Postman.

__Base Url:__ `https://reqres.in`




## Endpoint: List Users
### URL: `/api/users?page={number}`
### Method: `GET`

### Description:
This point retrieves a paged list of users. You can specify the page number in the request to get a specific user page.

### Query Parameters: 

* __Page:__ (optional): An integer that specifies the page of results to obtain.

### Successful Request: 

* __Code__: `200 ok`
* __Content__: A JSON object that contains the following information:
    * __`page:` (int)__ The number of the current page.
    * __`per_page:` (int)__ The number of users per page.
    * __`total:` (int)__ The total of users avaible. 
    * __`total_pages:` (int)__ the total pages available in the api.
    * __`data:` (array)__ An array of users, where each user contains:
        * __`id:` (int)__ The unique ID of the user. 
        * __`email:` (string)__ The user's email. 
        * __`first_name:` (string)__ First name of the user. 
        * __`last_name:` (string)__ Last name of the user. 
        * __`avatar:` (string)__ The URL of the user's avatar.
    * __`support:` (object)__ An object that contains the URL for contribute with the reqres.in proyect: 
        * __`url:` (string)__ url for the support page for the reqres proyect. 
        * __`text:` (string)__ a basic description for why support the proyect.

### Example of response: 

```
{
    "page": 2,
    "per_page": 2,
    "total": 12,
    "total_pages": 2,
    "data": [
    {
        "id": 7,
        "email": "michael.lawson@reqres.in",
        "first_name": "Michael",
        "last_name": "Lawson",
        "avatar": "https://reqres.in/img/faces/7-image.jpg"
    },
    // ... more users
  ],
  "support": {
        "url": "https://reqres.in/#support-heading",
        "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
    }
}
```

### Examples of code for call the endpoint:

* __curl:__
```
curl -X GET "https://reqres.in/api/users?page=2"
```

* __javascript (Fetch):__
```
async function fetchUsers(page) {
  try {
    const response = await fetch(`https://reqres.in/api/users?page=${page}`);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchUsers(2); // Calls the funtion with the page number you want.
```

* __Python (Requests):__
```
import requests

response = requests.get("https://reqres.in/api/users?page=2")
data = response.json()
print(data)
```

### Errors: 

* __Code:__ `200 ok` 
* __Content:__

    ```
    {
        "page": 8,
        "per_page": 6,
        "total": 12,
        "total_pages": 2,
        "data": [],
        "support": {
            "url": "https://reqres.in/#support-heading",
            "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
        }
    }
    ```

* __Description:__ This "Error" is actually an expected behavior, API will only return the data shown above. 


## Endpoint: Single User

### URL: `/api/users/{id}`

### Method: `GET`

### Description:
Retrieve detailed information of a single user by using their unique ID.

### Query Parameters:
`id` (int): The unique ID of the user.

### Successful Request: 
* __`Code:`__ 200 ok status
* __`Content:` (Obj)__ A JSON object that contains the following information:
    * __`data:`__ A Object that contains the following information:
        * __`id:` (int)__ The unique ID number for the user.
        * __`email:` (string)__ User's email address.
        * __`first_name:`(string)__ User's first name.
        * __`last_name:`(string)__ User's last name.
        * __`avatar:`(string)__ Url to the User's avatar image.
        * __`support:` (object)__ An object that contains the URL for contribute with the reqres.in proyect: 
            * __`url:` (string)__ url for the support page for the reqres proyect. 
            * __`text:` (string)__ a basic description for why support the proyect.

### Example of response: 

```
{
    "data": {
        "id": 2,
        "email": "janet.weaver@reqres.in",
        "first_name": "Janet",
        "last_name": "Weaver",
        "avatar": "https://reqres.in/img/faces/2-image.jpg"
    },
    "support": {
        "url": "https://reqres.in/#support-heading",
        "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
    }
}
```

### Examples of code for call the endpoint:

* __curl:__
```
curl -X GET "https://reqres.in/api/users/2"
```

* __javascript (Fetch):__
```
async function fetchSingleUser(userId) {
  try {
    const response = await fetch(`https://reqres.in/api/users/${userId}`);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchSingleUser(2); // Calls the function with the number of the user you want.

```

* __Python (Requests):__
```
import requests

response = requests.get("https://reqres.in/api/users/2")
data = response.json()
print(data)
```

### Errors: 

* __Code:__ `404 not found` 
* __Content:__

    ```
    {}
    ```

* __Description:__ This error is returned when a non-existing user is selected, and empty object will be returned with a 404 status.



## Endpoint: Single User Not Found

### URL: `/api/users/{id}`

### Method: `GET`

### Description: 
When a request is done to a inexisting user ID, the API returns an empty objet with a 404 error message. 

### Query Parameters:
`id` (integer): a user ID that does not exist in the database. 

### Example of response: 
* __code:__ `404 not found`
* __content:__ 
```
  {}
```

### Examples of code for call the endpoint:

* __Curl:__ 

```
curl -X GET "https://reqres.in/api/users/23" -H "accept: application/json"

```

* __Javascript:__
```
async function getUser() {
  try {
    const response = await fetch("https://reqres.in/api/users/23");
    if (!response.ok) {
      throw new Error('User not found');
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

getUser();
```

* __Python:__ 
```
import requests

response = requests.get("https://reqres.in/api/users/23")

if response.status_code == 404:
    print("User not found")
else:
    user = response.json()
    print(user)
```

### Errors: 

* __Code:__ 404
* __Content:__
```
  {}
```
This status code is expected when the ID is invalid, and the API will return an empty object.


## List Resource

### URL: `/api/unknown?page={number}`

### Method: `GET`

### Description: 
This endpoints returns a list of different colors with their ID, name, Hexadecimal code and the panton code (world standar for the color code).

### Query Parameters:
* __`page`__ (optional): by default each page has 6 different colors, in total there are 2 pages.

### Successfull Request: 

* __`Code:`__  200 OK
* __`Content:`__ A JSON object that contains the following information:
  * __`page:`__ (int) The current page number.
  * __`per_page:`__ (int) The number of items per page.
  * __`total:`__ (int) The total number of items.
  * __`total_pages`:__ (int) The total number of pages.
  * __`data:`__ (array) An array of objects where each object contains information about a resource:
    * __`id:`__ (int) The unique ID number for the resource.
    * __`name:`__ (string) The name of the resource.
    * __`year:`__ (int) The year of the resource.
    * __`color:`__ (string) The color associated with the resource.
    * __`pantone_value:`__ (string) The pantone value of the resource.


### Example of response: 
```
{
    "page": 1,
    "per_page": 6,
    "total": 12,
    "total_pages": 2,
    "data": [
        {
            "id": 1,
            "name": "cerulean",
            "year": 2000,
            "color": "#98B2D1",
            "pantone_value": "15-4020"
        },
        // ... other resource objects
    ],
    "support": {
            "url": "https://reqres.in/#support-heading",
            "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
        }
}
```


### Examples of code for call the endpoint:

* __Curl:__
```
curl -X GET "https://reqres.in/api/unknown" -H "accept: application/json"
```

* __Javascript:__
```
  async function getResourceList() {
    try {
      const response = await fetch("https://reqres.in/api/unknown?page=1");

      if (!response.ok) {
        throw new Error('Network response was not ok');
      }

      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error('Error:', error);
    }
  }

  getResourceList();
```

* __python:__
```
import requests

response = requests.get("https://reqres.in/api/unknown?page=1")

if response.status_code == 200:
    data = response.json()

    print(data)
else:
    print("Error fetching the resources")
```

### Errors: 

* __Code:__ `200 ok` 
* __Content:__

```
{
    "page": 987,
    "per_page": 6,
    "total": 12,
    "total_pages": 2,
    "data": [],
    "support": {
        "url": "https://reqres.in/#support-heading",
        "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
    }
}
```

* __Description:__ This "Error" is actually an expected behavior, API will only return the data shown above when and non-existing page number is selected. 



## Single Resource

### URL
`/api/unknown/{id}`

### Method
`GET`

### Description
Retrieves information about a specific resource by its ID.

### Query Parameters
`id` unique ID of the resource. 

### Successful Request
- __Code:__ `200 OK`
- __Content:__ A JSON object that includes details about the resource and support information.
  - `data`: (object) Contains details about the resource:
    - `id`: (int) The unique identifier for the resource.
    - `name`: (string) The name of the resource.
    - `year`: (int) The year associated with the resource.
    - `color`: (string) The color representation of the resource.
    - `pantone_value`: (string) The pantone value linked to the resource.
  - `support`: (object) Contains support information for the reqres project:
    - `url`: (string) The URL to the support page for the reqres project.
    - `text`: (string) A short description of why to support the project.

### Example of Response
```
{
  "data": {
    "id": 2,
    "name": "fuchsia rose",
    "year": 2001,
    "color": "#C74375",
    "pantone_value": "17-2031"
  },
  "support": {
    "url": "https://reqres.in/#support-heading",
    "text": "To keep ReqRes free, contributions towards server costs are appreciated!"
  }
}
```

### Examples of code for call the endpoint:

* __Curl:__
```
curl -X GET "https://reqres.in/api/unknown/2" -H "accept: application/json"
```

* __Javascript:__
```
async function getSingleResource() {
  try {
    const response = await fetch("https://reqres.in/api/unknown/2");

    if (!response.ok) {
      throw new Error('Network response was not ok: ' + response.statusText);
    }

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

getSingleResource();
```

* __Python:__
```
import requests

response = requests.get("https://reqres.in/api/unknown/2")

if response.status_code == 200:
    data = response.json()

    print(data)
else:
    print('Error:', response.status_code, response.text)
```

### Errors: 

* __Code:__ `404 Not Found` 
* __Content:__

```
{}
```

* __Description:__ The API will return a 404 error when a non-existing ID is requested, also it will return an empty object.

