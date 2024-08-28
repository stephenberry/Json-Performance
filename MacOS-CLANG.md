# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the Clang 19.1.1 compiler).  

Latest Results: (Oct 23, 2024)
#### Using the following commits:
----
| Jsonifier: [135affd](https://github.com/RealTimeChris/Jsonifier/commit/135affd)  
| Glaze: [2d5deae](https://github.com/stephenberry/glaze/commit/2d5deae)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2028.46 | 665125 | 327896 | 97 | 2466.85 | 665125 | 269625 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1553.89 | 665031 | 427980 | 99 | 2470.32 | 665031 | 269208 | 244 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 761.286 | 665031 | 873562 | 98 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1242.72 | 343458 | 276375 | 98 | 1791.76 | 343458 | 191688 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1050.85 | 343364 | 326750 | 191 | 1744.82 | 343364 | 196791 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 400.191 | 343364 | 858000 | 300 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2037.53 | 665125 | 326438 | 98 | 2375.45 | 665125 | 280000 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1535.35 | 665031 | 433146 | 206 | 2444.22 | 665031 | 272084 | 158 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 305.984 | 665031 | 2.17342e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1236.02 | 343458 | 277875 | 99 | 1832.39 | 343458 | 187438 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1053.6 | 343364 | 325896 | 262 | 1771.82 | 343364 | 193792 | 94 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 162.221 | 343364 | 2.11665e+06 | 98 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3242.95 | 132014 | 40708 | 99 | 2893.46 | 132014 | 45625 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1897.76 | 138774 | 73125 | 97 | 3453.16 | 138774 | 40187.5 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1648.6 | 138482 | 84000 | 293 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1821.63 | 62277 | 34187.5 | 99 | 1970.54 | 62277 | 31604 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1334.58 | 69037 | 51729.5 | 97 | 2646.77 | 69037 | 26083.5 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 870.416 | 68745 | 78979.5 | 98 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3057.43 | 6661880 | 2.17892e+06 | 98 | 2150.35 | 6661880 | 3.09804e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2918.07 | 6661897 | 2.28298e+06 | 98 | 2336.19 | 6661897 | 2.8516e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1157.58 | 6661897 | 5.75502e+06 | 97 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1078.59 | 2090234 | 1.93794e+06 | 98 | 985.117 | 2090234 | 2.12181e+06 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1015.7 | 2090217 | 2.05792e+06 | 99 | 939.635 | 2090217 | 2.2245e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 364.854 | 2090234 | 5.72896e+06 | 100 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 4500.64 | 1420981 | 315729 | 97 | 3491.71 | 1420981 | 406958 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2875.81 | 1439584 | 500584 | 98 | 4242.65 | 1439584 | 339312 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2031.33 | 1427811 | 702896 | 97 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3059.33 | 481718 | 157458 | 96 | 2132.28 | 481718 | 225916 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1758.78 | 500299 | 284458 | 97 | 2345.16 | 500299 | 213333 | 94 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 792.958 | 497284 | 627125 | 99 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2680.12 | 524969 | 195875 | 96 | 3140.41 | 524969 | 167166 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2381.42 | 719139 | 301979 | 96 | 4432.29 | 719139 | 162250 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1430.41 | 659030 | 460728 | 99 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2036.77 | 477706 | 234542 | 99 | 3902.28 | 477706 | 122417 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1754.73 | 283536 | 161584 | 96 | 2338.44 | 283536 | 121250 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 968.024 | 425043 | 439083 | 98 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 899.025 | 69037 | 76791 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 681.847 | 69037 | 101250 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 560.515 | 69037 | 123167 | 97 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1460.76 | 665074 | 455292 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1415.93 | 665074 | 469708 | 96 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2291.31 | 118385 | 51667 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2226.66 | 118385 | 53167 | 99 | 