# REALITY CHECK: High-Pressure Benchmark Report


### Environment: The "Cloud-Standard" Constraints
Most benchmarks give engines gigabytes of "dream-room." We don't. 
This test reflects real-world cloud density where resources cost money.

* **JVM:** `-Xmx128m` (Hard limit)
* **Optimization:** `-XX:Tier4CompileThreshold=1000 -Xbatch` (Forced JIT)
* **Pressure:** 64MB Pre-allocated Byte-Buffer (Leaving only ~40-50MB for active operations)
* **Scope:** 2,000 Warm-ups | 1,000 Recorded Runs

---

## 📊 Final Performance Matrix
**Values:** CPU COST PER RUN in ms | [citm / canada / twitter]

```text
+----------------------+------------+------------+------------+------------+------------+
| Category / File      | Apex2C     | Apex2M     | Apex2S     | Apex2MS    | Ind. Std.  |
|                      | (Std)      | (Mem)      | (Safe)     | (Fort)     | (Ref)      |
+----------------------+------------+------------+------------+------------+------------+
| Pre-parser           | ---        | ---        | 3.4/ 2.7/1 | 3.2/ 2.7/1 | ---        |
+----------------------+------------+------------+------------+------------+------------+
| deserialize (Safe)   | ---        | ---        | 8.0/24.8/4 | 8.4/25.2/4 | ---        |
+----------------------+------------+------------+------------+------------+------------+
| deserialize (Unsafe) | 4.7/22.2/2 | 4.7/21.8/2 | 5.2/22.1/2 | 5.7/22.5/2 | 7.1/35.7/3 |
+----------------------+------------+------------+------------+------------+------------+
| serialize (Pretty)   | 6.6/22.5/2 | 6.5/22.7/2 | 6.6/22.8/2 | 7.5/22.8/2 | 6.1/18.2/3 |
+----------------------+------------+------------+------------+------------+------------+
| serialize (Compact)  | 3.8/13.6/2 | 3.7/14.1/2 | 4.2/14.2/2 | 3.7/14.0/2 | 4.1/15.0/2 |
+----------------------+------------+------------+------------+------------+------------+
```
Note: Apex Pre-parsing enables high-speed early-exit validation (2.7ms for Canada GeoJSON) with near-zero memory footprint.


## Reality RAM Utilization (Used MB)
**Values:** Baseline / Active Run (Peak) | [citm / canada / twitter]
```text
+----------------------+------------+------------+------------+------------+------------+
| Category / File      | Apex2C     | Apex2M     | Apex2S     | Apex2MS    | Ind. Std.  |
+----------------------+------------+------------+------------+------------+------------+
| Pre-parser           | ---        | ---        |  82 / 82   |  80 / 80   | ---        |
|                      |            |            |  82 / 82   |  80 / 80   |            |
|                      |            |            |  69 / 69   |  69 / 69   |            |
+----------------------+------------+------------+------------+------------+------------+
| deserialize (Safe)   | ---        | ---        |  71 / 91   |  71 / 111  | ---        |
|                      |            |            |  71 / 109  |  71 / 109  |            |
|                      |            |            |  69 / 82   |  70 / 82   |            |
+----------------------+------------+------------+------------+------------+------------+
| deserialize (Unsafe) |  71 / 111  |  80 / 92   |  71 / 95   |  71 / 107  |  82 / 111  |
|                      |  71 / 109  |  71 / 109  |  71 / 109  |  71 / 110  |  69 / 118  |
|                      |  69 / 82   |  69 / 94   |  69 / 82   |  69 / 82   |  69 / 99   |
+----------------------+------------+------------+------------+------------+------------+
| serialize (Pretty)   |  74 / 80   |  78 / 91   |  74 / 80   |  78 / 105  |  72 / 90   |
|                      |  81 / 95   |  85 / 91   |  81 / 87   |  85 / 99   |  73 / 96   |
|                      |  78 / 97   |  80 / 91   |  78 / 89   |  80 / 99   |  70 / 91   |
+----------------------+------------+------------+------------+------------+------------+
| serialize (Compact)  |  74 / 76   |  78 / 87   |  74 / 83   |  78 / 81   |  72 / 111  |
|                      |  81 / 84   |  85 / 88   |  81 / 84   |  85 / 90   |  73 / 117  |
|                      |  78 / 81   |  80 / 85   |  78 / 85   |  80 / 85   |  70 / 93   |
+----------------------+------------+------------+------------+------------+------------+
```


## The "Jitter" Myth
Observers will notice "Jitter Detected" warnings across all contestants (including the Industry Standard).
- **The Observation:** Increasing RAM to 512MB or 1024MB does not change the core CPU/Time values significantly.
- **The Reality:** OS interference and JVM background tasks are a constant. A truly resilient engine must deliver stable Core CPU Time regardless of environmental noise.
- **The Winner:** Apex demonstrates a significantly higher "Performance Floor." While the Industry Standard's efficiency collapses when the heap is 90% full (approaching OOM at 117MB), Apex maintains its speed and safety margin.


## Developer Takeaway
If you are developing for AWS Lambda, Google Cloud Functions, or high-density Kubernetes clusters:
- **Don't pay for idle RAM:** Apex is designed to work in the "starvation zone" where others trigger OOM (Out Of Memory) or GC-death-spirals.
- **Predictable Latency:** Even under extreme pressure, the core execution time remains surgical.
Security without Tax: The Fortress (MS) edition provides full structural safety with less memory overhead than the Industry Standard's "Unsafe" mode.
- **Reality Check:** Forcing Industry Standard into a 128MB heap reveals the cost of object-heavy architectures. Apex is built for hardware ROI.



