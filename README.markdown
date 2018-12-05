
# Extending the Yahoo Streaming Benchmarks 


### Background
This code is a fork of the original [Yahoo! Streaming benchmark code](https://github.com/yahoo/streaming-benchmarks).




flink.benchmark.AdvertisingTopologyFlinkWindows
This Flink program does the same operation in Flink as in the original benchmarks but uses Flink's native windowing and trigger support to accomplish the same things. It computes 10 seconds windows, emitting them to Redis when they're complete and also emits early updates every second.

flink.benchmark.genertor.AdImpressionGenerator
A data generator for Flink compatible with the original Yahoo data generator. This generator runs via Flink and writes data to Kafka. It can also be embedded directly in your Flink program as a source if Kafka becomes a bottleneck. This is the generator we used in the benchmarks as it was difficult to get the Clojure based generator to run at a high enough throughput for our experiments.

flink.benchmark.AdvertisingTopologyRedisDirect
This Flink program builds 60 minute windows directly in Redis. It's purpose is to illustrate the key-value store as the bottleneck when you don't have fault-tolerant state in the streaming system. Flink provides alternatives to this approach. The window time is configurable.

storm.benchmark.AdvertisingTopologyHighKeyCard
This Storm program is derivative of Yahoo's original AdvertisingTopology code. The difference is that it is designed for very high #'s of campaigns and builds the output windows by directly updating them in Redis. This benchmark represents any computation where it's neccessary to build state outside of the streaming system such that it's fault tolerant. Many applications in production work exactly this way and typically their throughput is limited by the remote key-value store. The windows in this case are set to 60 minutes by default



