# Useful Hystrix addons

[![Travis CI][travis img]][travis]
[![Download][bintray img]][bintray]
[![codecov][codecov img]][codecov]
[![Codacy][codacy img]][codacy]
[![][license img]][license]


1. **ComposedHystrixMetricsPublisher**

    According to Hystrix specification it is possible to register only one plugin of every type. This class is supposed to avoid this limitation and register list of plugins.
    All of these plugins will be called sequentially in case of Hystrix events. Sometimes it can be useful.

    Example:
    ```java
        HystrixCodaHaleMetricsPublisher plugin1 = new HystrixCodaHaleMetricsPublisher(new MetricRegistry());
        HystrixMetricsInitializationNotifier plugin2 = new HystrixMetricsInitializationNotifier();
        ComposedHystrixMetricsPublisher composedPlugin = new ComposedHystrixMetricsPublisher(plugin1, plugin2);
        HystrixPlugins.getInstance().registerMetricsPublisher(composedPlugin);
    ```

2. **HystrixAggregatedEventStream**

    This event stream aggregates all Hystrix events for every Hystrix Command and exposes it as a rx-java Observable. 
    It also dynamically adds lazy-initialized commands so event stream is fully aggregated.

    Example:
    ```java
        HystrixMetricsInitializationNotifier initNotifier = new HystrixMetricsInitializationNotifier();
        HystrixAggregatedEventStream aggregatedStream = new HystrixAggregatedEventStream(initNotifier, m -> true);
        ...
        aggregatedStream.observe().map(<...>).filter(<...>);

    ```

[travis]:https://travis-ci.org/ringcentral/hystrix-addons
[travis img]:https://travis-ci.org/ringcentral/hystrix-addons.svg?branch=master
[bintray]:https://bintray.com/ringcentral/maven/com.ringcentral.platform%3Ahystrix-addons/_latestVersion
[bintray img]:https://api.bintray.com/packages/ringcentral/maven/com.ringcentral.platform%3Ahystrix-addons/images/download.svg
[codecov]:https://codecov.io/gh/ringcentral/hystrix-addons
[codecov img]:https://codecov.io/gh/ringcentral/hystrix-addons/branch/develop/graph/badge.svg
[codacy]:https://www.codacy.com/app/mskonovalov/hystrix-addons?utm_source=github.com&utm_medium=referral&utm_content=ringcentral/hystrix-addons&utm_campaign=badger
[codacy img]:https://api.codacy.com/project/badge/Grade/d48232b8c6014ef99f420b06df8f5e27
[license]:LICENSE
[license img]:https://img.shields.io/badge/License-MIT-blue.svg


