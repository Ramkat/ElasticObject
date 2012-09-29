# ElasticObject #

ElasticObject is a multi level dynamic object implementation using .NET 4.0 dynamic features, for fluent access of data types like XML. 

For example, consider the XML 

> &lt;entry name="user"/&gt; 

One possible use of ElasticObject is, you can access the same using fluent dynamic wrappers, like 

> var n=entry.name; 

You can also use it like ExpandoObject, with multi level property support. To start with, here are few scenarios you can use ElasticObject

* An easier, fluid way to work with data formats – like XML and JSON. Presently, we’ve some support for XML.
* Cleaner code though it is duck typed
* A hierarchical way to maintain loosely typed data.


###How to use ElasticObject###

You can create dynamic objects with multiple levels of properties. ElasticObject has got its own conventions ;)

'''
    dynamic CreateStoreObject()
        {
            dynamic store = new ElasticObject("Store");
            store.Name = "Acme Store";
            store.Location.Address = "West Avenue, Heaven Street Road, LA";
            store.Products.Count = 2;

            store.Owner.FirstName = "Jack";
            store.Owner.SecondName = "Jack";

            //try to set the internal content for an element
            store.Owner <<= "this is some internal content for owner";

            //Add a new product
            var p1 = store.Products.Product();
            p1.Name = "Acme Floor Cleaner";
            p1.Price = 20;

            //Add another product
            var p2 = store.Products.Product();
            p2.Name = "Acme Bun";
            p2.Price = 22;

            return store;

        }
'''		

Now, you can convert this to XML quite easily, using the > operator. You can convert the XML back to elasticobject as well. See below.

'''
            var store = CreateStoreObject();
            XElement el = store > FormatType.Xml;
            dynamic storeClone = el.ToElastic();
            XElement elCopy = storeClone > FormatType.Xml;
            Assert.AreEqual(el.ToString(), elCopy.ToString());
'''
			
See the unit tests for more examples.			


### Using ElasticObject for traversing XML ###

It is pretty easy to use ElasticObject to traverse XML. For example, here is a Console client that gets my Twitter timeline as XML, and print some properties.

Note the ToElastic extension method available for converting XElements to an ElasticObject

'''
class Program
    {
        static void Main(string[] args)
        {
            var cl=new WebClient();
            Console.WriteLine("Reading public time line");
            using (var r = new StreamReader
                (cl.OpenRead(@"http://twitter.com/statuses/user_timeline/amazedsaint.xml")))
            {
                var data = r.ReadToEnd();
                IterateTweets(data);
            }
            Console.ReadLine();

        }

        static void IterateTweets(string data)
        {
            dynamic root = XElement.Parse(data).ToElastic();
            foreach (var s in root["status"])
            {
                Console.WriteLine(~s.user.screen_name + " - " + ~s.text);
                Console.WriteLine();
            }
        }
    }
	
'''	
			


### Using ElasticObject for XML driven T4 Code generation in Visual Studio ###

You can use ElasticObject to generate code using T4 from simple XML files. To install AmazedSaint.ElasticObject package from nuget, run the following command in the Package Manager Console

> Install-Package AmazedSaint.ElasticObject

Or you can install this via the Nuget Package manager, it is your choice. See the example once you install the package.

### More ###

* [Introduction To ElasticObject] (http://www.amazedsaint.com/2010/02/introducing-elasticobject-for-net-40.html)
* [XML driven Code Generation using T4 and ElasticObject] (http://www.amazedsaint.com/2012/02/xml-driven-ct4-code-generation-with.html)
