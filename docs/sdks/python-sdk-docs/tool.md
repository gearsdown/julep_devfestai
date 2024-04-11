# Tools

[Julep Python SDK Index](./#julep-python-sdk-index) / [Julep](../../python-sdk-docs/julep/index.md#julep) / [Managers](../../python-sdk-docs/julep/managers/index.md#managers) / Tool

> Auto-generated documentation for [julep.managers.tool](../../../julep/managers/tool.py) module.

* [Tool](tool.md#tool)
  * [AsyncToolsManager](tool.md#asynctoolsmanager)
  * [BaseToolsManager](tool.md#basetoolsmanager)
  * [ToolsManager](tool.md#toolsmanager)

## AsyncToolsManager

[Show source in tool.py:344](../../../julep/managers/tool.py#L344)

A manager for asynchronous tools handling.

This class provides async methods to manage tools, allowing create, retrieve, update, and delete operations.

Methods: get: Asynchronously retrieves tools associated with an agent. create: Asynchronously creates a new tool associated with an agent. delete: Asynchronously deletes a tool associated with an agent. update: Asynchronously updates a tool associated with an agent.

Attributes: Inherited from BaseToolsManager.

#### Signature

```python
class AsyncToolsManager(BaseToolsManager): ...
```

#### See also

* [BaseToolsManager](tool.md#basetoolsmanager)

### AsyncToolsManager().create

[Show source in tool.py:395](../../../julep/managers/tool.py#L395)

Create a new resource asynchronously.

This method creates a new resource using the provided `agent_id` and `tool` information.

#### Arguments

agent\_id (Union\[str, UUID]): The identifier of the agent, which can be a string or a UUID object.

* `tool` _ToolDict_ - A dictionary containing tool-specific data.

#### Returns

* `ResourceCreatedResponse` - An object representing the response received after creating the resource.

#### Raises

* `BeartypeException` - If the type of any argument does not match the expected type.

#### Signature

```python
@beartype
async def create(
    self, agent_id: Union[str, UUID], tool: ToolDict
) -> ResourceCreatedResponse: ...
```

### AsyncToolsManager().delete

[Show source in tool.py:422](../../../julep/managers/tool.py#L422)

Asynchronously delete a specified agent-tool association.

This function is a high-level asynchronous API that delegates to a private coroutinal method `_delete` to perform the actual deletion based on the provided `agent_id` and `tool_id`.

Args: agent\_id (Union\[str, UUID]): The unique identifier of the agent. tool\_id (Union\[str, UUID]): The unique identifier of the tool.

Returns: The return type is not explicitly stated in the function signature. Typically, the returned value would be documented here, but you may need to investigate the implementation of `_delete` to determine what it returns.

Raises: The exceptions that this function might raise are not stated in the snippet provided. If the private method `_delete` raises any exceptions, they should be documented here. Depending on the implementation, common exceptions might include `ValueError` if identifiers are invalid or `RuntimeError` if deletion fails.

#### Signature

```python
@beartype
async def delete(self, agent_id: Union[str, UUID], tool_id: Union[str, UUID]): ...
```

### AsyncToolsManager().get

[Show source in tool.py:360](../../../julep/managers/tool.py#L360)

Asynchronously get a list of Tool objects based on provided filters.

This method fetches Tool objects with the option to limit the results and offset them, to allow for pagination.

#### Arguments

agent\_id (Union\[str, UUID]): The unique identifier of the agent for which to fetch tools.

* `limit` _Optional\[int], optional_ - The maximum number of tools to return. Defaults to None, which implies no limit.
* `offset` _Optional\[int], optional_ - The number of tools to skip before starting to return the tools. Defaults to None, which means start from the beginning.

#### Returns

* `List[Tool]` - A list of Tool objects that match the criteria.

#### Notes

This function is decorated with beartype, which assures that the input arguments adhere to the specified types at runtime. It is an asynchronous function and should be called with `await`.

#### Signature

```python
@beartype
async def get(
    self,
    agent_id: Union[str, UUID],
    limit: Optional[int] = None,
    offset: Optional[int] = None,
) -> List[Tool]: ...
```

### AsyncToolsManager().update

[Show source in tool.py:458](../../../julep/managers/tool.py#L458)

Asynchronously updates a resource identified by the agent\_id and tool\_id with a new definition.

This function is type-enforced using the `beartype` decorator.

#### Arguments

agent\_id (Union\[str, UUID]): The unique identifier for the agent. tool\_id (Union\[str, UUID]): The unique identifier for the tool.

* `function` _FunctionDefDict_ - A dictionary containing the function definition which needs to be updated.

#### Returns

* `ResourceUpdatedResponse` - An object representing the response received after updating the resource.

#### Raises

This will depend on the implementation of the `_update` method and any exceptions that it raises.

#### Signature

```python
@beartype
async def update(
    self,
    agent_id: Union[str, UUID],
    tool_id: Union[str, UUID],
    function: FunctionDefDict,
) -> ResourceUpdatedResponse: ...
```

## BaseToolsManager

[Show source in tool.py:21](../../../julep/managers/tool.py#L21)

A class to manage base tools by interacting with an API client.

This class provides an interface for creating, reading, updating, and deleting tools, where each tool is associated with an agent.

#### Attributes

* `api_client` - The API client utilized to send requests to the service.

#### Methods

* `_get(self,` _agent\_id_ - Union\[str, UUID], limit: Optional\[int]=None, offset: Optional\[int]=None) -> Union\[GetAgentToolsResponse, Awaitable\[GetAgentToolsResponse]]: Retrieve a list of tools associated with the given agent using the API client.
* `_create(self,` _agent\_id_ - Union\[str, UUID], tool: ToolDict) -> Union\[ResourceCreatedResponse, Awaitable\[ResourceCreatedResponse]]: Create a new tool associated with the given agent using the API client.
* `_update(self,` _agent\_id_ - Union\[str, UUID], tool\_id: Union\[str, UUID], function: FunctionDefDict) -> Union\[ResourceUpdatedResponse, Awaitable\[ResourceUpdatedResponse]]: Update the definition of an existing tool associated with the given agent using the API client.
* `_delete(self,` _agent\_id_ - Union\[str, UUID], tool\_id: Union\[str, UUID]): Delete a tool associated with the given agent using the API client.

#### Notes

All methods assert the validity of UUIDs for agent\_id and tool\_id when applicable. The \_get, \_create, and \_update methods may return either synchronous or asynchronous responses, indicated by the return type Union\[..., Awaitable\[...]].

#### Signature

```python
class BaseToolsManager(BaseManager): ...
```

### BaseToolsManager().\_create

[Show source in tool.py:80](../../../julep/managers/tool.py#L80)

Create a new tool associated with a given agent.

Args: agent\_id (Union\[str, UUID]): The ID of the agent for which to create the tool. Must be a valid UUID v4. tool (ToolDict): A dictionary with tool data conforming to the CreateToolRequest structure.

Returns: Union\[ResourceCreatedResponse, Awaitable\[ResourceCreatedResponse]]: The response object indicating the newly created tool, either as a direct response or as an awaitable if it's an asynchronous operation.

#### Signature

```python
def _create(
    self, agent_id: Union[str, UUID], tool: ToolDict
) -> Union[ResourceCreatedResponse, Awaitable[ResourceCreatedResponse]]: ...
```

### BaseToolsManager().\_delete

[Show source in tool.py:137](../../../julep/managers/tool.py#L137)

Delete a tool associated with an agent.

Args: agent\_id (Union\[str, UUID]): The UUID of the agent. tool\_id (Union\[str, UUID]): The UUID of the tool to be deleted.

Returns: The response from the API client's delete\_agent\_tool method.

Raises: AssertionError: If either `agent_id` or `tool_id` is not a valid UUID v4.

#### Signature

```python
def _delete(self, agent_id: Union[str, UUID], tool_id: Union[str, UUID]): ...
```

### BaseToolsManager().\_get

[Show source in tool.py:48](../../../julep/managers/tool.py#L48)

Retrieve tools associated with the given agent.

This is a private method that fetches tools for the provided agent ID, with optional limit and offset parameters for pagination.

#### Arguments

agent\_id (Union\[str, UUID]): The unique identifier for the agent, which can be a string or UUID object.

* `limit` _Optional\[int], optional_ - The maximum number of tools to retrieve. Defaults to None.
* `offset` _Optional\[int], optional_ - The number of tools to skip before starting to collect the result set. Defaults to None.

#### Returns

* `Union[GetAgentToolsResponse,` _Awaitable\[GetAgentToolsResponse]]_ - The response object which contains the list of tools, or an awaitable response object for asynchronous operations.

#### Raises

* `AssertionError` - If the agent\_id is not a valid UUID v4.

#### Signature

```python
def _get(
    self,
    agent_id: Union[str, UUID],
    limit: Optional[int] = None,
    offset: Optional[int] = None,
) -> Union[GetAgentToolsResponse, Awaitable[GetAgentToolsResponse]]: ...
```

### BaseToolsManager().\_update

[Show source in tool.py:105](../../../julep/managers/tool.py#L105)

Update the tool definition for a given agent.

Args: agent\_id (Union\[str, UUID]): The unique identifier for the agent, either in string or UUID format. tool\_id (Union\[str, UUID]): The unique identifier for the tool, either in string or UUID format. function (FunctionDefDict): A dictionary containing the function definition that conforms with the required API schema.

Returns: Union\[ResourceUpdatedResponse, Awaitable\[ResourceUpdatedResponse]]: The updated resource response sync or async.

Raises: AssertionError: If the `agent_id` or `tool_id` is not a valid UUID v4.

#### Signature

```python
def _update(
    self,
    agent_id: Union[str, UUID],
    tool_id: Union[str, UUID],
    function: FunctionDefDict,
) -> Union[ResourceUpdatedResponse, Awaitable[ResourceUpdatedResponse]]: ...
```

## ToolsManager

[Show source in tool.py:165](../../../julep/managers/tool.py#L165)

A manager class for handling tools related to agents.

This class provides an interface to manage tools, including their retrieval, creation, deletion, and updating. It extends the functionalities of the BaseToolsManager.

#### Methods

get: Retrieves a list of tools for the given agent.

#### Arguments

agent\_id (Union\[str, UUID]): The identifier of the agent whose tools are being retrieved.

* `limit` _Optional\[int], optional_ - The maximum number of tools to retrieve.
* `offset` _Optional\[int], optional_ - The index from which to start the retrieval.

agent\_id (Union\[str, UUID]): The identifier of the agent for whom the tool is being created.

* `tool` _ToolDict_ - A dictionary of tool attributes.

agent\_id (Union\[str, UUID]): The identifier of the agent whose tool is being deleted. tool\_id (Union\[str, UUID]): The unique identifier of the tool to be deleted.

update: Updates the definition of an existing tool for the given agent.

agent\_id (Union\[str, UUID]): The identifier of the agent whose tool is being updated. tool\_id (Union\[str, UUID]): The unique identifier of the tool to be updated.

* `function` _FunctionDefDict_ - A dictionary representing the definition of the tool to be updated.

#### Returns

* `List[Tool]` - A list of Tool objects.

create: Creates a new tool for the given agent.

* `ResourceCreatedResponse` - An object indicating the successful creation of the tool.

delete: Deletes a tool for the given agent.

* `ResourceUpdatedResponse` - An object indicating the successful update of the tool.

Inherits: - [BaseToolsManager](tool.md#basetoolsmanager) - A base class that defines the basic operations for tool management.

#### Signature

```python
class ToolsManager(BaseToolsManager): ...
```

#### See also

* [BaseToolsManager](tool.md#basetoolsmanager)

### ToolsManager().create

[Show source in tool.py:247](../../../julep/managers/tool.py#L247)

Create a new resource with the provided agent identifier and tool information.

This method wraps the internal `_create` method to construct and return a ResourceCreatedResponse.

Args: agent\_id (Union\[str, UUID]): The unique identifier for the agent. Can be a string or a UUID object. tool (ToolDict): A dictionary containing tool-specific configuration or information.

Returns: ResourceCreatedResponse: An object representing the successfully created resource, including metadata like creation timestamps and resource identifiers.

Raises: TypeError: If the `agent_id` or `tool` arguments are not of the expected type. ValueError: If any values within the `tool` dictionary are invalid or out of accepted range. RuntimeError: If the creation process encounters an unexpected error.

Note: The `@beartype` decorator is used to enforce type checking of the arguments at runtime.

Example usage:

```python
>>> response = instance.create(agent_id="123e4567-e89b-12d3-a456-426614174000", tool={"type": "screwdriver", "size": "M4"})
>>> print(response)
ResourceCreatedResponse(resource_id='abcde-12345', created_at='2021-01-01T12:00:00Z')
```

#### Signature

```python
@beartype
def create(
    self, agent_id: Union[str, UUID], tool: ToolDict
) -> ResourceCreatedResponse: ...
```

### ToolsManager().delete

[Show source in tool.py:285](../../../julep/managers/tool.py#L285)

Deletes an agent's access to a specific tool.

#### Arguments

agent\_id (Union\[str, UUID]): The unique identifier of the agent. tool\_id (Union\[str, UUID]): The unique identifier of the tool.

#### Returns

The result of the delete operation, the specific type of which may depend on the implementation of `_delete`.

#### Raises

* `Beartype` _exceptions_ - If `agent_id` or `tool_id` are of the wrong type.

#### Signature

```python
@beartype
def delete(self, agent_id: Union[str, UUID], tool_id: Union[str, UUID]): ...
```

### ToolsManager().get

[Show source in tool.py:216](../../../julep/managers/tool.py#L216)

Retrieve a list of Tool objects for the specified agent.

This method wraps the internal \_get method and returns the 'items' property from the result, which contains a list of Tool instances.

Args: agent\_id (Union\[str, UUID]): The ID of the agent to retrieve Tool objects for. limit (Optional\[int]): The maximum number of Tool objects to return. Defaults to None, implying no limit. offset (Optional\[int]): The number to skip before starting to collect the result set. Defaults to None, implying no offset.

Returns: List\[Tool]: A list of Tool instances associated with the specified agent ID.

Raises: BeartypeException: If the input argument types do not match the expected types.

#### Signature

```python
@beartype
def get(
    self,
    agent_id: Union[str, UUID],
    limit: Optional[int] = None,
    offset: Optional[int] = None,
) -> List[Tool]: ...
```

### ToolsManager().update

[Show source in tool.py:310](../../../julep/managers/tool.py#L310)

Update a specific tool definition for an agent.

#### Arguments

agent\_id (Union\[str, UUID]): The unique identifier of the agent. tool\_id (Union\[str, UUID]): The unique identifier of the tool to be updated.

* `function` _FunctionDefDict_ - A dictionary containing the new definition of the tool.

#### Returns

* `ResourceUpdatedResponse` - An object representing the update operation response.

#### Notes

This function is decorated with `beartype` which ensures that the arguments provided match the expected types at runtime.

#### Raises

* `BeartypeDecorHintPepParamException` - If the type of any parameter does not match the expected type. Any exceptions that `self._update` method might raise.

#### Signature

```python
@beartype
def update(
    self,
    agent_id: Union[str, UUID],
    tool_id: Union[str, UUID],
    function: FunctionDefDict,
) -> ResourceUpdatedResponse: ...
```