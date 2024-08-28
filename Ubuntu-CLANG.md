# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Linux 6.5.0-1025-azure using the Clang 20.0.0 compiler).  

Latest Results: (Oct 23, 2024)
#### Using the following commits:
----
| Jsonifier: [135affd](https://github.com/RealTimeChris/Jsonifier/commit/135affd)  
| Glaze: [2d5deae](https://github.com/stephenberry/glaze/commit/2d5deae)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1762.97 | 1.38711e+06 | 880210 | 1.22095e+06 | 299 | 1711.26 | 1.42903e+06 | 880210 | 1.25784e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1184.49 | 2.06454e+06 | 880079 | 1.81696e+06 | 164 | 1711.79 | 1.42858e+06 | 880079 | 1.25727e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 665.34 | 3.67546e+06 | 880079 | 3.2347e+06 | 174 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1375.85 | 1.77739e+06 | 596320 | 1.05989e+06 | 98 | 1379.19 | 1.7731e+06 | 596320 | 1.05733e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 982.487 | 2.48902e+06 | 596189 | 1.48393e+06 | 99 | 1353.68 | 1.80651e+06 | 596189 | 1.07702e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 470.601 | 5.1964e+06 | 596189 | 3.09804e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1756.61 | 1.39213e+06 | 880210 | 1.22537e+06 | 98 | 1696.82 | 1.44119e+06 | 880210 | 1.26855e+06 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1184.68 | 2.06422e+06 | 880079 | 1.81668e+06 | 98 | 1716.35 | 1.42478e+06 | 880079 | 1.25392e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 339.92 | 7.19414e+06 | 880079 | 6.33141e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1384.14 | 1.76675e+06 | 596320 | 1.05355e+06 | 98 | 1364.23 | 1.79253e+06 | 596320 | 1.06892e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 979.915 | 2.49556e+06 | 596189 | 1.48782e+06 | 98 | 1337.06 | 1.82897e+06 | 596189 | 1.09041e+06 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 237.097 | 1.0314e+07 | 596189 | 6.14912e+06 | 98 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2259.63 | 1.08223e+06 | 138774 | 150185 | 97 | 2197.25 | 1.11295e+06 | 138774 | 154448 | 212 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1780.86 | 1.37318e+06 | 138774 | 190561 | 98 | 1865.15 | 1.31112e+06 | 138774 | 181950 | 158 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 820.808 | 2.9793e+06 | 138482 | 412580 | 97 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2075.92 | 1.25326e+06 | 69037 | 86521.5 | 99 | 1569.99 | 1.65713e+06 | 69037 | 114403 | 166 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1433.61 | 1.88619e+06 | 69037 | 130217 | 98 | 1612.96 | 1.67646e+06 | 69037 | 115738 | 165 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 415.13 | 5.89076e+06 | 68745 | 404960 | 95 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 3022.38 | 1.07268e+06 | 6661897 | 7.14606e+06 | 98 | 2161.99 | 1.49957e+06 | 6661897 | 9.98995e+06 | 96 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2480.07 | 986034 | 6661897 | 6.56885e+06 | 97 | 1557.67 | 1.56993e+06 | 6661897 | 1.04587e+07 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 755.121 | 3.23847e+06 | 6661897 | 2.15743e+07 | 99 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 830.064 | 2.94608e+06 | 2090234 | 6.15799e+06 | 98 | 612.114 | 3.99506e+06 | 2090234 | 8.35062e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 803.83 | 3.04223e+06 | 2090234 | 6.35896e+06 | 98 | 617.942 | 3.95739e+06 | 2090234 | 8.27186e+06 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 238.567 | 1.02505e+07 | 2090234 | 2.1426e+07 | 99 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3328.21 | 734758 | 1439556 | 1.05773e+06 | 98 | 2653.48 | 921595 | 1439556 | 1.32669e+06 | 159 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2538.69 | 963264 | 1439584 | 1.3867e+06 | 99 | 2394.47 | 1.02128e+06 | 1439584 | 1.47022e+06 | 180 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1065.31 | 2.29551e+06 | 1426596 | 3.27477e+06 | 99 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2650.11 | 922766 | 500293 | 461654 | 163 | 1696.89 | 1.44113e+06 | 500293 | 720986 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1498.59 | 1.63183e+06 | 500299 | 816402 | 94 | 1640.95 | 1.49025e+06 | 500299 | 745572 | 179 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 385.98 | 6.33565e+06 | 496069 | 3.14292e+06 | 96 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2776.54 | 880747 | 719230 | 633460 | 158 | 2929.26 | 834829 | 719230 | 600434 | 208 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1836.69 | 1.33143e+06 | 719139 | 957484 | 195 | 2534.46 | 964872 | 719139 | 693877 | 171 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1027.65 | 2.37964e+06 | 732130 | 1.74221e+06 | 165 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2790.64 | 876298 | 477797 | 418692 | 300 | 2512.81 | 973186 | 477797 | 464986 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1631.25 | 1.49911e+06 | 477706 | 716135 | 97 | 2617.2 | 934369 | 477706 | 446354 | 165 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 716.85 | 3.41136e+06 | 498143 | 1.69934e+06 | 99 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 747.541 | 3.2713e+06 | 69037 | 225841 | 206 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 683.751 | 3.5765e+06 | 69037 | 246910 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 404.51 | 6.04542e+06 | 69037 | 417358 | 96 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1819.62 | 1.34392e+06 | 880210 | 1.18293e+06 | 165 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1495.92 | 1.63473e+06 | 880210 | 1.43891e+06 | 188 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3598.74 | 679524 | 118385 | 80445.5 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1720.88 | 1.42103e+06 | 118385 | 168229 | 99 | 