# Apex-JSON-Engine
High-Performance Java NIO JSON Engine. Optimized for extreme speed and low-resource overhead. Outperforms industry standards in processing, CPU/RAM efficiency, and usability—because time is money. (Advanced 400GB+ and Pre-Parser shield available in Business Editions).

---

Key Features & Apex Specials
Apex goes beyond the standard JSON specification to provide a more flexible and efficient data format:

Extended Numeric Support:
Leading Zeros/Signs: Supports 005, +5.
Flexible Decimals: Supports .5, -.5.
Special Constants: Native handling for NaN and Infinity.
High Precision: Native BigDecimal support for financial or scientific data.
Smart Type Mapping: Automatically finds the smallest matching container for your data to save RAM:
Integers: byte → short → int → long.
Decimals: float → double → BigDecimal.
Text: char → String.
Developer Friendly:
Line Comments: Use // for single-line notes.
Block Comments: Use /* ... */ for documentation within the data.
High Performance: Industry-leading serialization speed.

Quick Example:
{
  // This is allowed in Apex
  "threshold": .5,
  "status": NaN,
  /* Smart container will pick 'byte' 
     internally for this value */
  "count": 005 
}

Built-in Safety & Limits
Apex is designed to handle extreme data structures without crashing the JVM:
Deep Nesting Support: Validated up to 10,500 levels of depth.
Stack Safety: Internal recursion limits and StackOverflowError protection ensure that deep nesting returns a clean false / null rather than crashing the process.
Memory Efficient: Tested with heap allocations up to 512MB, maintaining stable performance.

---

How to use Apex in your Java Project
Apex is designed for zero-friction integration. Just add the JAR to your
Java Classpath and you are ready to go.

---

Usage
Serialization (Object → File/String)

// Static "Safe" way
Apex2CJson.saveJava("data.json", myObject, true); // true = Pretty Print
String json = Apex2CJson.serializeJava(myObject, false);

// AutoCloseable way
try (Apex2CJson apex = new Apex2CJson()) {
    apex.save("data.json", myObject, true);
}


Deserialization (File/String -> Java Object)

// Static "Safe" way
// Returns 'LoadedContent' to allow manual buffer recycling
LoadedContent content = Apex2CJava.loadJson("data.json"); 
char[] rawBuffer      = content.data;
int length            = content.actualLength;

Object data  = Apex2CJava.parseJson("data.json");              
Object data2 = Apex2CJava.parseJson(rawBuffer);            

// AutoCloseable way
try (Apex2CJava apex = new Apex2CJava()) {
    Object result  = apex.parse("data.json");  
    Object result2 = apex.parse("{\"data\": NaN}".toCharArray());  
}

---

The Business Case: Why Apex Pays for Itself
Switching from industry standards to Apex isn't just a technical upgrade—it’s a direct reduction in operational costs (OpEx).

Scenario: Processing 100 Million JSON Requests / Day
Based on our canada_provinces.geojson benchmarks (41% faster, 65% less active RAM).

Metric             | Industry Standard | Apex2-Series   | Your Savings
-------------------|-------------------|----------------|-----------------
Compute Time       | ~1,211 Hours      | ~716 Hours     | -495 Hours (41%)
Active Heap Load   | 100% Capacity     | ~35% Capacity  | -65% RAM Overhead
Hardware Density   | 100 Nodes         | ~60 Nodes      | 40% Fewer Servers

The Financial Impact:
Cloud Bills (AWS/Azure/GCP): By reducing CPU execution time by 41%, you directly slash your "Pay-per-ms" compute costs.
Infrastructure Scaling: Since Apex2 uses 65% less active RAM, you can fit 2x more concurrent users on the same hardware, delaying expensive vertical scaling.
Energy & Cooling: Lower CPU cycles mean lower TDP (Thermal Design Power). For large-scale data centers, this translates into thousands of dollars saved in electricity and cooling.

The "Clean Road" Strategy: Apex Shield
The Sentinel: Stops invalid data/attacks at the door.
The Worker:   Only starts if the Sentinel gives the green light.

"Don't let bad data clog your infrastructure."
Apex is the only engine that validates at the speed of light with a near-zero memory footprint.
We clear the road, freeing up your CPU and RAM so your business logic 
can focus on what it was originally planned for: running your core services and generating profit.

---

Which Apex Edition is right for you?

1. Apex Standard (The Speed Demon)
*Best for: Developers, Students, and Personal Projects.*
- Usage: Strictly private, non-professional use on local personal machines.
- Goal:  Fastest possible parsing for trusted data.
- Cost:  100% FREE (Personal Use Only).

2. Apex Professional (The Efficiency Master)
*Best for: Freelancers, Startups, and Independent SaaS owners.*
- Usage: Commercial environments and for-profit applications.
- Goal:  Reduce Cloud Bills (AWS/Azure/GCP) and handle large data on small instances (Apex-M).
- Business Case: License fee is typically covered by monthly server savings.

3. Apex Enterprise (The Fortress)
*Best for: Corporations, Banks, and High-Traffic Platforms.*
- Usage: Mission-critical infrastructure handling untrusted public data.
- Goal: Prevention of "Poison JSON" / DoS attacks (Apex-S/MS) and malformed data.
- Business Case: Advanced infrastructure protection.
- The Apex-Sentinel is engineered to validate, process and discard malformed, corrupt, or injected JSON data at near wire-speed—ensuring your parser never becomes the bottleneck, even under massive network load.

4. Apex-XZ (The IO-Titan)
*Best for: AI Research, High-Performance Computing (HPC), and Large-Scale Data Centers.*
- Usage: Massive-scale AI training, data context ingestion, and scientific research.
- Goal:  Processing extreme datasets across the entire spectrum—from Gigabytes to Exabytes.
- Business Case: Engineered for environments where information density is critical.
- The Reality: The software has no internal limits. It reads and processes data as long as there is physical RAM available to hold the resulting objects. The only boundary is your hardware. If your server provides the RAM, Apex-XZ delivers the data.

---

The Industry Standard Reality Check

Scenario        | Industry Standard         | Apex Professional/Enterprise
----------------|---------------------------|------------------------------
100M Requests   | High "Inefficiency Tax"   | Massive Cost Savings
Deep Nesting    | Risk of StackOverflowError| Clean, Safe Exceptions
Resource Needs  | "Heavy" Footprint         | Ultra-Lean Execution

Ready to Upgrade?
Don't let inefficient parsing burn your budget. Stop paying the "Industry Standard Tax" to your cloud provider and invest in Apex instead.

Contact us for your Commercial License:
micha.laskowski@yahoo.com

