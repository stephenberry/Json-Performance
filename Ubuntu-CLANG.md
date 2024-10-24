# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Linux 6.5.0-1025-azure using the Clang 20.0.0 compiler).  

Latest Results: (Oct 24, 2024)
#### Using the following commits:
----
| Jsonifier: [ced96ae](https://github.com/RealTimeChris/Jsonifier/commit/ced96ae)  
| Glaze: [9d6f9c4](https://github.com/stephenberry/glaze/commit/9d6f9c4)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1755.01 | 1.3934e+06 | 847936 | 1.18151e+06 | 99 | 1696.39 | 1.44155e+06 | 847936 | 1.22234e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1261.35 | 2.06149e+06 | 847814 | 1.74776e+06 | 99 | 1790.21 | 1.45248e+06 | 847814 | 1.23143e+06 | 266 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 943.492 | 3.26199e+06 | 847814 | 2.76556e+06 | 288 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1379.76 | 1.77236e+06 | 577597 | 1.02371e+06 | 99 | 1360.13 | 1.79793e+06 | 577597 | 1.03848e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1034.33 | 2.49745e+06 | 577475 | 1.44222e+06 | 99 | 1416.58 | 1.82354e+06 | 577475 | 1.05305e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 587.958 | 4.65478e+06 | 577475 | 2.68802e+06 | 97 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1755.56 | 1.39296e+06 | 847936 | 1.18114e+06 | 97 | 1678.73 | 1.45672e+06 | 847936 | 1.2352e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1313.98 | 2.0641e+06 | 847814 | 1.74997e+06 | 268 | 1852.84 | 1.46381e+06 | 847814 | 1.24104e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 358.258 | 6.82589e+06 | 847814 | 5.78708e+06 | 162 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1378.43 | 1.77407e+06 | 577597 | 1.0247e+06 | 98 | 1354.92 | 1.80485e+06 | 577597 | 1.04248e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 982.415 | 2.4892e+06 | 577475 | 1.43745e+06 | 98 | 1337.49 | 1.82837e+06 | 577475 | 1.05584e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 263.752 | 9.8661e+06 | 577475 | 5.69743e+06 | 98 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2484.1 | 1.07649e+06 | 138774 | 149388 | 99 | 2377.08 | 1.12495e+06 | 138774 | 156114 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1786.69 | 1.45907e+06 | 138774 | 202480 | 98 | 1984.02 | 1.31395e+06 | 138774 | 182342 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1243.58 | 1.96645e+06 | 138482 | 272318 | 199 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2119.3 | 1.25859e+06 | 69037 | 86889.5 | 99 | 1617.25 | 1.64931e+06 | 69037 | 113864 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1439.94 | 1.8988e+06 | 69037 | 131088 | 257 | 1649.77 | 1.6573e+06 | 69037 | 114415 | 160 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 679.294 | 3.82121e+06 | 68745 | 262689 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3275.12 | 988898 | 6661897 | 6.58794e+06 | 98 | 2010.32 | 1.61107e+06 | 6661897 | 1.07328e+07 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2257.42 | 1.08329e+06 | 6661897 | 7.21674e+06 | 96 | 1530.02 | 1.5983e+06 | 6661897 | 1.06477e+07 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 931.944 | 2.62401e+06 | 6661897 | 1.74809e+07 | 97 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1103.09 | 2.94056e+06 | 2090234 | 6.14645e+06 | 98 | 812.723 | 3.99114e+06 | 2090234 | 8.34241e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1066.46 | 3.04082e+06 | 2090234 | 6.35604e+06 | 99 | 810.078 | 4.00323e+06 | 2090234 | 8.36769e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 388.447 | 8.3468e+06 | 2090234 | 1.74468e+07 | 100 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 4464.91 | 726411 | 1439556 | 1.04571e+06 | 98 | 3321.77 | 976396 | 1439556 | 1.40558e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 3298.32 | 983466 | 1439584 | 1.41578e+06 | 157 | 3299.29 | 983176 | 1439584 | 1.41536e+06 | 197 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2180.03 | 1.488e+06 | 1426839 | 2.12313e+06 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3548.04 | 913756 | 500293 | 457146 | 99 | 2268.66 | 1.42906e+06 | 500293 | 714946 | 195 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1906.09 | 1.70168e+06 | 500299 | 851350 | 99 | 2135.85 | 1.51863e+06 | 500299 | 759770 | 170 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 812.288 | 3.99321e+06 | 496312 | 1.98188e+06 | 96 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3685.55 | 879827 | 719230 | 632798 | 98 | 3671.26 | 883250 | 719230 | 635260 | 188 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2425.05 | 1.33755e+06 | 719139 | 961882 | 99 | 3370.99 | 962214 | 719139 | 691966 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1722.86 | 1.8824e+06 | 757230 | 1.42541e+06 | 97 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3763.26 | 861711 | 477797 | 411723 | 95 | 3351.44 | 967597 | 477797 | 462315 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2039.61 | 1.58933e+06 | 477706 | 759230 | 98 | 3462.27 | 936266 | 477706 | 447260 | 182 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1227.9 | 2.6417e+06 | 523243 | 1.38225e+06 | 99 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 997.94 | 3.25072e+06 | 69037 | 224420 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 931.44 | 3.48263e+06 | 69037 | 240430 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 541.484 | 5.99059e+06 | 69037 | 413572 | 96 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2405.84 | 1.34832e+06 | 847936 | 1.14329e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1998.03 | 1.62357e+06 | 847936 | 1.37668e+06 | 195 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 4767.45 | 680458 | 118385 | 80556 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2388.75 | 1.35782e+06 | 118385 | 160745 | 98 | 