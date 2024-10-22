# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Linux 6.5.0-1025-azure using the GNU 12.3.0 compiler).  

Latest Results: (Oct 22, 2024)
#### Using the following commits:
----
| Jsonifier: [eb38d50](https://github.com/RealTimeChris/Jsonifier/commit/eb38d50)  
| Glaze: [65d45d5](https://github.com/stephenberry/glaze/commit/65d45d5)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2245.04 | 1.4443e+06 | 825395 | 1.19212e+06 | 97 | 2231.49 | 1.45307e+06 | 825395 | 1.19936e+06 | 236 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1503.55 | 2.15714e+06 | 825297 | 1.78028e+06 | 295 | 2243.37 | 1.44575e+06 | 825297 | 1.19317e+06 | 204 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1009 | 3.21428e+06 | 825297 | 2.65274e+06 | 300 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1705.46 | 1.90162e+06 | 558859 | 1.06274e+06 | 98 | 1788.58 | 1.81324e+06 | 558859 | 1.01334e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1261.13 | 2.57119e+06 | 558761 | 1.43668e+06 | 98 | 1829.65 | 1.77225e+06 | 558761 | 990266 | 193 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 705.887 | 4.59578e+06 | 558761 | 2.56794e+06 | 100 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1686.91 | 1.44965e+06 | 825395 | 1.19653e+06 | 98 | 1668.7 | 1.46547e+06 | 825395 | 1.20959e+06 | 167 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1137.06 | 2.15067e+06 | 825297 | 1.77494e+06 | 156 | 1689.26 | 1.44764e+06 | 825297 | 1.19473e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 435.205 | 7.34597e+06 | 825297 | 6.06261e+06 | 99 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1288.35 | 1.89811e+06 | 558859 | 1.06078e+06 | 98 | 1339.68 | 1.82538e+06 | 558859 | 1.02013e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 951.333 | 2.57053e+06 | 558761 | 1.43631e+06 | 97 | 1362.32 | 1.79505e+06 | 558761 | 1.00301e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 230.516 | 1.06085e+07 | 558761 | 5.9276e+06 | 99 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2646.64 | 1.23803e+06 | 138774 | 171806 | 99 | 3208.22 | 1.02132e+06 | 138774 | 141732 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2129.94 | 1.52024e+06 | 138774 | 210970 | 98 | 2741.95 | 1.18092e+06 | 138774 | 163881 | 161 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 570.822 | 5.6826e+06 | 47820 | 271742 | 97 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1414.22 | 1.72917e+06 | 69037 | 119376 | 220 | 1741.21 | 1.40444e+06 | 69037 | 96958.5 | 162 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1214.88 | 2.01289e+06 | 69037 | 138964 | 99 | 1656.64 | 1.47614e+06 | 69037 | 101908 | 231 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 289.122 | 1.11891e+07 | 23197 | 259553 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2553.39 | 957718 | 6661897 | 6.38022e+06 | 98 | 1569.8 | 1.55779e+06 | 6661897 | 1.03779e+07 | 100 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2370.8 | 1.03148e+06 | 6661897 | 6.87159e+06 | 97 | 1640.37 | 1.49078e+06 | 6661897 | 9.93143e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 885.003 | 2.76319e+06 | 6661897 | 1.84081e+07 | 168 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1179.76 | 2.75223e+06 | 2090234 | 5.75281e+06 | 97 | 761.264 | 4.26524e+06 | 2090234 | 8.91535e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 863.962 | 2.83048e+06 | 2090234 | 5.91637e+06 | 97 | 582.265 | 4.19986e+06 | 2090234 | 8.77868e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 281.817 | 8.67736e+06 | 2090234 | 1.81377e+07 | 98 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3111.93 | 785825 | 1439556 | 1.13124e+06 | 98 | 2901.16 | 842915 | 1439556 | 1.21342e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2452.04 | 997302 | 1439584 | 1.4357e+06 | 299 | 2395.05 | 1.02103e+06 | 1439584 | 1.46987e+06 | 160 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1325.42 | 1.84503e+06 | 1423437 | 2.62628e+06 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1951.96 | 1.25281e+06 | 500293 | 626772 | 176 | 2073.97 | 1.17911e+06 | 500293 | 589898 | 169 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1642.03 | 1.48927e+06 | 500299 | 745082 | 98 | 2111.13 | 1.15835e+06 | 500299 | 579523 | 170 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 486.645 | 5.02508e+06 | 492910 | 2.47691e+06 | 98 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2354.16 | 1.03877e+06 | 719230 | 747115 | 96 | 2537.51 | 963710 | 719230 | 693130 | 184 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1664.21 | 1.46943e+06 | 719139 | 1.05672e+06 | 98 | 2685.41 | 910635 | 719139 | 654873 | 179 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1015.1 | 2.40906e+06 | 638830 | 1.53898e+06 | 168 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2165.05 | 1.1295e+06 | 477797 | 539674 | 95 | 2279.55 | 1.07277e+06 | 477797 | 512564 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1532.45 | 1.59576e+06 | 477706 | 762306 | 297 | 2845.38 | 859439 | 477706 | 410559 | 158 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 683.469 | 3.57796e+06 | 416843 | 1.49145e+06 | 166 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 774.422 | 3.15775e+06 | 69037 | 218002 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 745.559 | 3.27999e+06 | 69037 | 226441 | 174 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 476.001 | 5.13745e+06 | 69037 | 354674 | 260 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1885.6 | 1.2969e+06 | 825395 | 1.07045e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1609.55 | 1.51933e+06 | 825395 | 1.25404e+06 | 99 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3652.65 | 669494 | 118385 | 79258 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1541 | 1.58691e+06 | 118385 | 187866 | 98 | 