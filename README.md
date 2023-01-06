# the_red

 * Run install_program.sh before running, and install zookeeper and redis.
 * Docker must be executable.

## Chapter 1

 * It shows an example of a stateless service. Stateless servers can be easily expanded by adding them to Load Balancer.

### geoip
 * This is an example of a country that tells you when you type ip. Use the published maxmind library.
  * An example of a stateless service that operates independently.

### scrap
 * This is an example of parsing and showing the entered url's Opengraph.
  * An example of a stateless service that operates independently.

## Chapter 2

### loadbalancer
 * The example of loadbalancer shows that loadbalancer works simply using nginx.
  * nginx installation is required.
```
   sudo apt install -y nginx
```
  * The nginx setting is: 127.0.0.1:7001 and 127.0.0.1:7002. You can run two scrap servers to use ports 7001 and 7002.
   * You can use Docker.
   * Docker build
```
   docker build . -t ch1/scrap
```
   * Docker Run
```
   docker run -e ENDPOINTS=0.0.0.0:7001 --network host ch1/scrap
   docker run -e ENDPOINTS=0.0.0.0:7002 --network host ch1/scrap
```

  * You can try running it with the following command:

### service discovery
 * Zookeeper must be run.
 * When callers are added/removed, callers will be notified of the change in callers through Zookeeper.
  * callee
   * The service that performs the actual Scrap.
  * caller
   * Service to request Scrap to callee.
   * The caller takes a list of calls and makes a request in a Round Robin way.
