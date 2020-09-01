---
description: Overview of functions API methods
---

# Functions API

{% api-method method="post" host="https://api.codemash.io" path="/:version/serverless/functions/:id/execute" %}
{% api-method-summary %}
Execute Function
{% endapi-method-summary %}

{% api-method-description %}
Executes a function during request.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="version" type="string" required=true %}
The version of API endpoint. Current latest **v1**.
{% endapi-method-parameter %}

{% api-method-parameter name="id" type="string" required=true %}
ID of function to be executed.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Your project's secret key.
{% endapi-method-parameter %}

{% api-method-parameter name="x-cm-projectid" type="string" required=true %}
Your project's ID. Can be passed as query parameter.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Template" type="string" required=false %}
Parameter of JSON format to pass into function.
{% endapi-method-parameter %}

{% api-method-parameter name="Qualifier" type="string" required=false %}
Version or alias of a function to execute.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns a response received from a function as string.
{% endapi-method-response-example-description %}

```javascript
{
    Result: ""
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Returns if the user does not have a valid permission to call this method.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% tabs %}
{% tab title=".NET" %}
```csharp
var client = new CodeMashClient(apiKey, projectId);
var codeService = new CodeMashCodeService(client);

var response = await codeService.ExecuteFunctionAsync(new ExecuteFunctionRequest
{
    Id = Guid.Parse("{FUNCTION_ID}"),
});
```
{% endtab %}

{% tab title="Node" %}
```

```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
For execute function method you can use **GET** method instead of **POST**.
{% endhint %}
