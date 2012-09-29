# ElasticObject #

ElasticObject is a multi level dynamic object implementation using .NET 4.0 dynamic features, for fluent access of data types like XML. 

For example, consider the XML 

> &lt;entry name="user"/&gt; 

You can access the same using fluent dynamic wrappers, like 

> var n=entry.name; 

You can also use it like ExpandoObject, with multi level property support. To start with, here are few scenarios you can use ElasticObject

* An easier, fluid way to work with data formats – like XML and JSON. Presently, we’ve some support for XML.
* Cleaner code though it is duck typed
* A hierarchical way to maintain loosely typed data.

### Using ElasticObject for XML driven T4 Code generation in Visual Studio ###

You can use ElasticObject to generate code using T4 from simple XML files. To install AmazedSaint.ElasticObject package from nuget, run the following command in the Package Manager Console

> Install-Package AmazedSaint.ElasticObject

Or you can install this via the Nuget Package manager, it is your choice.

### More ###

* [Introduction To ElasticObject] (http://www.amazedsaint.com/2010/02/introducing-elasticobject-for-net-40.html)
* [XML driven Code Generation using T4 and ElasticObject] (http://www.amazedsaint.com/2012/02/xml-driven-ct4-code-generation-with.html)
