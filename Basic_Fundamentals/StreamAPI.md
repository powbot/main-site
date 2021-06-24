# Stream API

The stream API utilises the Java 11's stream functionality. Which is has been modernised and optimised so in turn is mroe cost-effective when it comes to processing power.

There are many different streams which will be covered in the docs, but for argument sake, we're going to use the inventory stream for our example.

```java
ItemStream items = ctx.inventory.toStream();
Item firstItem = items.first();
```

This then streams all of the items in your inventory and will allow you to filter on those to return the desired item.

### Filtering

The act of filtering will remove the items from our inventory which don't meet the criteria provided. Removing said items are the way we can filter down to a group of items which share the same criteria, e.g. all iron ore to drop.
It's also the way we can filter down to a single item e.g. a knife ready to cut some logs.

#### Optimised Filtering

Filtering on the desktop client is much quicker as there is more processing power available. However on Mobile, it's a little more restricted. In turn, we need to consider how we want to filter our streams.
With streams generically it's recomended to .filter() on the stream. This is not optimal for mobile and should only be used as a last resort.

```java
ctx.inventory.toStream().filter(i->i.id()==995).first();
```
In this snippet I'm filtering my inventory stream to return the item which ID is 995 (gp) and then using .first() to return the first item from the stream. While this is a valid way to filter the stream, it's not optimal.

```java
ctx.inventory.toStream().id(995).first();
```
The above snippet is the optimal way. id(), name(), at(), within(), nearest() have all been optimised to help reduce the processing power required to do the filtering and for mobile, you need optimisation where possible.