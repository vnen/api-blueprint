# Resource Blueprint
A proposal of resource-oriented, protocol-independent [API Blueprint](http://apiblueprint.org). This proposal is focused on modeling API resources, its attributes, affordances and an API state machine.

## Use Case API
As an use-case API the Resource Blueprint uses [Gist Fox API](../examples/Gist%20Fox%20API.md). To demonstrate the description of the API state machine the Gist Fox API is extended with additional resource states.

The actual proposal source can be found in the [Gist API.md](Gist%20API.md) file.

## Gist State Machine

### Gists Resource 
An entry point to Resource Blueprint Gist API is the `Gists` resource in its `collection` state. This resource has two states: `collection` and 
`navigation`:

![fig1](assets/Gist%20State%20Machine%20001.png)

> **Note:** Collection essentially servers a factory for individual entities.

### Gist Resource

![fig2](assets/Gist%20State%20Machine%20002.png)


### Embedded Entities 

![fig3](assets/Gist%20State%20Machine%20003.png)

---

profile = /alps.io/Gists


REQUIRED
			Collection – a factory for individual entities

REQUIRED



REQUIRED



OPTIONAL
			Global traits, e.g. user id




OPTIONAL


OPTIONAL



OPTIONAL


Conditions, Permissions, Rights is associated with business rules tied to an affordance being available or present in a response.

Reference to a resource' state: [<resource>#<state>][]
Reference to a resource' affordance: [<resource>.<state>][]
