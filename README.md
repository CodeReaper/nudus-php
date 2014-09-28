nudus-php
=========

If you only want MVC and you mean ONLY that, this is the (not-really-a-)framework for you.

## Getting started

Installation is the same steps as upgrading:

- git clone https://github.com/CodeReaper/nudus-php.git
- cd nudus-php
- cp -r .htaccess nudus &lt;path to your project root&gt;

## Mapping

If you access the root of your project, Nudus will route to the defaultController and use the defaultAction and display the default view. Assuming you have the following code in a file named 'controller/defaultController.php':

    class defaultController {
        function defaultAction() {
            view('default');
        }
    }

To map a URL like '/php/echo/key1/value1/key2/value2', you could create a php controller by creating a file at named "controller/phpController.php" with contents:

    class phpController {
        function echoAction($data) {
            // $data contains the keys key1 and key2
            // and their values value1 and value2
            view('default', $data);
        }
    }

### Things to note

- Controller class names are suffixed with 'Controller'.
- Controller class file names must match the class names.
- Callable methods on controller classes are suffixed with 'Action'.
- Implementing a 404 response requires you to need a Http404Controller class with a defaultAction().

## Views

Nudus provides two global functions to aid you in creating your views, view and baseurl.

### view($name, $data)

Extracts the key-value data from the $data parameter and loads the the file /view/{$name}.php.

### baseurl($name, $return = false)

Prints or returns $name prepended with the site root. Useful for when the site is e.g. located at /subdir/ to create a link to an asset or another page.

## Benchmark

Testing machine:

<pre>Hardware Overview:

  Model Name: MacBook Pro
  Model Identifier: MacBookPro10,2
  Processor Name: Intel Core i7
  Processor Speed: 2,9 GHz
  Number of Processors: 1
  Total Number of Cores: 2
  L2 Cache (per Core): 256 KB
  L3 Cache: 4 MB
  Memory: 8 GB</pre>

A single request on the testing machine uses 256 Kb RAM.

Siege of 1000 requests with 5 concurrent clients' result is below.

<pre>$ ab -n 1000 -c 5 http://localhost:8888/nudus-php/
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests


Server Software:        Apache/2.2.26
Server Hostname:        localhost
Server Port:            8888

Document Path:          /nudus-php/
Document Length:        1884 bytes

Concurrency Level:      5
Time taken for tests:   0.913 seconds
Complete requests:      1000
Failed requests:        0
Write errors:           0
Total transferred:      2182000 bytes
HTML transferred:       1884000 bytes
Requests per second:    1094.86 [#/sec] (mean)
Time per request:       4.567 [ms] (mean)
Time per request:       0.913 [ms] (mean, across all concurrent requests)
Transfer rate:          2332.99 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    1   1.0      1      12
Processing:     1    3   1.6      3      16
Waiting:        0    3   1.5      2      15
Total:          2    4   2.1      4      20

Percentage of the requests served within a certain time (ms)
  50%      4
  66%      4
  75%      5
  80%      5
  90%      7
  95%      8
  98%     10
  99%     12
 100%     20 (longest request)</pre>