# opentsdb-tsuid-ratelimiter

Provides an implementation of the OpenTSDB meta cache interface as discussed on the OpenTSDB [mailing list](https://groups.google.com/d/msg/opentsdb/oMLi0GCNF30/I32rpm8cCgAJ).

It works by allowing TSD instances to cache what tsmeta combinations have been seen and only writing a tsmeta
entry in tsdb-meta if a data point write misses this cache. The cache can obviously be bounded to limit memory consumption
and and is an LRU. This allows you to trade TSD memory consumption against tsdb-meta write rate.

Directions for use:

* Add the following to your OpenTSDB configuration:
```
tsd.core.meta.cache.plugin=uk.co.exemel.opentsdb.RateLimitedTsuidTracking
```
* Ensure the plugin Jar is in your classpath
* Set optional configuration for max cache size:
```
tsd.meta.cache.max_size=100000
```
* Set optional configuration for ttl
```
tsd.meta.cache.ttl_seconds=3600
```
