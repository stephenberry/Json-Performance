# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the Clang 19.1.1 compiler).  

Latest Results: (Oct 24, 2024)
#### Using the following commits:
----
| Jsonifier: [ced96ae](https://github.com/RealTimeChris/Jsonifier/commit/ced96ae)  
| Glaze: [9d6f9c4](https://github.com/stephenberry/glaze/commit/9d6f9c4)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1966.19 | 731629 | 372104 | 99 | 2355.34 | 731629 | 310625 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1412.21 | 731524 | 518000 | 243 | 2385.25 | 731524 | 306687 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 724.73 | 731524 | 1.00937e+06 | 200 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1226.2 | 377413 | 307791 | 97 | 1783.4 | 377413 | 211625 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 900.407 | 377308 | 419042 | 300 | 1643.9 | 377308 | 229520 | 181 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 397.184 | 377308 | 949958 | 183 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1937.66 | 731629 | 377583 | 98 | 2241.97 | 731629 | 326334 | 296 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1435.65 | 731524 | 509542 | 174 | 2358.8 | 731524 | 310125 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 291.914 | 731524 | 2.50596e+06 | 245 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1175.28 | 377413 | 321125 | 98 | 1729.11 | 377413 | 218270 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 950.248 | 377308 | 397062 | 300 | 1655.92 | 377308 | 227854 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 154.837 | 377308 | 2.43681e+06 | 97 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3136.92 | 132014 | 42084 | 285 | 2389.39 | 132014 | 55250 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1784.87 | 138774 | 77750 | 97 | 3589 | 138774 | 38666.5 | 178 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1631.99 | 138482 | 84854.5 | 96 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1762.52 | 62277 | 35334 | 169 | 1902.81 | 62277 | 32729 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1295.45 | 69037 | 53292 | 98 | 2588.86 | 69037 | 26667 | 201 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 862.904 | 68745 | 79667 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2980.15 | 6661880 | 2.23542e+06 | 202 | 2101.17 | 6661880 | 3.17056e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2868.08 | 6661897 | 2.32277e+06 | 97 | 2293.86 | 6661897 | 2.90423e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1101.54 | 6661897 | 6.04781e+06 | 166 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1039.28 | 2090234 | 2.01123e+06 | 96 | 954.027 | 2090234 | 2.19096e+06 | 96 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 981.889 | 2090217 | 2.12877e+06 | 181 | 908.099 | 2090217 | 2.30175e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 346.247 | 2090234 | 6.03683e+06 | 98 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 4325.4 | 1420981 | 328520 | 99 | 3120.61 | 1420981 | 455354 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2750.91 | 1439584 | 523312 | 211 | 4139.22 | 1439584 | 347792 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1948.69 | 1423437 | 730458 | 186 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2958.35 | 481718 | 162834 | 96 | 2058.26 | 481718 | 234042 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1702.54 | 500299 | 293854 | 98 | 2281.43 | 500299 | 219292 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 762.33 | 492910 | 646584 | 98 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2589.77 | 524969 | 202708 | 98 | 2623.48 | 524969 | 200104 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2313.43 | 719139 | 310854 | 98 | 4316.46 | 719139 | 166604 | 297 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1422.84 | 659130 | 463250 | 217 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1979.1 | 477706 | 241375 | 187 | 3803.89 | 477706 | 125584 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1697.82 | 283536 | 167000 | 96 | 2246.58 | 283536 | 126208 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 962.497 | 425143 | 441708 | 210 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 860.499 | 69037 | 80229 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 669.044 | 69037 | 103188 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 535.171 | 69037 | 129000 | 96 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1369.73 | 731581 | 534104 | 99 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1365.21 | 731581 | 535875 | 99 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2212.8 | 118385 | 53500 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2159.01 | 118385 | 54833 | 169 | 