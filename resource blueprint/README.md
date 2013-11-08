# Resource Blueprint
A proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). This proposal is focused on modeling API resources, its attributes, affordances and an API state machine.

## Use Case API
As an use-case API the Resource Blueprint uses [Gist Fox API](../examples/Gist%20Fox%20API.md). To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.

The actual proposal can be found in the [Gist API.md](Gist%20API.md) file. Refer to [Resource Blueprint Syntax](#syntax) for explanation of the syntax constructs. 

To view the source of the Gist API check its [raw version](https://raw.github.com/apiaryio/api-blueprint/resource-blueprint/resource%20blueprint/Gist%20API.md).

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

![fig1](assets/Gist%20State%20Machine%20001.png)

> **Note:** Collection essentially servers as a factory for individual entities.

### Gist Resource
The `Gist` resource, created by the `create` affordance of the `Gists` Resource has following two states: `active` and `archived` each with appropriate set of affordances:

![fig2](assets/Gist%20State%20Machine%20002.png)

### Embedded Entities
Finally a `Gist` resource embedded in the `Gists` resource can be accessed via the `self` affordance of the particular embedded entity forming the complete API state machine:

![fig3](assets/Gist%20State%20Machine%20003.png)

<a name="syntax"></a>
## Resource Blueprint Syntax

### Keywords
New keywords introduced in the Resource Blueprint are:

+ 	`API Entry Point` - Denotes state machine entry point referencing a resource and its state.

+ 	`Resource` - Definition of a resource e.g. `Resource <resource name>`.

+ 	`Attributes` - Definition of resource attributes. Alt keyword: `Properites`.

+ 	`Affordances` - Definition of **all** resource's affordances. Alt keywords: `Transition`, `Actions` or `Link Relations`.

+ 	`States` (optional) - definition of resource states and state transitions invoked using affordances.
	Each state should lists all available affordances the final state of using the relevant affordance in format:

    ```
    <affordance> -> <new state>
    ```

    The new state might be a reference to another resource state (see Referencing Syntax bellow). One affordance per state should be marked as `self` to represent the default "retrieve" affordance. 

+ 	`Conditions` (optional) - list of conditions for an affordance to be available in the respective state.
	Associated with business rules tied to an affordance being available or present in a response. 
	Alt keywords: `Permissions` or `Rights`

+	`HTTP`, `TCP`, `COAP`, `<other protocol>` (optional) - Protocol specific implementation of respective affordances.

+	`Media Types` (optional) - List of supported media type representation of respective resource attributes and affordances.
	Might include an explicit example asset.

> **Note:** Consider using alt keywords to improve clarity for majority of users.

### Naming Attributes and Affordances
Where possible use an undecorated plain text. In the case of a clash with a keyword and/or need for escaping to not collide with Markdown formatting use [Markdown code span element syntax](http://daringfireball.net/projects/markdown/syntax#code) e.g. `\`Attributes\``.

### Referencing Syntax
+ 	Reference to a resource representation: `[<resource>][]`
+ 	Reference to a resource state: `[<resource>#<state>][]`
+ 	Reference to a resource affordance: `[<resource>.<affordance>][]`

