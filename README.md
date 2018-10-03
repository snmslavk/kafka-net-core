# kafka-net-core

This is the net core versions of the library kafka-net

Examples
-----------
##### Producer
```sh
var options = new KafkaOptions(new Uri("http://SERVER1:9092"), new Uri("http://SERVER2:9092"));
var router = new BrokerRouter(options);
var client = new Producer(router);

client.SendMessageAsync("TestHarness", new[] { new Message("hello world")}).Wait();

using (client) { }
```
##### Consumer
```sh
var options = new KafkaOptions(new Uri("http://SERVER1:9092"), new Uri("http://SERVER2:9092"));
var router = new BrokerRouter(options);
var consumer = new Consumer(new ConsumerOptions("TestHarness", router));

//Consume returns a blocking IEnumerable (ie: never ending stream)
foreach (var message in consumer.Consume())
{
    Console.WriteLine("Response: P{0},O{1} : {2}", 
        message.Meta.PartitionId, message.Meta.Offset, message.Value);  
}
```
