# HTTP Server Benchmark: Node.js vs Deno

This repository contains a benchmark comparison of HTTP servers implemented using Node.js and Deno. The goal is to evaluate the performance differences between these two environments in handling HTTP requests.

## Table of Contents

- [Introduction](#introduction)
- [Setup](#setup)
- [Running the Benchmark](#running-the-benchmark)

## Introduction

Node.js and Deno are both JavaScript/TypeScript runtime environments. Node.js has been widely used for server-side development, while Deno is a newer runtime created by the original developer of Node.js, Ryan Dahl. This benchmark aims to provide insights into the performance of HTTP servers in these two environments.

> NOTE: while using node cluster there will be some issue if you manage any kind of in-memory caching or global state that needs to be shared between these processes

## Setup

### Prerequisites

- Node.js (20.15.1)
- Deno (1.45.4)
- bombardier


## Running the Benchmark

To benchmark the servers, we will use bombardier

1. Start the Node.js server:

```bash
node baseline.mjs
```

2. Start the Deno server:

```bash
deno run --allow-all baseline.mjs
```

3. Benchmark using [bombardier](https://github.com/codesenberg/bombardier):

### Node.js
```bash
$ bombardier -n 10000 -c 30 http://localhost:8001/
Bombarding http://localhost:8001/ with 10000 request(s) using 30 connection(s)
 10000 / 10000 [=========================================================================================================================================================================] 100.00% 2622/s 3s
Done!
Statistics        Avg      Stdev        Max
  Reqs/sec      2642.36     362.15    4325.58
  Latency       11.36ms     3.87ms    58.77ms
  HTTP codes:
    1xx - 0, 2xx - 10000, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:   530.32KB/s
```

### Deno

```bash
$ bombardier -n 10000 -c 30 http://localhost:8001/
Bombarding http://localhost:8001/ with 10000 request(s) using 30 connection(s)
 10000 / 10000 [=========================================================================================================================================================================] 100.00% 1847/s 5s
Done!
Statistics        Avg      Stdev        Max
  Reqs/sec      1853.93     414.48    2985.33
  Latency       16.20ms     3.29ms    49.81ms
  HTTP codes:
    1xx - 0, 2xx - 10000, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:   328.77KB/s
```
