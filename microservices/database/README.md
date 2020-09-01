---
description: Overview of database service
---

# Database

CodeMash **Database** service provides many operations for database management like CRUD operations, schema builder and data validation.

When you enable a database service in your [CodeMash dashboard page](https://cloud.codemash.io/) we create a new MongoDb database for you. When that is done you are able to create collections using our provided tools in the dashboard. After you create a collection you can start adding records through the dashboard or calling to API endpoints.

Features included in database service:

1. Collections - just like any database collection.
2. Taxonomies - special kind of collections used mostly for basic select type data.
3. Imports - importing records to collections.
4. Exports - exporting records from collections.
5. Backups - dumping and restoring collections.

## Using SDK

If you decide to use one of our provided SDK, the following code shows how to initialize database service.

{% tabs %}
{% tab title=".NET" %}
```csharp
var projectId = Guid.Parse("{YOUR_PROJECT_ID}");
var apiKey = "{YOUR_SECRET_KEY}";

var client = new CodeMashClient(apiKey, projectId);
var service = new CodeMashRepository<Person>(client);
```

Here **`Person`** is a class which extends interface **`IEntity`**. The example below shows a class extending **`Entity`** class which extends **`IEntity`** interface. Attribute **`CollectionName`** is a helper for a client. It takes one parameter - name of your collection in CodeMash.

```csharp
[Collection("persons")]
public class Person : Entity
{
    [Field("name")]
    public string Name { get; set; }
}
```

Here `UniqueName` is an attribute which is used to set the unique name of a field \(the name that is used inside a database\). This name can be found in your collection, field details. If this attribute is not used, then your field will be serialized and deserialized as a lowercase property name.
{% endtab %}

{% tab title="Node" %}
```javascript
import { db } from 'codemash';
```
{% endtab %}
{% endtabs %}

The following are the examples of database SDK using different languages and frameworks.

{% tabs %}
{% tab title=".NET" %}
```csharp
using System;
using CodeMash.Client;
using CodeMash.Repository;
using MongoDB.Driver;

namespace ConsoleApplication
{
    [CollectionName("persons")]
    public class Person : Entity
    {
        public string Name { get; set; }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // 1. Get your Project ID and Secret Key
            var projectId = Guid.Parse("{YOUR_PROJECT_ID}");
            var apiKey = "{YOUR_SECRET_KEY}";
            
            // 2. Create a general client for API calls
            var client = new CodeMashClient(apiKey, projectId);
            
            // 3. Create a service object
            var dbService = new CodeMashRepository<Person>(client);
            
            // 4. Call an API method
            var filter = Builders<Person>.Filter.Eq(x => x.Name, "John");
            var result = dbService.Find(filter);
        }
    }
}
```
{% endtab %}

{% tab title="Node" %}
```javascript
export async function getHolidaysOfEmployee(userId) {
    
    const filter = JSON.stringify({
        application_user: userId,
        status: 'Approved',
    });
    
    // gets first 100 records - all approved holidays sorted out by start date 
    const response = 
        await db.getRecords('holidays', 0, 100, { start: -1 }, filter);
    
    return response;
}
```
{% endtab %}
{% endtabs %}

## Working with Database Service

The following links explore the usage of database service:

{% page-ref page="collections/" %}

{% page-ref page="taxonomies-1.md" %}

{% page-ref page="imports.md" %}

{% page-ref page="exports.md" %}

{% page-ref page="backups.md" %}
