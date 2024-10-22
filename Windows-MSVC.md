# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Windows 10.0.20348 using the MSVC 19.41.34123.0 compiler).  

Latest Results: (Oct 22, 2024)
#### Using the following commits:
----
| Jsonifier: [eb38d50](https://github.com/RealTimeChris/Jsonifier/commit/eb38d50)  
| Glaze: [65d45d5](https://github.com/stephenberry/glaze/commit/65d45d5)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1386.83 | 1.76331e+06 | 1008330 | 1.778e+06 | 97 | 1325.11 | 1.84545e+06 | 1008330 | 1.86082e+06 | 184 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 819.936 | 2.98244e+06 | 1008187 | 3.00686e+06 | 97 | 1393.37 | 1.75503e+06 | 1008187 | 1.7694e+06 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 306.581 | 7.97636e+06 | 1008187 | 8.04166e+06 | 97 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1031.19 | 2.37146e+06 | 683853 | 1.62173e+06 | 97 | 1100.19 | 2.22272e+06 | 683853 | 1.52002e+06 | 296 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 638.866 | 3.82774e+06 | 683710 | 2.61707e+06 | 97 | 1083.31 | 2.25737e+06 | 683710 | 1.54339e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 211.861 | 1.15425e+07 | 683710 | 7.89176e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1402.48 | 1.74363e+06 | 1008330 | 1.75816e+06 | 98 | 1325.52 | 1.84488e+06 | 1008330 | 1.86025e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 824.954 | 2.9643e+06 | 1008187 | 2.98857e+06 | 98 | 1414.31 | 1.72906e+06 | 1008187 | 1.74321e+06 | 259 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 84.5405 | 2.89259e+07 | 1008187 | 2.91627e+07 | 97 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1028.38 | 2.37794e+06 | 683853 | 1.62616e+06 | 165 | 1096.03 | 2.23116e+06 | 683853 | 1.52579e+06 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 639.376 | 3.8247e+06 | 683710 | 2.61498e+06 | 99 | 1082.33 | 2.2594e+06 | 683710 | 1.54477e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 57.7082 | 4.23756e+07 | 683710 | 2.89726e+07 | 96 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1454.45 | 1.68133e+06 | 138774 | 233326 | 99 | 1948.44 | 1.25507e+06 | 138774 | 174170 | 298 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1036.32 | 2.35971e+06 | 138774 | 327467 | 98 | 1911.34 | 1.27943e+06 | 138774 | 177552 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 90.5934 | 2.69933e+07 | 47820 | 1.29082e+06 | 184 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 915.05 | 2.67244e+06 | 69037 | 184498 | 99 | 1381.61 | 1.76998e+06 | 69037 | 122194 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 750.672 | 3.25764e+06 | 69037 | 224898 | 188 | 1275.01 | 1.91796e+06 | 69037 | 132410 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 44.5014 | 5.49515e+07 | 23197 | 1.27471e+06 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1515.86 | 1.61321e+06 | 6661897 | 1.07471e+07 | 97 | 1104.22 | 2.21462e+06 | 6661897 | 1.47535e+07 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1101.71 | 2.21965e+06 | 6661897 | 1.4787e+07 | 98 | 1143.09 | 2.13931e+06 | 6661897 | 1.42519e+07 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 447.528 | 5.46425e+06 | 6661897 | 3.64023e+07 | 188 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 490.021 | 4.99042e+06 | 2090234 | 1.04311e+07 | 97 | 445.502 | 5.48913e+06 | 2090234 | 1.14736e+07 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 357.278 | 6.84456e+06 | 2090234 | 1.43067e+07 | 98 | 436.339 | 5.60441e+06 | 2090234 | 1.17145e+07 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 142.267 | 1.71888e+07 | 2090234 | 3.59287e+07 | 197 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2805 | 871805 | 1439556 | 1.25501e+06 | 96 | 2298.1 | 1.0641e+06 | 1439556 | 1.53184e+06 | 192 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1952.03 | 1.25275e+06 | 1439584 | 1.80345e+06 | 167 | 2447.82 | 999021 | 1439584 | 1.43817e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 640.643 | 3.81713e+06 | 1425381 | 5.44086e+06 | 97 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1604.36 | 1.52423e+06 | 500293 | 762562 | 97 | 1617.51 | 1.51184e+06 | 500293 | 756364 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1098.5 | 2.22613e+06 | 500299 | 1.11373e+06 | 98 | 1289.28 | 1.89673e+06 | 500299 | 948934 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 232.839 | 1.05026e+07 | 494854 | 5.19725e+06 | 97 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1606.83 | 1.52189e+06 | 719230 | 1.09459e+06 | 97 | 2277.99 | 1.0735e+06 | 719230 | 772093 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1065.98 | 2.29405e+06 | 719139 | 1.64974e+06 | 97 | 2409.32 | 1.01499e+06 | 719139 | 729916 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 321.959 | 7.5954e+06 | 657230 | 4.99192e+06 | 98 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1344.07 | 1.81941e+06 | 477797 | 869308 | 98 | 2320.92 | 1.05364e+06 | 477797 | 503426 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 837.152 | 2.92112e+06 | 477706 | 1.39543e+06 | 297 | 2046.45 | 1.19496e+06 | 477706 | 570838 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 170.015 | 1.43836e+07 | 341243 | 4.90829e+06 | 99 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 530.427 | 4.61027e+06 | 69037 | 318280 | 176 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 476.906 | 5.12769e+06 | 69037 | 354000 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 286.067 | 8.54841e+06 | 69037 | 590156 | 97 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1318.68 | 1.85444e+06 | 1008330 | 1.86989e+06 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1292.95 | 1.89135e+06 | 1008330 | 1.9071e+06 | 96 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2325.25 | 1.05168e+06 | 123050 | 129409 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1560.41 | 1.56716e+06 | 123050 | 192839 | 98 | 