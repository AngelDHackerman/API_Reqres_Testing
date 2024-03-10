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

### Errors: 

* __Code:__ `404 not found` 
* __Content:__

    ```
    {}
    ```

* __Description:__ This error is returned when a non-existing user is selected, and empty object will be returned with a 404 status.