[![NuGet version](https://badge.fury.io/nu/kafka-net-core.svg)](https://badge.fury.io/nu/kafka-net-core)

# kafka-net-core

This is the net core versions of the library [kafka-net](https://github.com/Jroland/kafka-net)

# Examples

Use .NET CLI
```sh
dotnet add package kafka-net-core --version 1.0.2
```
##### Producer
```csharp
var options = new KafkaOptions(new Uri("http://localhost:9092"));
var router = new BrokerRouter(options);

using (Producer client = new Producer(router))
{
    client.SendMessageAsync("test_topic", new[] { new Message("hello world") }).Wait();
}
```
##### Consumer
```csharp
var options = new KafkaOptions(new Uri("http://localhost:9092"));
var router = new BrokerRouter(options);
using (var consumer = new Consumer(new ConsumerOptions("test_topic", router)))
{
    // Consume returns a blocking IEnumerable (ie: never ending stream)
    foreach (var message in consumer.Consume())
    {
        Console.WriteLine("Response: P{0},O{1} : {2}",
            message.Meta.PartitionId, message.Meta.Offset, message.Value);
    }
}
```
