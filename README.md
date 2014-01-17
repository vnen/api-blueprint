# Resource Blueprint
Initial proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). Focused on modeling API resources, their attributes, [affordances](http://en.wikipedia.org/wiki/Affordance) and an API state machine.

## Concepts
The following highlights the API design concepts underlying a Resource Blueprint.

* Semantically define data and affordances (link relations).
* Define a state-machine representing the resource and the transition conditions (business rules) in different states.
    * Ideally, this should ultimately draw the state-machine as part of the design process.
    * Will be used mock the API to act as a true hypermedia API based on state.
* Adding metadata to elements that could be used to define a profile (e.g. ALPS) from the blueprint and other uses in 
the machine-readable output of the API Blueprint parser.
* Specify supported media-types.
    * The API Blueprint parser will generate sample representations based on the semantics, state-machine and 
    known media-types.
* Enter protocol specific information as an implementation detail well after having designed the actual API.
    * Initially only supports HTTP protocol.
    * The only actual URI you will see in the human-readable version is the entry point, even though you can enter 
    URIs in the blueprint.
* Specify the entry point to the resource.

APIs associated with specific resources can be designed individually as parts of an overall API that may span several
resource blueprints to represent the overall API application state-machine.

## Use Case API
As a use-case API this proposal is built on [Gist Fox API](../examples/Gist%20Fox%20API.md). This [example API](Gist%20API.md) includes:

* Entry point details
* Gists collection resource in full detail
* Gist entity resource in minimal detail

To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.
The actual proposed blueprint can be found in the [Gist API.md](Gist%20API.md) file. To view the source of the Gist API 
check its [raw version](https://raw.github.com/apiaryio/api-blueprint/resource-blueprint/resource%20blueprint/Gist%20API.md). Refer to [Resource Blueprint Syntax](#syntax) for explanation of new syntax constructs.

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

![fig1](assets/Gist%20State%20Machine%20001.png)

> **Note:** Collection also serves as a factory for individual `Gist` entities.

### Gist Resource
A `Gist` resource created by the `Gists`'s `create` affordance has following two states: `active` and `archived`:

![fig2](assets/Gist%20State%20Machine%20002.png)

### Embedded Entities
Finally, an individual `Gist` resource embedded in the `items` attribute of a `Gists` resource can be accessed directly via its `self` affordance:

![fig3](assets/Gist%20State%20Machine%20003.png)

<a name="syntax"></a>
## Resource Blueprint Syntax

### Keywords
New keywords introduced in the Resource Blueprint are:

+   `API Entry Point` (optional) - Denotes state machine entry point referencing a resource and its state.

+   `Resource` - Definition of a resource e.g. `Resource <resource name>`.

+   `Attributes` - Definition of resource attributes. *Alt keyword:* `Properties`.

+   `Affordances` (optional) - Definition of **all** resource's affordances. *Alt keywords:* `Transitions`, `Actions` or `Link Relations`.
        
    *Optional:* A resource definition without any affordance should assume one default "show/self" affordance.

+   `States` (optional) - definition of resource states and state transitions invoked using affordances.
    Each state should list all available affordances and the associated final state using the relevant affordance in the format:

    ```
    <affordance> -> <new state>
    ```

    The new state might be a reference to another resource state (see Referencing Syntax bellow). One affordance per state should be marked as `self` to represent the default "retrieve" affordance. 

    *Optional:* While defining states radically improves experience and possibilities in the following Resource Blueprint tool chain it should be valid to define a resource without states definition (and therefore without the `API Entry Point`). 

+   `Conditions` (optional) - list of conditions for an affordance to be available in the respective state.
    Associated with business rules tied to an affordance being available or present in a response. 
    *Alt keywords:* `Permissions` or `Rights`

    *Optional:* Conditions on affordances are completely optional. Absent conditions, an affordance should be considered always present in a response.

+   `HTTP`, `TCP`, `COAP`, `<other protocol>` (optional) - Protocol specific implementation of respective affordances.

    *Optional:* Protocol section should be optional. If not present, in the case of HTTP, a default method (GET?) should be expected with a default URI constructed from the resource name and possibly affordance parameters and or name. To be decided. 

+   `Media Types` (optional) - List of supported media type representations of respective resource attributes and affordances.
    Might include an explicit example asset.

    *Optional:* If media types are not present a default media type should be provided possibly `application/hal+json` and `application/vnd.siren+json`

    If a media type is specified but no explicit example is provided, a default representation using attributes and affordances will be
    generated for known media-types. For unknown media-types an explicit example should be included.

+   `Metadata` (optional) - Specific metadata as [planned for Format 1A](https://github.com/apiaryio/api-blueprint/issues/38). 

    The Gists Resource of *Gist API* demonstrates additional metadata to be used for generating an ALPS profile. 

> **Note:** Consider using alt keywords to improve clarity for general audience.

### Naming Attributes and Affordances
Where possible use undecorated plain text. In the case of a clash with keyword and/or the need for escaping (to not collide with Markdown syntax) use [Markdown code span element syntax](http://daringfireball.net/projects/markdown/syntax#code) e.g. `` `Attributes` ``.

### Referencing Syntax
+   Reference to a resource representation: `[<resource>][]`
+   Reference to a resource state: `[<resource>#<state>][]`
+   Reference to a resource affordance: `[<resource>.<affordance>][]`


## Acknowledgements
Special thanks to @fosdev for his tremendous contribution as well as images of the Gist State Machine. 
