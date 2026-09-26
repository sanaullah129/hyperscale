Core Utilization = ((Total Time - Total Idle Time) / Total Time) \* 100

CPU Utilization = (Core 1 + Core 2 +...+ Core N Utilizations) / Total number of cores

Autocannon command:

`autocannon GET -c 20 -d 20 -p 2 -w 1 "http://localhost:3001/simple"`

- `autocannon`: Runs the HTTP load test.
- `GET`: Sends HTTP GET requests.
- `-c 20`: Uses 20 concurrent client connections.
- `-d 20`: Runs the test for 20 seconds.
- `-p 2`: Enables HTTP pipelining with up to 2 outstanding requests per connection.
- `-w 1`: Uses 1 worker thread to run the load test.
- `"http://localhost:3001/simple"`: The endpoint being tested on the local Express server.

## Benchmarks

- PORT 3000 = cpeak
- PORT 3001 = express
- PORT 3002 = fastify

### 1) cpeak (PORT 3000)

```bash
$ autocannon GET -c 20 -d 20 -p 2 -w 1 "http://localhost:3000/simple"
```

```text
Running 20s test @ http://GET,http://localhost:3000/simple
20 connections with 2 pipelining factor
1 workers

| Stat    | 2.5% | 50% | 97.5% | 99% | Avg     | Stdev   | Max    |
|---------|------|-----|-------|-----|---------|---------|--------|
| Latency | 0 ms | 0 ms | 1 ms | 1 ms | 0.06 ms | 0.54 ms | 126 ms |

| Stat      | 1%     | 2.5%   | 50%    | 97.5%  | Avg       | Stdev   | Min     |
|-----------|--------|--------|--------|--------|-----------|---------|---------|
| Req/Sec   | 31,503 | 31,503 | 39,007 | 41,823 | 38,730.81 | 2,241.83 | 31,495  |
| Bytes/Sec | 5.39 MB | 5.39 MB | 6.67 MB | 7.15 MB | 6.62 MB | 384 kB | 5.39 MB |

Req/Bytes counts sampled once per second.
# of samples: 20

781k requests in 20.84s, 132 MB read
3k errors (0 timeouts)
```

### 2) express (PORT 3001)

```bash
$ autocannon GET -c 20 -d 20 -p 2 -w 1 "http://localhost:3001/simple"
```

```text
Running 20s test @ http://GET,http://localhost:3001/simple
20 connections with 2 pipelining factor
1 workers

| Stat    | 2.5% | 50% | 97.5% | 99% | Avg    | Stdev | Max    |
|---------|------|-----|-------|-----|--------|-------|--------|
| Latency | 0 ms | 0 ms | 2 ms | 2 ms | 0.53 ms | 0.83 ms | 114 ms |

| Stat      | 1%     | 2.5%   | 50%    | 97.5%  | Avg       | Stdev  | Min     |
|-----------|--------|--------|--------|--------|-----------|--------|---------|
| Req/Sec   | 16,447 | 16,447 | 18,943 | 20,287 | 18,958.41 | 793.63 | 16,440  |
| Bytes/Sec | 4.13 MB | 4.13 MB | 4.76 MB | 5.09 MB | 4.76 MB | 199 kB | 4.13 MB |

Req/Bytes counts sampled once per second.
# of samples: 20

385k requests in 20.83s, 95.2 MB read
3k errors (0 timeouts)
```

### 3) fastify (PORT 3002)

```bash
$ autocannon GET -c 20 -d 20 -p 2 -w 1 "http://localhost:3002/simple"
```

```text
Running 20s test @ http://GET,http://localhost:3002/simple
20 connections with 2 pipelining factor
1 workers

| Stat    | 2.5% | 50% | 97.5% | 99% | Avg    | Stdev   | Max    |
|---------|------|-----|-------|-----|--------|---------|--------|
| Latency | 0 ms | 0 ms | 1 ms | 1 ms | 0.07 ms | 0.51 ms | 109 ms |

| Stat      | 1%     | 2.5%   | 50%    | 97.5%  | Avg       | Stdev   | Min     |
|-----------|--------|--------|--------|--------|-----------|---------|---------|
| Req/Sec   | 29,647 | 29,647 | 35,711 | 38,463 | 35,302.4 | 2,722.85 | 29,644  |
| Bytes/Sec | 5.55 MB | 5.55 MB | 6.68 MB | 7.19 MB | 6.6 MB | 509 kB | 5.54 MB |

Req/Bytes counts sampled once per second.
# of samples: 20

712k requests in 20.85s, 132 MB read
3k errors (0 timeouts)
```