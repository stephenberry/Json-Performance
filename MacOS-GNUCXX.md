# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the AppleClang 15.0.0.15000309 compiler).  

Latest Results: (Oct 22, 2024)
#### Using the following commits:
----
| Jsonifier: [eb38d50](https://github.com/RealTimeChris/Jsonifier/commit/eb38d50)  
| Glaze: [65d45d5](https://github.com/stephenberry/glaze/commit/65d45d5)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2088.22 | 682849 | 327000 | 251 | 1998.09 | 682849 | 341750 | 241 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1598.68 | 682770 | 427084 | 159 | 2482.05 | 682770 | 275084 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 779.158 | 682770 | 876292 | 242 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1268.72 | 353392 | 278542 | 231 | 1708.58 | 353392 | 206834 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1079.85 | 353313 | 327187 | 234 | 1767.86 | 353313 | 199854 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 411.987 | 353313 | 857584 | 98 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2101.61 | 682849 | 324916 | 97 | 2141.15 | 682849 | 318916 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1613.16 | 682770 | 423250 | 204 | 2469.15 | 682770 | 276520 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 339.887 | 682770 | 2.00881e+06 | 99 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1269.67 | 353392 | 278333 | 254 | 1799.39 | 353392 | 196396 | 231 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1032.13 | 353313 | 342313 | 215 | 1784.41 | 353313 | 198000 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 182.116 | 353313 | 1.94004e+06 | 256 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2944.57 | 132014 | 44833 | 98 | 2548.93 | 132014 | 51792 | 297 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1953.44 | 138774 | 71041 | 170 | 3558.31 | 138774 | 39000 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 618.029 | 47820 | 77375 | 97 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1727.9 | 62277 | 36042 | 100 | 1889.59 | 62277 | 32958 | 100 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1363.69 | 69037 | 50625 | 299 | 2514.28 | 69037 | 27458 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 301.913 | 23197 | 76833.5 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3265.66 | 6661880 | 2.03998e+06 | 98 | 1695.4 | 6661880 | 3.9294e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 3068.38 | 6661897 | 2.17115e+06 | 297 | 2336.65 | 6661897 | 2.85104e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1191.17 | 6661897 | 5.59273e+06 | 205 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1080.85 | 2090234 | 1.93388e+06 | 295 | 1001.68 | 2090234 | 2.08673e+06 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1068.81 | 2090217 | 1.95565e+06 | 97 | 775.004 | 2090217 | 2.69704e+06 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 374.625 | 2090234 | 5.57954e+06 | 183 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 4459.44 | 1420981 | 318646 | 99 | 2601.14 | 1420981 | 546292 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2992.12 | 1439584 | 481124 | 96 | 4214.7 | 1439584 | 341563 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2057.98 | 1425624 | 692730 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3057.72 | 481718 | 157542 | 94 | 2074.88 | 481718 | 232166 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1627.32 | 500299 | 307437 | 99 | 2369.22 | 500299 | 211166 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 807.498 | 495097 | 613125 | 98 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2590.58 | 524969 | 202646 | 98 | 2960 | 524969 | 177354 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2463.69 | 719139 | 291896 | 172 | 4345.79 | 719139 | 165480 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1497.16 | 659030 | 440188 | 98 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2117.45 | 477706 | 225604 | 97 | 3862.19 | 477706 | 123688 | 96 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1685.83 | 283536 | 168188 | 96 | 2328.84 | 283536 | 121750 | 209 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1015.48 | 425043 | 418562 | 98 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 906.39 | 69037 | 76167 | 163 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 590.272 | 69037 | 116958 | 177 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 563.664 | 69037 | 122479 | 293 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1362.16 | 682810 | 501270 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1260.38 | 682810 | 541750 | 97 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2217.99 | 118385 | 53375 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1906.87 | 118385 | 62083.5 | 98 | 