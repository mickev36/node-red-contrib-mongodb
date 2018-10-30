# node-red-contrib-mongodb

Read and write a mongodb database. Fork from node-red-nodes/node-red-node-mongodb

"Official" alternative : https://github.com/node-red/node-red-nodes

Community alternative : https://github.com/ozomer/node-red-contrib-mongodb2


Pre-requisite
-------------

To run this you need a MongoDB server running. For details see
<a href="https://www.mongodb.org/" target="_new">the MongoDB site</a>.

Install
-------

Run the following command in your Node-RED user directory - typically `~/.node-red`

        npm install node-red-contrib-mongodb

Usage
-----

Nodes to save and retrieve data in a local MongoDB instance.

Optionally, you may also (via a function) set

- a `msg.projection` object to constrain the returned fields,
- a `msg.sort` object,
- a `msg.limit` number,
- a `msg.skip` number.

You can either set the collection method in the node config or on `msg.collection`.
Setting it in the node will override `msg.collection`.

See the <a href="http://docs.mongodb.org/manual/reference/method/db.collection.find/" target="new">*MongoDB collection methods docs*</a> for examples.

MongoDB only accepts objects.

*Find* queries a collection using the `msg.payload` as the query statement as
per the *.find()* function.

*Count* returns a count of the number of documents in a collection or matching a
query using the `msg.payload` as the query statement.

*Aggregate* provides access to the aggregation pipeline using the `msg.payload` as the pipeline array.

*Save* will update an existing object or insert a new object if one does not already exist.

*Insert* will insert a new object.

*Update* will modify an existing object or objects. The query to select objects
to update uses `msg.query` and the update to the element uses `msg.payload`.
Update can add an object if it does not exist or update multiple objects.

*Remove* will remove objects that match the query passed in on `msg.payload`.
A blank query will delete *all of the objects* in the collection.
By default MongoDB creates an `msg._id` property as the primary key - so
repeated injections of the same `msg` will result in many database entries.
If this is NOT the desired behaviour - ie. you want repeated entries to overwrite,
then you must set the `msg._id` property to be a constant by the use of a previous function node.
This must be done at the correct level. If only writing msg.payload then payload must contain the \_id property.
If writing the whole msg object then it must contain an \_id property.

This could be a unique constant or you could create one based on some other msg property.

Currently we do not limit or cap the collection size at all...

The result is returned in `msg.payload`.
