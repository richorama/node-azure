node-azure
==========

Node-Azure is a Node.js package (available via NPM) which allows native javascript access to the Windows Azure storage API.
This is embryonic and incomplete, but proves the concepts and looks like a good basis for further work.

Node-Azure currently supports most of methods on these storage types:

* Blob storage
* Table storage
* Queues

Blob Examples
-------------

Upload text as a blob:

    azure.blob.put_blob(account, "container", azure.blob.BlockBlob, "blobname",
      "Hello world!", {'Content-Type': "text/plain"}, callback);

Download a blob:

    azure.blob.get_blob(account, "container", "blobname", function(x) {
      // x == "Hello world!"
    });
	
Table Examples
--------------

Insert an entity:

    azure.tables.insert_entity(account, 'tablename',
      { RowKey:'123', PartitionKey: 'xyz', Value: 'foo' }, callback);

Get an entity:

    azure.tables.get_entity(account, 'tablename', 'xyz', '123', function(entity){
      // x == { RowKey:'123', PartitionKey: 'xyz', Value: 'foo' }
    });

Query a table:

    azure.tables.query_entities(account, 'tablename', "Value+eq+'foo'", function(entities){
      // entities is an array of matching items
    });

Queue Examples
--------------

Put a message on a queue:

    azure.queues.put_message(account, q, {Test:"Message"}, callback);

Pop the message off the queue:

    azure.queues.get_message(account, q, function(message){
      // our javascript object is returned: message.Data
    });

To install
----------

    npm install node-azure

Or alternatively, manually copy the repository into a node_modules/node-azure folder.

About
-----

By Rob Blackwell, Richard Astbury, Max Spencer
http://www.two10degrees.com

Any feedback / patches gratefully received

Depends on xml2js which can be installed via NPM

TODO
----

* Implement the wider APIs
* Make it NPM installable
* Implement a parser for Azure connection strings
* Implement a queue reader that looks like a callback
* Implement other Azure APIs? AppFabric? Service Management?
