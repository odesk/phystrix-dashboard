### About

[Hystrix Dashboard](https://github.com/Netflix/Hystrix/wiki/Dashboard) provides instant insight into your application metrics.

*phystrix-dashboard* implements `text/event-stream` emitting server compatible with Hystrix Dashboard and lets you see stats for all Phystrix commands being executed on the machine.

### Installation and requirements

1. The pre-requirement is to have [Hystrix Dashboard](https://github.com/Netflix/Hystrix/wiki/Dashboard) installed and running. Read about installation and configuration in [Hystrix Dashboard Wiki](https://github.com/Netflix/Hystrix/wiki/Dashboard).
2. Run `composer require odesk/phystrix-dashboard` to download the source code.
3. Prepare a PHP file, to make use of phystrix-dashboard:

        // Composer built-in autoloader is used for event streaming endpoint
        include_once __DIR__ . '/../vendor/autoload.php';

        // $config is the same configuration you use for Odesk\Phystrix\CommandFactory in your application
        $config = new Zend\Config\Config(array(/* ... */));
        $metricsPoller = new \Odesk\PhystrixDashboard\MetricsEventStream\ApcMetricsPoller($config);
        $metricsServer = new \Odesk\PhystrixDashboard\MetricsEventStream\MetricsServer($metricsPoller);
        $metricsServer->run();

4. Serve this with a web server of your choice.
5. Point Hystrix Dashboard UI to this endpoint

### Limitations and known problems

* Due to a problem in Hystrix Dashboard's UI javascript, you cannot use backslash "\\" in command keys.

### License

Copyright 2013-2014 oDesk Corporation. All Rights Reserved.

phystrix-dashboard is licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.