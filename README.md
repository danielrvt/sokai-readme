Sokai Sushi Plugin
=====

### This plugin contains web services for an electronic menu platform addressed to Sokai Sushi restaurant

##### Headers
The following headers must be used in the invokation of each of the services that are contained within the plugin

|      Header      |        Value       |
| ---------------- | ------------------ |
| Content-Type     | application/json   |
| Accept-Language  | en                 |

   
The documentation of the web services are detailed below:

### GET /api/users

Gets the list of all users (username and password pairs)

###### Response (HTTP status 200)
Array of:

|   Parameter   |     Type    |              Description             |   Required   |
| --------------| ------------|--------------------------------------|--------------|
| username      | String      | User id for the application          | Required     |
| password      | String      | User password for the application    | Required     |

**Example:**
```javascript
[
  {
    "username": "Jhon",
    "password": "1111"
  },
  {
    "username": "Daniel",
    "password": "daniel"
  }
]
```

###### Response Error Messages
| HTTP status code |            Message           |                     Comments                     |
| -----------------| -----------------------------| -------------------------------------------------|
| 404              | Custom object X not found    | Where X is the custom object type name for users |

**Example:**
```javascript
{
  "message": "Custom object User not found"
}
```


### GET /api/categories

Gets the list of categories with their dishes

###### Parameters

|  Parameter   | SubParameter |     Type     |       Description     | Required   |
| -------------| -------------|--------------|-----------------------|------------|
| id           |              | String       | Category id           | Required   |
| title        |              | String       | Category title        | Required   |
| description  |              | String       | Category description  | Required   |
| image        |              | String       | Category image id     | Required   |
| dishes       |              | Array of     | Category dishes       | Required   |
|              | id           | String       | Dish id               | Required   |
|              | name         | String       | Dish name             | Required   |
|              | description  | String       | Dish description      | Required   |
|              | price        | String       | Dish price            | Required   |
|              | images       | String Array | Dish images ids       | Required   |

**Example:**
```javascript
[
  {
    "id": "category1",
    "title": "category title",
    "description": "this is the category description",
    "image": "category1",
    "dishes": [
      {
        "id": "dish-1-c1",
        "name": "dish name",
        "description": "this is the dish description",
        "price": 134,
        "images": [
          "dish-1-c1-1",
          "disg-1-c1-2"
        ]
      }
    ]
  },
  {
    "id": "category2",
    "title": "title",
    "description": "this is the category description",
    "image": "category2",
    "dishes": [
      {
        "id": "dish-1-c2",
        "name": "dish name ",
        "description": "this is the dish description",
        "price": 123.4,
        "images": [
          "dish-1-c2-1"
        ]
      }
    ]
  }
]
```

###### Response Error Messages
| HTTP status code |            Message           |                      Comments                         |
| -----------------| -----------------------------| ------------------------------------------------------|
| 404              | Custom object X not found    | Where X is the custom object type name for categories |

**Example:**
```javascript
{
  "message": "Custom object Category not found"
}
```

### GET /api/images/:type

Gets the list of images locations of the categories or dishes

###### Response (HTTP status 200)
Array of:

|  Parameter   |     Type    |                Description             |   Required   |
| -------------| ------------|----------------------------------------|--------------|
| type         | String      | Type of images to get (path parameter) | Required     |
| id           | String      | Image id (name of media)               | Required     |
| image        | String      | URL location of the image              | Required     |

**Example:**
```javascript
[
  {
    "id": "category1",
    "image": "http://hostname.test/images.jpg"
  },
  {
    "id": "category2",
    "image": "http://occ-sokai-cms.herokuapp.com/media/2015/7/e819c1b1-3856-4ee9-95eb-bdd6bfa0d609-1436419360219.jpg"
  }
]
```

###### Response Error Messages
| HTTP status code |            Message           |                     Comments                    |
| -----------------| -----------------------------| ------------------------------------------------|
| 400              | type is invalid              | Type parameter should be category or dish topic |

**Example:**
```javascript
{
  "message": "type is invalid"
}
```


  
### GET /api/images/content/:type

Gets the list of images of the categories or dishes

###### Response (HTTP status 200)
Array of:

|  Parameter   |     Type    |                Description             |   Required   |
| -------------| ------------|----------------------------------------|--------------|
| type         | String      | Type of images to get (path parameter) | Required     |
| id           | String      | Image id (name of media)               | Required     |
| image        | String      | base64 string of the image content     | Required     |

**Example:**
```javascript
[
  {
    "id": "dish1",
    "image": "eHh4eHhhMTFoZTFpMnVlaHFpdWRvbHUxMmUyZQ=="
  }
]
```

###### Response Error Messages
| HTTP status code |            Message           |                     Comments                    |
| -----------------| -----------------------------| ------------------------------------------------|
| 400              | type is invalid              | Type parameter should be category or dish topic |

**Example:**
```javascript
{
  "message": "type is invalid"
}
```


### POST /api/questions/:id/answers

Saves an answer to the *id* question

###### Parameters
|   Parameter   |     Type     |         Description          |   Required   |
| --------------| -------------|------------------------------|--------------|
| id            | String       | Question id (path parameter) | Required     |
| score         | Numeric      | Score of the answer          | Required     |
| comment       | String       | Comment of the answer        | Optional     |

**Example:**
```javascript
{
    "score": "5",
    "comment": "comment"
}
```
###### Response (HTTP status 200)
**Example:**
```javascript
{
  "message": "Answer saved and question1 updated"
}
```

###### Response Messages
| HTTP status code |                 Message               |                             Comments                            |
| -----------------| --------------------------------------| ----------------------------------------------------------------|
| 400              | Invalid json                          |                                                                 |
| 400              | score is required                     |                                                                 |
| 400              | score is invalid                      |                                                                 |
| 400              | Error saving X                        | Where X is the custom object type name for questions or answers |                                                                    |
| 404              | Custom object X not found             | Where X is the custom object type name for questions or answers |
| 404              | X from custom object type Y not found | Where X is a question id and Y is the custom object type name for questions |                                   |

**Example:**
```javascript
{
  "message": "question31 from custom object type Question not found"
}
```

### POST /api/contacts

Saves contact messages

###### Parameters
|   Parameter   |     Type     |                Description              |   Required   |
| --------------| -------------|-----------------------------------------|--------------|
| name          | String       | Name of the person sending the message  | Required     |
| email         | String       | Email of the person sending the message | Required     |
| message       | String       | Contact message                         | Required     |

**Example:**
```javascript
{
    "name": "James",
    "email": "test@test.com",
    "message": "contact message"
}
```
###### Response (HTTP status 200)
**Example:**
```javascript
{
  "message": "ContactMessage saved"
}
```
###### Response Messages
| HTTP status code |                 Message          |                          Comments                           |
| -----------------| ---------------------------------| ------------------------------------------------------------|
| 400              | Invalid json                     |                                                             |
| 400              | X is required                    | Where X is the name of the missing field                    |
| 400              | email is invalid                 |                                                             |
| 400              | Error saving X                   | Where X is the custom object type name for contact messages |
| 404              | Custom object X not found        | Where X is the custom object type name for contact messages |

**Example:**
```javascript
{
  "message": "Invalid json"
}
```


