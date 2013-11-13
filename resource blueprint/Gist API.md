# Gist API
Gist API.

## API Entry Point
[Gists.list][]

## Resource Gists
The Gists resource is a list of individual Gist pastes.

### Attributes
The properties of a gist collection (Gists resource).

+ total_count (number) - The count of gists in the collection.
  + Metadata
    + profile:
      + type: semantic

+ items (array) - An array of embedded individual Gist entities.
  + Metadata
    + profile:
      + type: semantic
      

### Affordances
Link relations of a gist collection.

+ list - Returns the current resource.
  + Metadata
    + profile:
      + type: safe      

+ create - Creates a gist, adds a gist to collection.
  + Metadata
    + profile:
      + type: unsafe

  + Attributes
    + description (string) - Description of the gist.
      + Metadata
        + profile:
          + type: semantic

    + content (string) - Content of the gist.
      + Metadata
        + profile:
          + type: semantic

+ search - Filters results based on parameters.
  + Metadata
    + profile:
      + type: safe

  + Parameters
    + search_by (string) - Keyword to search on.
      + Metadata
        + profile:
          + type: semantic

    + search_by_attribute (string) - Attribute to apply search to.
      + Metadata
        + profile:
          + type: semantic

      + Values
        + description
        + content

+ first
+ previous
+ next
+ last

### States
States / state machine of a gist collection.

+ collection (entry point) - Lorem Ipsum
    + Affordances
        + list (self) -> collection
        + create -> [Gist#active][]
            + Conditions
                + can_create
                + can_update

        + search -> navigation
        + next -> navigation
        + last -> navigation

+ navigation
    + Affordances
        + search (self) -> navigation
        + list -> collection
        + create -> [Gist#active][]
            + Conditions
                + can_create
                + can_update

        + first -> navigation
        + previous -> navigation
        + next -> navigation
        + last -> navigation

### HTTP
HTTP protocol-specific implementation. 

+ list: GET /gists
    + Response 200
        
        [Gists][]

+ create: POST /gists
    + Request (application/json)

            {
                "description": "Description of Gist",
                "content": "String Content"
            }

    + Response 201

        [Gist][]

+ search: GET /gists{?search_by,search_by_attribute}
    + Response 200

        [Gists][]

+ first: GET /gists?page=1{;per_page}
    + Response 200

        [Gists][]

+ previous: GET /gists{?page,per_page} 
    + Response 200

        [Gists][]       

+ next: GET /gists{?page,per_page}
    + Response 200

        [Gists][]

+ last: GET /gists{?page,per_page}
    + Response 200

        [Gists][]

### TCP
...

### COAP
...

### <other protocol>
...

### Media Types
+ application/hal+json

+ application/vnd.siren+json

+ application/json
    
    ```json
    { ... }
    ```

## Resource Gist

### Attributes
+ id
+ description
+ content
+ created_at
+ author
    + name

### Affordances
+ show 
+ edit
+ delete
+ archive
+ restore
+ author

### States
+ active
    + Affordances
        + show (self) -> active
        + edit -> active
        + delete (exit point)
        + archive -> archived
        + restore -> active
        + author -> [Author#show][]

+ archived
    + Affordances
        + show (self) -> archived
        + restore -> active
        + author -> [Author#show][]
