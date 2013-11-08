# Resource Blueprint
Initial proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). Focused on modeling API resources, its attributes, affordances and an API state machine.

## Use Case API
As a use-case API this proposal is built on [Gist Fox API](../examples/Gist%20Fox%20API.md). To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.

The actual proposed blueprint can be found in the [Gist API.md](Gist%20API.md) file. To view the source of the Gist API check its [raw version](https://raw.github.com/apiaryio/api-blueprint/resource-blueprint/resource%20blueprint/Gist%20API.md). Refer to [Resource Blueprint Syntax](#syntax) for explanation of new syntax constructs.

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

![fig1](assets/Gist%20State%20Machine%20001.png)

> **Note:** Collection also serves as a factory for individual entities.

### Gist Resource
A `Gist` resource created by the `Gists`'s `create` affordance has following two states: `active` and `archived`:

![fig2](assets/Gist%20State%20Machine%20002.png)

### Embedded Entities
Finally, a `Gist` resource embedded in the `items` attribute of a `Gists` resource can be accessed via its `self` affordance:

![fig3](assets/Gist%20State%20Machine%20003.png)

> **Note:** The `Gist` Resource also specifies an undefined `Author` affordance. This is inte

<a name="syntax"></a>
## Resource Blueprint Syntax

### Keywords
New keywords introduced in the Resource Blueprint are:

+ 	`API Entry Point` (optional) - Denotes state machine entry point referencing a resource and its state.

+ 	`Resource` - Definition of a resource e.g. `Resource <resource name>`.

+ 	`Attributes` - Definition of resource attributes. *Alt keyword:* `Properites`.

+ 	`Affordances` (optional) - Definition of **all** resource's affordances. *Alt keywords:* `Transition`, `Actions` or `Link Relations`.
		
	*Optional:* A resource definition without any affordance should assume one default "show/self" affordance.

+ 	`States` (optional) - definition of resource states and state transitions invoked using affordances.
	Each state should lists all available affordances the final state of using the relevant affordance in format:

    ```
    <affordance> -> <new state>
    ```

    The new state might be a reference to another resource state (see Referencing Syntax bellow). One affordance per state should be marked as `self` to represent the default "retrieve" affordance. 

    *Optional:* While defining states radically improves experience and possibilities in the following Resource Blueprint tool chain it should be valid to define a resource without states definition (and therefore without the `API Entry Point`). 

+ 	`Conditions` (optional) - list of conditions for an affordance to be available in the respective state.
	Associated with business rules tied to an affordance being available or present in a response. 
	*Alt keywords:* `Permissions` or `Rights`

	*Optional:* Conditional affordances are completely optional.

+	`HTTP`, `TCP`, `COAP`, `<other protocol>` (optional) - Protocol specific implementation of respective affordances.

	*Optional:* Protocol section should be optional. If not present, in the case of HTTP, a default method (GET?) should be expected with a default URI constructed from the resource name and possibly affordance parameters and or name. To be decided. 

+	`Media Types` (optional) - List of supported media type representation of respective resource attributes and affordances.
	Might include an explicit example asset.

	*Optional:* If media types are not present a default media type should be provided possibly `application/hal+json` and `application/vnd.siren+json`

	If a media type is specified by no explicit example is provided a default representation using attributes and affordances should be provided.

> **Note:** Consider using alt keywords to improve clarity for general audience.

### Naming Attributes and Affordances
Where possible use an undecorated plain text. In the case of a clash with keyword and/or the need for escaping (to not collide with Markdown syntax) use [Markdown code span element syntax](http://daringfireball.net/projects/markdown/syntax#code) e.g. `` `Attributes` ``.

### Referencing Syntax
+ 	Reference to a resource representation: `[<resource>][]`
+ 	Reference to a resource state: `[<resource>#<state>][]`
+ 	Reference to a resource affordance: `[<resource>.<affordance>][]`


## Acknowledgements
Special thanks to @fosdev for his tremendous contribution as well as images of the Gist State Machine. 
