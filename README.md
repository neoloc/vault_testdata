benchmark.hcl

```hcl
# Basic Benchmark config options
vault_addr = "https://vault.service.consul:8200"
vault_token = "hvs.CAESIFfnJR8nmzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz"
vault_namespace="root"
duration = "30s"
cleanup = true

test "approle_auth" "approle_logins" {
  weight = 30
  config {
    role {
      role_name = "benchmark-role"
      token_ttl="2m"
    }
  }
}

test "kvv2_write" "static_secret_writes" {
  weight = 10
  config {
    numkvs = 128
    kvsize = 64
  }
}

test "kvv2_read" "static_secret_reads" {
  weight = 60
  config {
    numkvs = 128
    kvsize = 64
  }
}
```

Additional latency: 0ms

```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T19:51:54.161+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T19:52:10.926+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T19:52:40.994+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T19:53:41.001+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        1449   48.358665  48.192048   153.496703ms  233.79019ms   297.522875ms  100.00%
static_secret_reads   2774   92.450602  92.431185   8.709678ms    18.874435ms   44.550189ms   100.00%
static_secret_writes  511    17.044834  17.004662   104.996258ms  168.136942ms  232.971902ms  100.00%
```


Additional latency: 25ms `sudo tc qdisc add dev wlo1 root netem delay 25ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T19:58:14.421+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T19:58:38.404+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T19:59:08.536+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:00:08.539+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        1128   37.597348  37.437420   164.779373ms  287.638661ms  388.268296ms  100.00%
static_secret_reads   2177   72.592665  72.518358   33.440918ms   41.405737ms   68.25389ms    100.00%
static_secret_writes  357    11.906169  11.858999   117.802785ms  196.605008ms  287.767335ms  100.00%
```



Additional latency: 50ms `sudo tc qdisc add dev wlo1 root netem delay 50ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:02:17.643+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:02:49.852+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:03:20.064+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:04:20.066+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        910    30.389481  30.183415   173.624611ms  254.71907ms   342.23546ms   100.00%
static_secret_reads   1752   58.455307  58.279003   59.425928ms   70.243538ms   92.24325ms    100.00%
static_secret_writes  289    9.726292   9.646781    134.449627ms  191.322902ms  228.175519ms  100.00%
```


Additional latency: 75ms `sudo tc qdisc add dev wlo1 root netem delay 75ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:09:00.088+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:09:34.584+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:10:04.696+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:11:04.700+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        833    27.788145  27.663993   159.684529ms  196.980114ms  222.082873ms  100.00%
static_secret_reads   1675   55.809949  55.663369   79.965832ms   84.203559ms   92.501406ms   100.00%
static_secret_writes  249    8.382448   8.347132    135.177347ms  167.204954ms  192.148927ms  100.00%
```


Additional latency: 100ms `sudo tc qdisc add dev wlo1 root netem delay 100ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:15:50.632+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:16:32.148+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:17:02.312+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:18:02.313+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        645    21.503646  21.384048   184.028308ms  238.738209ms  274.971339ms  100.00%
static_secret_reads   1366   45.527129  45.370194   107.936802ms  120.973321ms  201.868998ms  100.00%
static_secret_writes  220    7.345359   7.309658    157.70166ms   195.575192ms  247.541012ms  100.00%
```


Additional latency: 125ms `sudo tc qdisc add dev wlo1 root netem delay 125ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:19:58.263+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:20:47.861+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:21:18.006+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:22:18.015+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        547    18.258791  18.146426   217.381476ms  268.941885ms  359.983861ms  100.00%
static_secret_reads   1087   36.224637  36.068469   136.413739ms  151.370826ms  264.76401ms   100.00%
static_secret_writes  177    5.999424   5.964391    190.188574ms  237.051722ms  353.481312ms  100.00%
```


Additional latency: 150ms `sudo tc qdisc add dev wlo1 root netem delay 150ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:25:51.280+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:26:47.205+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:27:17.395+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:28:14.141+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        458    15.285901  15.179818   226.793671ms  284.531551ms  354.336442ms  100.00%
static_secret_reads   1017   33.865551  33.688088   159.075822ms  190.192434ms  255.496873ms  100.00%
static_secret_writes  172    5.893261   5.855284    205.810867ms  284.745951ms  364.825208ms  100.00%
```


