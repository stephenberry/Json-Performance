# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Linux 6.5.0-1025-azure using the GNU 12.3.0 compiler).  

Latest Results: (Oct 23, 2024)
#### Using the following commits:
----
| Jsonifier: [135affd](https://github.com/RealTimeChris/Jsonifier/commit/135affd)  
| Glaze: [2d5deae](https://github.com/stephenberry/glaze/commit/2d5deae)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1674.95 | 1.46e+06 | 918347 | 1.34079e+06 | 179 | 1666.17 | 1.4677e+06 | 918347 | 1.34786e+06 | 188 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1523.72 | 2.13579e+06 | 918242 | 1.96118e+06 | 293 | 2210.07 | 1.47251e+06 | 918242 | 1.35212e+06 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 755.757 | 3.23574e+06 | 918242 | 2.97119e+06 | 98 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1697.09 | 1.91246e+06 | 627154 | 1.19941e+06 | 99 | 1785.4 | 1.81787e+06 | 627154 | 1.14008e+06 | 205 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1287.74 | 2.52285e+06 | 627049 | 1.58195e+06 | 98 | 1795.07 | 1.80983e+06 | 627049 | 1.13485e+06 | 220 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 534.35 | 4.57645e+06 | 627049 | 2.86966e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2220.77 | 1.46364e+06 | 918347 | 1.34413e+06 | 98 | 2206.71 | 1.47297e+06 | 918347 | 1.35269e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1149.24 | 2.12787e+06 | 918242 | 1.9539e+06 | 99 | 1656.61 | 1.47616e+06 | 918242 | 1.35548e+06 | 159 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 345.887 | 7.07002e+06 | 918242 | 6.49199e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1286.37 | 2.52115e+06 | 627049 | 1.58089e+06 | 158 | 1790.55 | 1.81126e+06 | 627049 | 1.13575e+06 | 173 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1278.65 | 1.9125e+06 | 627154 | 1.19943e+06 | 98 | 1324.86 | 1.8458e+06 | 627154 | 1.1576e+06 | 169 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 240.582 | 1.01646e+07 | 627049 | 6.37372e+06 | 98 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1989.59 | 1.22911e+06 | 138774 | 170568 | 98 | 2376.72 | 1.02891e+06 | 138774 | 142786 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1693.65 | 1.44388e+06 | 138774 | 200373 | 97 | 2053.75 | 1.19071e+06 | 138774 | 165240 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1210.05 | 2.02094e+06 | 138482 | 279864 | 202 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1886.34 | 1.7194e+06 | 69037 | 118702 | 97 | 2332.05 | 1.39079e+06 | 69037 | 96016 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1629.26 | 1.99071e+06 | 69037 | 137432 | 98 | 2197.23 | 1.47613e+06 | 69037 | 101908 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 833.169 | 3.8932e+06 | 68745 | 267638 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2584.27 | 946275 | 6661897 | 6.30398e+06 | 99 | 1544.87 | 1.58294e+06 | 6661897 | 1.05454e+07 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2507.96 | 1.03239e+06 | 6661897 | 6.87768e+06 | 99 | 1731.73 | 1.49515e+06 | 6661897 | 9.96052e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 957.07 | 2.71374e+06 | 6661897 | 1.80786e+07 | 99 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 895.766 | 2.72999e+06 | 2090234 | 5.70631e+06 | 99 | 574.876 | 4.25384e+06 | 2090234 | 8.89152e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 860.74 | 2.84108e+06 | 2090234 | 5.93852e+06 | 176 | 576.865 | 4.23917e+06 | 2090234 | 8.86085e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 285.488 | 8.56579e+06 | 2090234 | 1.79045e+07 | 99 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3117.5 | 784421 | 1439556 | 1.12922e+06 | 98 | 2914.28 | 839120 | 1439556 | 1.20796e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2533.1 | 965392 | 1439584 | 1.38976e+06 | 98 | 2392.88 | 1.02196e+06 | 1439584 | 1.4712e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1384.56 | 1.83354e+06 | 1423437 | 2.60992e+06 | 99 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1934.72 | 1.26397e+06 | 500293 | 632357 | 96 | 2046.77 | 1.19478e+06 | 500293 | 597738 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1612.18 | 1.51684e+06 | 500299 | 758875 | 195 | 2109.47 | 1.15926e+06 | 500299 | 579976 | 169 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 490.365 | 4.98696e+06 | 492910 | 2.45812e+06 | 97 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2412.3 | 1.01373e+06 | 719230 | 729108 | 168 | 2514.4 | 972568 | 719230 | 699500 | 183 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1723.67 | 1.41873e+06 | 719139 | 1.02027e+06 | 99 | 2675.2 | 914109 | 719139 | 657372 | 183 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1006.77 | 2.42899e+06 | 635630 | 1.54394e+06 | 99 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2160.19 | 1.13204e+06 | 477797 | 540886 | 208 | 2267.85 | 1.0783e+06 | 477797 | 515210 | 233 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1604.37 | 1.61905e+06 | 477706 | 773428 | 99 | 2990 | 868747 | 477706 | 415006 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 681.259 | 3.58957e+06 | 416843 | 1.49629e+06 | 96 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1024.48 | 3.05376e+06 | 69037 | 210822 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 833.073 | 3.28444e+06 | 69037 | 226748 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 482.94 | 5.06363e+06 | 69037 | 349578 | 179 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1610.87 | 1.51808e+06 | 918347 | 1.39412e+06 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1472.69 | 1.66052e+06 | 918347 | 1.52493e+06 | 184 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 4176.39 | 665245 | 118385 | 78755 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1629.89 | 1.58711e+06 | 118385 | 187890 | 98 | 