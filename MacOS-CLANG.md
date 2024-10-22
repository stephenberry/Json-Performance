# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the Clang 19.1.1 compiler).  

Latest Results: (Oct 22, 2024)
#### Using the following commits:
----
| Jsonifier: [eb38d50](https://github.com/RealTimeChris/Jsonifier/commit/eb38d50)  
| Glaze: [65d45d5](https://github.com/stephenberry/glaze/commit/65d45d5)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2104.87 | 604844 | 287354 | 97 | 2376.01 | 604844 | 254562 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1556.03 | 604776 | 388667 | 98 | 2341.63 | 604776 | 258271 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 755.38 | 604776 | 800625 | 297 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1273.08 | 310843 | 244167 | 98 | 1863.66 | 310843 | 166792 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1056.46 | 310775 | 294166 | 222 | 1770.38 | 310775 | 175542 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 413.884 | 310775 | 750876 | 99 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2061.68 | 604844 | 293375 | 98 | 2339.07 | 604844 | 258583 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1556.53 | 604776 | 388542 | 97 | 2448.69 | 604776 | 246980 | 248 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 301.603 | 604776 | 2.00521e+06 | 96 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1199.78 | 310843 | 259084 | 252 | 1842.94 | 310843 | 168666 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1026.72 | 310775 | 302688 | 300 | 1724.53 | 310775 | 180208 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 158.964 | 310775 | 1.955e+06 | 188 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3257.96 | 132014 | 40520.5 | 98 | 2918.76 | 132014 | 45229.5 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1887.03 | 138774 | 73541 | 98 | 3622.16 | 138774 | 38312.5 | 298 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 528.518 | 47820 | 90479.5 | 97 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1827.19 | 62277 | 34083.5 | 98 | 2174.02 | 62277 | 28646 | 100 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1329.76 | 69037 | 51917 | 98 | 2651.09 | 69037 | 26041 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 271.707 | 23197 | 85375 | 98 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3092.53 | 6661880 | 2.15419e+06 | 97 | 2177.59 | 6661880 | 3.05929e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2886.88 | 6661897 | 2.30765e+06 | 98 | 2344.79 | 6661897 | 2.84115e+06 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1158.31 | 6661897 | 5.7514e+06 | 159 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1077.43 | 2090234 | 1.94002e+06 | 299 | 985.892 | 2090234 | 2.12015e+06 | 300 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1017.79 | 2090217 | 2.05369e+06 | 170 | 944.971 | 2090217 | 2.21194e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 337.445 | 2090234 | 6.19429e+06 | 300 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 4357.45 | 1420981 | 326104 | 98 | 3621.49 | 1420981 | 392375 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2876.53 | 1439584 | 500458 | 98 | 4156.89 | 1439584 | 346312 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2033.92 | 1427811 | 702000 | 99 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3061.36 | 481718 | 157354 | 95 | 2133.66 | 481718 | 225771 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1642.23 | 500299 | 304646 | 100 | 2341.72 | 500299 | 213646 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 792.853 | 497284 | 627208 | 98 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2639.41 | 524969 | 198896 | 166 | 3071.48 | 524969 | 170917 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2367.86 | 719139 | 303708 | 99 | 4416.99 | 719139 | 162812 | 95 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1203.34 | 659030 | 547666 | 300 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2030.45 | 477706 | 235271 | 98 | 3893.67 | 477706 | 122688 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1760.41 | 283536 | 161062 | 97 | 2627.88 | 283536 | 107896 | 183 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 966.646 | 425043 | 439709 | 297 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 907.379 | 69037 | 76084 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 689.367 | 69037 | 100146 | 206 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 552.296 | 69037 | 125000 | 300 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1462.45 | 604813 | 413562 | 191 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1397.87 | 604813 | 432667 | 98 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2293.17 | 118385 | 51625 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2231.91 | 118385 | 53042 | 99 | 