Additional latency: 175ms `sudo tc qdisc add dev wlo1 root netem delay 175ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:31:16.177+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:32:20.206+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:32:50.427+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:33:49.801+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        420    14.016256  13.908277   250.082994ms  289.53662ms   333.685605ms  100.00%
static_secret_reads   871    29.044760  28.872948   185.110046ms  222.997101ms  300.894033ms  100.00%
static_secret_writes  152    5.065722   5.029743    229.381842ms  285.488399ms  357.478827ms  100.00%
```


Additional latency: 200ms `sudo tc qdisc add dev wlo1 root netem delay 200ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:37:30.561+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:38:40.709+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:39:10.972+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:39:58.947+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        388    12.950624  12.841242   281.726089ms  357.457328ms  416.62541ms   100.00%
static_secret_reads   771    25.768714  25.587574   213.080048ms  256.698263ms  358.113676ms  100.00%
static_secret_writes  106    3.580671   3.551114    259.938163ms  323.334284ms  385.678972ms  100.00%
```


Additional latency: 225ms `sudo tc qdisc add dev wlo1 root netem delay 225ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:41:12.338+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:42:28.481+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:42:58.787+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:43:42.561+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        354    11.792715  11.681118   299.0393ms    344.903949ms  456.562685ms  100.00%
static_secret_reads   706    23.562406  23.362368   233.010346ms  251.460982ms  330.140229ms  100.00%
static_secret_writes  112    3.859205   3.812254    275.663473ms  306.041261ms  337.590148ms  100.00%
```


Additional latency: 250ms `sudo tc qdisc add dev wlo1 root netem delay 250ms`
```
/usr/local/bin/vault-benchmark run -config=benchmark.hcl
2024-07-23T20:45:01.413+1000 [INFO]  vault-benchmark: setting up targets
2024-07-23T20:46:23.245+1000 [INFO]  vault-benchmark: starting benchmarks: duration=30s
2024-07-23T20:46:53.522+1000 [INFO]  vault-benchmark: cleaning up targets
2024-07-23T20:47:33.641+1000 [INFO]  vault-benchmark: benchmark complete
Target: https://vault.service.consul:8200
op                    count  rate       throughput  mean          95th%         99th%         successRatio
approle_logins        305    10.302917  10.184527   320.94028ms   358.446937ms  392.853538ms  100.00%
static_secret_reads   652    21.719152  21.535172   258.63109ms   267.494186ms  326.921066ms  100.00%
static_secret_writes  117    4.066710   4.026804    297.796397ms  325.377597ms  357.275372ms  100.00%
```



Analysis

```csv
Additional Latency	Operation	Count	Rate (ops/sec)	Throughput (ops/sec)	Mean Latency (ms)	95th Percentile (ms)	99th Percentile (ms)	Success Ratio (%)
0ms	logins	1449	48.36	48.19	153.50	233.79	297.52	100
0ms	reads	2774	92.45	92.43	8.71	18.87	44.55	100
0ms	writes	511	17.04	17.00	104.99	168.14	232.97	100
25ms	logins	1128	37.60	37.44	164.78	287.64	388.27	100
25ms	reads	2177	72.59	72.52	33.44	41.41	68.25	100
25ms	writes	357	11.91	11.86	117.80	196.61	287.77	100
50ms	logins	910	30.39	30.18	173.62	254.72	342.24	100
50ms	reads	1752	58.46	58.28	59.43	70.24	92.24	100
50ms	writes	289	9.73	9.65	134.45	191.32	228.18	100
75ms	logins	833	27.79	27.66	159.68	196.98	222.08	100
75ms	reads	1675	55.81	55.66	79.97	84.20	92.50	100
75ms	writes	249	8.38	8.35	135.18	167.20	192.15	100
100ms	logins	645	21.50	21.38	184.03	238.74	274.97	100
100ms	reads	1366	45.53	45.37	107.94	120.97	201.87	100
100ms	writes	220	7.35	7.31	157.70	195.58	247.54	100
125ms	logins	547	18.26	18.15	217.38	268.94	359.98	100
125ms	reads	1087	36.22	36.07	136.41	151.37	264.76	100
125ms	writes	177	5.99	5.96	190.19	237.05	353.48	100
150ms	logins	458	15.29	15.18	226.79	284.53	354.34	100
150ms	reads	1017	33.87	33.69	159.08	190.19	255.50	100
150ms	writes	172	5.89	5.86	205.81	284.75	364.83	100
175ms	logins	420	14.02	13.91	250.08	289.54	333.69	100
175ms	reads	871	29.04	28.87	185.11	223.00	300.89	100
175ms	writes	152	5.07	5.03	229.38	285.49	357.48	100
200ms	logins	388	12.95	12.84	281.73	357.46	416.63	100
200ms	reads	771	25.77	25.59	213.08	256.70	358.11	100
200ms	writes	106	3.58	3.55	259.94	323.33	385.68	100
225ms	logins	354	11.79	11.68	299.04	344.90	456.56	100
225ms	reads	706	23.56	23.36	233.01	251.46	330.14	100
225ms	writes	112	3.86	3.81	275.66	306.04	337.59	100
250ms	logins	305	10.30	10.18	320.94	358.45	392.85	100
250ms	reads	652	21.72	21.54	258.63	267.49	326.92	100
250ms	writes	117	4.07	4.03	297.80	325.38	357.28	100
```


