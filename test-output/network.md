```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-3xrjs9@email.com",
    "username": "author-3xrjs9",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-3xrjs9@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0zeHJqczkiLCJpYXQiOjE1MzM0MDUzNjgsImV4cCI6MTUzMzU3ODE2OH0.jgqeyQ1OaIdUb-XYY6xKmcHMO2tHewFar1BsE4j-y5A",
    "username": "author-3xrjs9",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-ev2nsw@email.com",
    "username": "authoress-ev2nsw",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-ev2nsw@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1ldjJuc3ciLCJpYXQiOjE1MzM0MDUzNjgsImV4cCI6MTUzMzU3ODE2OH0.g5W246utullpMohqYNthbZghju7nQnQSE2Xaag2q7jQ",
    "username": "authoress-ev2nsw",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-4ju1cq@email.com",
    "username": "non-author-4ju1cq",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-4ju1cq@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItNGp1MWNxIiwiaWF0IjoxNTMzNDA1MzY4LCJleHAiOjE1MzM1NzgxNjh9.u-rn5dlJ363bKefYwmHqK3wjNQWbt0HxFUU7jl1y4_c",
    "username": "non-author-4ju1cq",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-igtys9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405368346,
    "updatedAt": 1533405368346,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ube6zi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405368416,
    "updatedAt": 1533405368416,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-igtys9
```
```
200 OK

{
  "article": {
    "createdAt": 1533405368346,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-igtys9",
    "updatedAt": 1533405368346,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-ube6zi
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1533405368416,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-ube6zi",
    "updatedAt": 1533405368416,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/cpq176
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [cpq176]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-ube6zi

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1533405368416,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-ube6zi",
    "updatedAt": 1533405368416,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-ube6zi

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1533405368416,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-ube6zi",
    "updatedAt": 1533405368416,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-ube6zi

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1533405368416,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-ube6zi",
    "updatedAt": 1533405368416,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-ube6zi

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-ube6zi

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-ube6zi

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-ube6zi

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-ube6zi]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-ube6zi

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-3xrjs9]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-igtys9/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1533405368346,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-igtys9",
    "updatedAt": 1533405368346,
    "favoritedBy": [
      "non-author-4ju1cq"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-igtys9
```
```
200 OK

{
  "article": {
    "createdAt": 1533405368346,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-igtys9",
    "updatedAt": 1533405368346,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-igtys9/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-igtys9_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-igtys9_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-igtys9/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1533405368346,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-igtys9",
    "updatedAt": 1533405368346,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-igtys9
```
```
200 OK

{}
```
```
GET /articles/title-igtys9
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-igtys9]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-ube6zi
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-3xrjs9]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "k4j7zy",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xjfcxh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405370771,
    "updatedAt": 1533405370771,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "k4j7zy",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "i3atts",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7fin8r",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405370831,
    "updatedAt": 1533405370831,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "i3atts",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "we1g8l",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-524i4f",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405370884,
    "updatedAt": 1533405370884,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "we1g8l",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5o832f",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-g0ddfw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405370932,
    "updatedAt": 1533405370932,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5o832f",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "2gyzhh",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fitxi9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405370992,
    "updatedAt": 1533405370992,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "2gyzhh",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "288s9g",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mub85o",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371048,
    "updatedAt": 1533405371048,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "288s9g",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c3l6v7",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-m628b9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371120,
    "updatedAt": 1533405371120,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c3l6v7",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "qfu9tm",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-woc2rr",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371166,
    "updatedAt": 1533405371166,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "qfu9tm",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "g9jghg",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ufdj1e",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371202,
    "updatedAt": 1533405371202,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "g9jghg",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hwwex4",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tkywn2",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371250,
    "updatedAt": 1533405371250,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hwwex4",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "viig6g",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-84iemn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371294,
    "updatedAt": 1533405371294,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "viig6g",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "a6uxm6",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-t99nt3",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371349,
    "updatedAt": 1533405371349,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "a6uxm6",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "e97l64",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gr0hs4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371426,
    "updatedAt": 1533405371426,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "e97l64",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "seewtw",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2bcd4q",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371482,
    "updatedAt": 1533405371482,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "seewtw",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "1zgnup",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-h2vhsi",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371526,
    "updatedAt": 1533405371526,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "1zgnup",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "hfy08j",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-or58t4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371570,
    "updatedAt": 1533405371570,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "hfy08j",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7wszch",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7p34kn",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371713,
    "updatedAt": 1533405371713,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7wszch",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "fqlqdv",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-98fm5a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405371928,
    "updatedAt": 1533405371928,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "fqlqdv",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "cmtvv4",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-o7n02o",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405372141,
    "updatedAt": 1533405372141,
    "author": {
      "username": "authoress-ev2nsw",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "cmtvv4",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8iqbvn",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dk9iqk",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405372255,
    "updatedAt": 1533405372255,
    "author": {
      "username": "author-3xrjs9",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8iqbvn",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8iqbvn",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405372255,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dk9iqk",
      "updatedAt": 1533405372255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cmtvv4",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405372141,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o7n02o",
      "updatedAt": 1533405372141,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fqlqdv",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371928,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98fm5a",
      "updatedAt": 1533405371928,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7wszch",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371713,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7p34kn",
      "updatedAt": 1533405371713,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hfy08j",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371570,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-or58t4",
      "updatedAt": 1533405371570,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "seewtw",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371482,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2bcd4q",
      "updatedAt": 1533405371482,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "e97l64",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371426,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gr0hs4",
      "updatedAt": 1533405371426,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a6uxm6",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371349,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t99nt3",
      "updatedAt": 1533405371349,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "viig6g"
      ],
      "createdAt": 1533405371294,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-84iemn",
      "updatedAt": 1533405371294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hwwex4",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371250,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tkywn2",
      "updatedAt": 1533405371250,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfu9tm",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371166,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-woc2rr",
      "updatedAt": 1533405371166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c3l6v7",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371120,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m628b9",
      "updatedAt": 1533405371120,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "288s9g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371048,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mub85o",
      "updatedAt": 1533405371048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2gyzhh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370992,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fitxi9",
      "updatedAt": 1533405370992,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5o832f",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370932,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g0ddfw",
      "updatedAt": 1533405370932,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i3atts",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370831,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7fin8r",
      "updatedAt": 1533405370831,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k4j7zy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370771,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xjfcxh",
      "updatedAt": 1533405370771,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "qfu9tm",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371166,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-woc2rr",
      "updatedAt": 1533405371166,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "fqlqdv",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371928,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98fm5a",
      "updatedAt": 1533405371928,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a6uxm6",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371349,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t99nt3",
      "updatedAt": 1533405371349,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "288s9g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371048,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mub85o",
      "updatedAt": 1533405371048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-ev2nsw
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "cmtvv4",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405372141,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o7n02o",
      "updatedAt": 1533405372141,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7wszch",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371713,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7p34kn",
      "updatedAt": 1533405371713,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "e97l64",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371426,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gr0hs4",
      "updatedAt": 1533405371426,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "viig6g"
      ],
      "createdAt": 1533405371294,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-84iemn",
      "updatedAt": 1533405371294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c3l6v7",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371120,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m628b9",
      "updatedAt": 1533405371120,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2gyzhh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370992,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fitxi9",
      "updatedAt": 1533405370992,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k4j7zy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370771,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xjfcxh",
      "updatedAt": 1533405370771,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-4ju1cq
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-3xrjs9&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8iqbvn",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405372255,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dk9iqk",
      "updatedAt": 1533405372255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fqlqdv",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371928,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98fm5a",
      "updatedAt": 1533405371928,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-3xrjs9&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "hfy08j",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371570,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-or58t4",
      "updatedAt": 1533405371570,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "seewtw",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371482,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2bcd4q",
      "updatedAt": 1533405371482,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8iqbvn",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405372255,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dk9iqk",
      "updatedAt": 1533405372255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cmtvv4",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405372141,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o7n02o",
      "updatedAt": 1533405372141,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fqlqdv",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371928,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98fm5a",
      "updatedAt": 1533405371928,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7wszch",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371713,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7p34kn",
      "updatedAt": 1533405371713,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hfy08j",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371570,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-or58t4",
      "updatedAt": 1533405371570,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "seewtw",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371482,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2bcd4q",
      "updatedAt": 1533405371482,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "e97l64",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371426,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gr0hs4",
      "updatedAt": 1533405371426,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a6uxm6",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371349,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t99nt3",
      "updatedAt": 1533405371349,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "viig6g"
      ],
      "createdAt": 1533405371294,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-84iemn",
      "updatedAt": 1533405371294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hwwex4",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371250,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tkywn2",
      "updatedAt": 1533405371250,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfu9tm",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371166,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-woc2rr",
      "updatedAt": 1533405371166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c3l6v7",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371120,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m628b9",
      "updatedAt": 1533405371120,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "288s9g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371048,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mub85o",
      "updatedAt": 1533405371048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2gyzhh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370992,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fitxi9",
      "updatedAt": 1533405370992,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5o832f",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370932,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g0ddfw",
      "updatedAt": 1533405370932,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i3atts",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370831,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7fin8r",
      "updatedAt": 1533405370831,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k4j7zy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370771,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xjfcxh",
      "updatedAt": 1533405370771,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-ev2nsw/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-ev2nsw",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "cmtvv4",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405372141,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o7n02o",
      "updatedAt": 1533405372141,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7wszch",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371713,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7p34kn",
      "updatedAt": 1533405371713,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "e97l64",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371426,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gr0hs4",
      "updatedAt": 1533405371426,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "viig6g"
      ],
      "createdAt": 1533405371294,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-84iemn",
      "updatedAt": 1533405371294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c3l6v7",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371120,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m628b9",
      "updatedAt": 1533405371120,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2gyzhh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370992,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fitxi9",
      "updatedAt": 1533405370992,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k4j7zy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370771,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xjfcxh",
      "updatedAt": 1533405370771,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-3xrjs9/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-3xrjs9",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8iqbvn",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405372255,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dk9iqk",
      "updatedAt": 1533405372255,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "cmtvv4",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405372141,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-o7n02o",
      "updatedAt": 1533405372141,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "fqlqdv",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371928,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-98fm5a",
      "updatedAt": 1533405371928,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7wszch",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371713,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7p34kn",
      "updatedAt": 1533405371713,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hfy08j",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371570,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-or58t4",
      "updatedAt": 1533405371570,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "1zgnup",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371526,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-h2vhsi",
      "updatedAt": 1533405371526,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "seewtw",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371482,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2bcd4q",
      "updatedAt": 1533405371482,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "e97l64",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371426,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gr0hs4",
      "updatedAt": 1533405371426,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "a6uxm6",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371349,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-t99nt3",
      "updatedAt": 1533405371349,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "viig6g"
      ],
      "createdAt": 1533405371294,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-84iemn",
      "updatedAt": 1533405371294,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "hwwex4",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371250,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tkywn2",
      "updatedAt": 1533405371250,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "g9jghg",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371202,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ufdj1e",
      "updatedAt": 1533405371202,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "qfu9tm",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405371166,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-woc2rr",
      "updatedAt": 1533405371166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c3l6v7",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405371120,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m628b9",
      "updatedAt": 1533405371120,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "288s9g",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1533405371048,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mub85o",
      "updatedAt": 1533405371048,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "2gyzhh",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370992,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fitxi9",
      "updatedAt": 1533405370992,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5o832f",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370932,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g0ddfw",
      "updatedAt": 1533405370932,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "we1g8l"
      ],
      "createdAt": 1533405370884,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-524i4f",
      "updatedAt": 1533405370884,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i3atts",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1533405370831,
      "author": {
        "username": "author-3xrjs9",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7fin8r",
      "updatedAt": 1533405370831,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "k4j7zy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1533405370771,
      "author": {
        "username": "authoress-ev2nsw",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xjfcxh",
      "updatedAt": 1533405370771,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "1zgnup",
    "tag_14",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "a6uxm6",
    "tag_11",
    "tag_mod_2_1",
    "cmtvv4",
    "tag_18",
    "tag_mod_3_0",
    "qfu9tm",
    "tag_7",
    "tag_mod_3_1",
    "7wszch",
    "tag_16",
    "2gyzhh",
    "tag_4",
    "288s9g",
    "tag_5",
    "seewtw",
    "tag_13",
    "i3atts",
    "tag_1",
    "tag_2",
    "we1g8l",
    "c3l6v7",
    "tag_6",
    "g9jghg",
    "tag_8",
    "tag_10",
    "viig6g",
    "tag_a",
    "tag_b",
    "hfy08j",
    "tag_15",
    "hwwex4",
    "tag_9",
    "e97l64",
    "tag_12",
    "k4j7zy",
    "tag_0",
    "5o832f",
    "tag_3",
    "fqlqdv",
    "tag_17",
    "8iqbvn",
    "tag_19"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-sv41pv@email.com",
    "username": "author-sv41pv",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-sv41pv@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1zdjQxcHYiLCJpYXQiOjE1MzM0MDUzNzQsImV4cCI6MTUzMzU3ODE3NH0.zMvt83C8Bco-bLf5ffVSmRQ-pg41IidHyaEi1XCepvE",
    "username": "author-sv41pv",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-uwdyrt@email.com",
    "username": "commenter-uwdyrt",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-uwdyrt@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci11d2R5cnQiLCJpYXQiOjE1MzM0MDUzNzQsImV4cCI6MTUzMzU3ODE3NH0.9u2Rv9ytmGNiIsIU4J_enzENeV6_V2V5T5C_588NLxg",
    "username": "commenter-uwdyrt",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1fnk1u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1533405374284,
    "updatedAt": 1533405374284,
    "author": {
      "username": "author-sv41pv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 4e8fi"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f055fd95-a3bf-4f35-a693-c8f4dcc9e257",
    "slug": "title-1fnk1u",
    "body": "test comment 4e8fi",
    "createdAt": 1533405374330,
    "updatedAt": 1533405374330,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 7w25za"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "711e1f71-44dd-48c1-bac7-ed50cbb3a0ed",
    "slug": "title-1fnk1u",
    "body": "test comment 7w25za",
    "createdAt": 1533405374364,
    "updatedAt": 1533405374364,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 8xfetu"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2521c9da-2e66-479c-b2f7-7e1075df7a24",
    "slug": "title-1fnk1u",
    "body": "test comment 8xfetu",
    "createdAt": 1533405374398,
    "updatedAt": 1533405374398,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 1lzd5c"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "a117048d-35b2-4ce0-a6f9-69e2a77c233b",
    "slug": "title-1fnk1u",
    "body": "test comment 1lzd5c",
    "createdAt": 1533405374436,
    "updatedAt": 1533405374436,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment jt3xtq"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "241bc96f-0175-4720-a908-d05a606fd1c2",
    "slug": "title-1fnk1u",
    "body": "test comment jt3xtq",
    "createdAt": 1533405374487,
    "updatedAt": 1533405374487,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment b4w5v4"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "edf747c7-4f17-4841-8dbf-2c82052e0d76",
    "slug": "title-1fnk1u",
    "body": "test comment b4w5v4",
    "createdAt": 1533405374524,
    "updatedAt": 1533405374524,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 59tjsn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ea5be4b7-b3db-41d6-beff-03be13442eb8",
    "slug": "title-1fnk1u",
    "body": "test comment 59tjsn",
    "createdAt": 1533405374561,
    "updatedAt": 1533405374561,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment 6863pf"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "0899879c-e154-4a92-b56c-c5115dcd6782",
    "slug": "title-1fnk1u",
    "body": "test comment 6863pf",
    "createdAt": 1533405374605,
    "updatedAt": 1533405374605,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment ierhvb"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "db03dde2-c716-4a91-a81b-74b102f324ee",
    "slug": "title-1fnk1u",
    "body": "test comment ierhvb",
    "createdAt": 1533405374651,
    "updatedAt": 1533405374651,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-1fnk1u/comments

{
  "comment": {
    "body": "test comment jlxwuv"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "fc350284-2fdc-4ded-90a9-4ddb1b5e0f44",
    "slug": "title-1fnk1u",
    "body": "test comment jlxwuv",
    "createdAt": 1533405374703,
    "updatedAt": 1533405374703,
    "author": {
      "username": "commenter-uwdyrt",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-1fnk1u/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-1fnk1u/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment azykcd"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-1fnk1u/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1533405374398,
      "id": "2521c9da-2e66-479c-b2f7-7e1075df7a24",
      "body": "test comment 8xfetu",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374398
    },
    {
      "createdAt": 1533405374703,
      "id": "fc350284-2fdc-4ded-90a9-4ddb1b5e0f44",
      "body": "test comment jlxwuv",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374703
    },
    {
      "createdAt": 1533405374561,
      "id": "ea5be4b7-b3db-41d6-beff-03be13442eb8",
      "body": "test comment 59tjsn",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374561
    },
    {
      "createdAt": 1533405374330,
      "id": "f055fd95-a3bf-4f35-a693-c8f4dcc9e257",
      "body": "test comment 4e8fi",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374330
    },
    {
      "createdAt": 1533405374651,
      "id": "db03dde2-c716-4a91-a81b-74b102f324ee",
      "body": "test comment ierhvb",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374651
    },
    {
      "createdAt": 1533405374524,
      "id": "edf747c7-4f17-4841-8dbf-2c82052e0d76",
      "body": "test comment b4w5v4",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374524
    },
    {
      "createdAt": 1533405374436,
      "id": "a117048d-35b2-4ce0-a6f9-69e2a77c233b",
      "body": "test comment 1lzd5c",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374436
    },
    {
      "createdAt": 1533405374487,
      "id": "241bc96f-0175-4720-a908-d05a606fd1c2",
      "body": "test comment jt3xtq",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374487
    },
    {
      "createdAt": 1533405374364,
      "id": "711e1f71-44dd-48c1-bac7-ed50cbb3a0ed",
      "body": "test comment 7w25za",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374364
    },
    {
      "createdAt": 1533405374605,
      "id": "0899879c-e154-4a92-b56c-c5115dcd6782",
      "body": "test comment 6863pf",
      "slug": "title-1fnk1u",
      "author": {
        "username": "commenter-uwdyrt",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1533405374605
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-1fnk1u/comments/f055fd95-a3bf-4f35-a693-c8f4dcc9e257
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-1fnk1u/comments/711e1f71-44dd-48c1-bac7-ed50cbb3a0ed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-uwdyrt]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-1fnk1u/comments/711e1f71-44dd-48c1-bac7-ed50cbb3a0ed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-1fnk1u/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "username": "user1-0.co75htiiew",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA",
    "username": "user1-0.co75htiiew",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "username": "user1-0.co75htiiew",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.co75htiiew]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.co75htiiew@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.co75htiiew@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA",
    "username": "user1-0.co75htiiew",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.yq0imclqm8p",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.yq0imclqm8p]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "password": "0.x4u0coqw71k"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.co75htiiew@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA",
    "username": "user1-0.co75htiiew",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.co75htiiew
```
```
200 OK

{
  "profile": {
    "username": "user1-0.co75htiiew",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.x9ubjewgofb
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.x9ubjewgofb]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1MzM0MDUzNzUsImV4cCI6MTUzMzU3ODE3NX0.TEn8T-4MVbytur2H-pmj4ZWOPeXV51znDjkdctWU9dE",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.4tvk32j2e9c",
    "email": "user2-0.4tvk32j2e9c@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.4tvk32j2e9c@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuNHR2azMyajJlOWMiLCJpYXQiOjE1MzM0MDUzNzUsImV4cCI6MTUzMzU3ODE3NX0.5Ke89VYeMx88_7ex4IDsGdmB7bjCGsfx5RS-NoXsIqU",
    "username": "user2-0.4tvk32j2e9c",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.co75htiiew@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.co75htiiew",
    "email": "updated-user1-0.co75htiiew@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.co75htiiew",
    "email": "updated-user1-0.co75htiiew@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.co75htiiew",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.co75htiiew",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuY283NWh0aWlldyIsImlhdCI6MTUzMzQwNTM3NSwiZXhwIjoxNTMzNTc4MTc1fQ.8BFHgEZWGKDGl9hILeP7kaEKdZiow-rwl8BDhgnXEXA"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.yfrxypj0u8s@email.com",
    "username": "user2-0.yfrxypj0u8s",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.yfrxypj0u8s@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAueWZyeHlwajB1OHMiLCJpYXQiOjE1MzM0MDUzNzUsImV4cCI6MTUzMzU3ODE3NX0.Bz2S2ofgsQMSIHLafr3Ol-oCHx6tz8UnxJk9eNSFtYw",
    "username": "user2-0.yfrxypj0u8s",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.yfrxypj0u8s@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.yfrxypj0u8s@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2018-08-04T17:56:16.225Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
