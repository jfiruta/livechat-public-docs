# JavaScript API

To use the JavaScript API you have to attach the [core functionality](#core-functionality) script.

## Initialize the communication
```js
LiveChat.init();
```

Let the Agent App know the extension is ready. Once called, the Agent App removes the loader screen from the extension and sends a request to `https://your_extension_url/authorize/`. This mechanism allows you to introduce an authorization flow for your service.

## Get the ID of the session

Returns the ID of the current extension session.

```js
LiveChat.getSessionId();
```

## Refresh the session ID

Deletes the ID of the previous session and calls of a new one.

```js
LiveChat.refreshSessionId();
```

## Events 

Events allow you react to the actions in the Agent App. Use this method as a listener for certain events.

```js
LiveChat.on("<event_name>", function( data ) {
	// ...
})
```

| Event name | Triggers when |
|------------|-------------|
| `customer_profile` | the agent opens a customer profile within **Chats**, **Archives** or **Visitors** sections |
| `customer_profile_hidden` | opened customer profile is removed from the Customers list |
| `authorize` | the extension has been successfully authorized |
| `authorize_error` | the extension has not been successfully authorized |

Events `customer_profile` and `customer_profile_hidden` return object width additional properties.

### Customer profile displayed

> Example `data` object for `customer_profile` event

```json-doc
{
  "id": "S126126161.O136OJPO1",
  "name": "Mary Brown",
  "email": "mary.brown@email.com",
  "chat": {
    "id": "NY0U96PIT4",
    "groupID": "42"
  }
}
```

| Property | Description |
|------------|-------------|
| `id` | Unique ID of a visitor |
| `name` | Visitor name (if provided) |
| `email` | Visitor email (if provided) |
| `chat` | Object with two properties: `id` (unique chat id) and `groupID` (unique group id) |

### Customer profile hidden

> Example `data` object for `customer_profile_hidden` event

```json-doc
{
  "id": "S126126161.O136OJPO1"
}
```

| Property | Description |
|------------|-------------|
| `id` | Unique ID of a visitor |
