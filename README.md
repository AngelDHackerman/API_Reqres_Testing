# API_Reqres_Testing

Hi! this is the documentation created by myself for the API Reqres.in. Here you'll find the documentation for each endpoint as well as the test cases and the code for the automation test using Postman.

__Base Url:__ `https://reqres.in`




## Endpoint: List Users
### URL: `/api/users?page={number}`
### Method: `GET`

__Description:__ This point retrieves a paged list of users. You can specify the page number in the request to get a specific user page.

### Query Parameters: 

* __Page:__ (optional): An integer that specifies the page of results to obtain.

### Successful Request: 

* __Code__: `200 ok`
* __Content__: A JSON object that contains the following information:
    * __`page`__: The number of the current page.
    * __`per_page`__: The number of users per page.
    * __`total`__: The total of users avaible. 
    * __`data`__: An array of users, where each user contains:
        * __`id`__: The unique ID of the user. 
        * __`email`__: The user's email. 
        * __`first_name`__: First name of the user. 
        * __`last_name`__: Last name of the user. 
        * __`avatar`__: The URL of the user's avatar.
    * __`support`__: An object that contains the URL for contribute with the reqres.in proyect: 
        * __`url`__: url for the support page for the reqres proyect. 
        * __`text`__: a basic description for why support the proyect.

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

* Code: `200 ok` 
* Content:

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

* Description: This "Error" is returned when a non-existing page is selected. 