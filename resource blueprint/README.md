# Resource Blueprint
A proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). This proposal is focused on modeling API resources, its attributes, affordances and an API state machine.

## Use Case API
As an use-case API the Resource Blueprint uses [Gist Fox API](../examples/Gist%20Fox%20API.md). To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.

The actual proposal source can be found in the [Gist API.md](Gist%20API.md) file. Refer to [Resrouce Blueprint Syntax](#syntax) for 

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

> **Note:** Collection essentially servers a factory for individual entities.

![fig1](assets/Gist%20State%20Machine%20001.png)

### Gist Resource
The `Gist` resource, created by the `create` affordance of the `Gists` Resource has following two states: `active` and `archived` each with appropriate set of affordances:

![fig2](assets/Gist%20State%20Machine%20002.png)

### Embedded Entities
Finally a `Gist` resource embedded in the `Gists` resource can be accessed via the `self` affordance of the particular embedded entity forming the complete API state machine:

![fig3](assets/Gist%20State%20Machine%20003.png)

<a name="syntax"></a>
## Resource Blueprint Syntax

### Referencing Syntax

+ Reference to a resource state: `[<resource>#<state>][]`
+ Reference to a resource affordance: `[<resource>.<affordance>][]`


> **Note:** Conditions, Permissions, Rights is associated with business rules tied to an affordance being available or present in a response.