# Operations per Second vs Latency

```python
import matplotlib.pyplot as plt

# Data
latency = [0, 25, 50, 75, 100, 125, 150, 175, 200, 225, 250]
approle_logins_rate = [48.36, 37.60, 30.39, 27.79, 21.50, 18.26, 15.29, 14.02, 12.95, 11.79, 10.30]
static_secret_reads_rate = [92.45, 72.59, 58.46, 55.81, 45.53, 36.22, 33.87, 29.04, 25.77, 23.56, 21.72]
static_secret_writes_rate = [17.04, 11.91, 9.73, 8.38, 7.35, 5.99, 5.89, 5.07, 3.58, 3.86, 4.07]

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(latency, approle_logins_rate, label='approle_logins', marker='o')
plt.plot(latency, static_secret_reads_rate, label='static_secret_reads', marker='o')
plt.plot(latency, static_secret_writes_rate, label='static_secret_writes', marker='o')

plt.xlabel('Additional Latency (ms)')
plt.ylabel('Operations per Second')
plt.title('Operations per Second vs Latency')
plt.legend()
plt.grid(True)

plt.show()
```




# Percentage reduction in Throughput for each latency band

```python
import numpy as np

# Calculate percentage reduction in throughput
approle_logins_reduction = [100 * (1 - (t / approle_logins_rate[0])) for t in approle_logins_rate]
static_secret_reads_reduction = [100 * (1 - (t / static_secret_reads_rate[0])) for t in static_secret_reads_rate]
static_secret_writes_reduction = [100 * (1 - (t / static_secret_writes_rate[0])) for t in static_secret_writes_rate]

# Latency range
latency_ms = np.linspace(0, 250, len(approle_logins_rate))

# Plotting
plt.figure(figsize=(10, 6))
plt.plot(latency_ms, approle_logins_reduction, label='approle_logins', marker='o')
plt.plot(latency_ms, static_secret_reads_reduction, label='static_secret_reads', marker='o')
plt.plot(latency_ms, static_secret_writes_reduction, label='static_secret_writes', marker='o')

plt.xlabel('Additional Latency (ms)')
plt.ylabel('Percentage Reduction in Throughput (%)')
plt.title('Percentage Reduction in Throughput vs Additional Latency')
plt.legend()
plt.grid(True)

plt.show()
```


Throughput Impact Summary
```csv
Additional Latency (ms)	approle_logins Throughput (ops/sec)	static_secret_reads Throughput (ops/sec)	static_secret_writes Throughput (ops/sec)
0	48.19	92.43	17.00
25	37.44	72.52	11.86
50	30.18	58.28	9.65
75	27.66	55.66	8.35
100	21.38	45.37	7.31
125	18.15	36.07	5.96
150	15.18	33.69	5.86
175	13.91	28.87	5.03
200	12.84	25.59	3.55
225	11.68	23.36	3.81
250	10.18	21.54	4.03
```

