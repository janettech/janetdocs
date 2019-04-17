
# Final Question:
The Datadog community has written a substantial number of high quality integrations and libraries. Select one from [this page](https://docs.datadoghq.com/developers/libraries/). With this selection in mind, write a blog post that announces your selection and explains the benefits it offers our users/community. The post should cover installation, configuration, usage, and best practices along with code samples where applicable. You should also thank the contributor for their effort.

**Java DogStatsD Client**

DogStatsD is a metrics aggregation service bundled with the Datadog Agent. DogStatsD implements the [StatsD](https://github.com/etsy/statsd) protocol. 
A statsD client library is shown below implemented in Java which allows for Java applications to easily send metrics to DogStatsD.

![DogstatsD](images/dogstatsD.png)


**Getting started**

For usage of StatsD metrics, the Agent must be [running and available]
[https://docs.datadoghq.com/developers/dogstatsd/](https://docs.datadoghq.com/developers/dogstatsd/).

The source is available at the github repo at:
[https://github.com/DataDog/java-dogstatsd-client](https://github.com/DataDog/java-dogstatsd-client).

The client jar is distributed via maven central, and can be downloaded [here](http://search.maven.org/#search%7Cga%7C1%7Cg%3Acom.datadoghq%20a%3Ajava-dogstatsd-client).

Add the dependency to maven pom.xml file

    <dependency>
    <groupId>com.datadoghq</groupId>
    <artifactId>java-dogstatsd-client</artifactId>
    <version>2.7</version>
    </dependency>

## Usage

    
    import com.timgroup.statsd.ServiceCheck;
    import com.timgroup.statsd.StatsDClient;
    import com.timgroup.statsd.NonBlockingStatsDClient;

    public class Foo {
    private static final StatsDClient statsd = new NonBlockingStatsDClient(
    "my.prefix",                          /* prefix to any stats; may be null or empty string */
    "statsd-host",                        /* common case: localhost */
    8125,                                 /* port */
    new String[] {"tag:value"}            /* Datadog     extension: Constant tags, always applied */
    );
        public static final void main(String[] args) {
        statsd.incrementCounter("foo");
    statsd.recordGaugeValue("bar", 100);
    statsd.recordGaugeValue("baz", 0.01); /* DataDog  extension: support for floating-point gauges */
    statsd.recordHistogramValue("qux", 15);     /*     DataDog extension: histograms */
    statsd.recordHistogramValue("qux", 15.5);   /* ...also floating-point */
    statsd.recordDistributionValue("qux", 15);     /* DataDog extension: global distributions */
    statsd.recordDistributionValue("qux", 15.5);   /* ...also floating-point */
    ServiceCheck sc = ServiceCheck
          .builder()
          .withName("my.check.name")
          .withStatus(ServiceCheck.Status.OK)
          .build();
    statsd.serviceCheck(sc); /* Datadog extension: send service check status */
    statsd.recordExecutionTime("bag", 25, "cluster:foo"); /* DataDog extension: cluster tag */
     }
    }


Finally, let's thank Datadog for the official implementation of the client library. 



