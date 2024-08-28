# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the AppleClang 15.0.0.15000309 compiler).  

Latest Results: (Oct 23, 2024)
#### Using the following commits:
----
| Jsonifier: [135affd](https://github.com/RealTimeChris/Jsonifier/commit/135affd)  
| Glaze: [2d5deae](https://github.com/stephenberry/glaze/commit/2d5deae)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2075.31 | 545892 | 263041 | 96 | 2401.5 | 545892 | 227313 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1572.75 | 545841 | 347062 | 175 | 2491.24 | 545841 | 219104 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 771.076 | 545841 | 707896 | 245 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1289.86 | 281942 | 218583 | 99 | 1832.52 | 281942 | 153854 | 187 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1067.26 | 281891 | 264125 | 199 | 1833.19 | 281891 | 153770 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 421.244 | 281891 | 669188 | 99 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2054.64 | 545892 | 265688 | 97 | 2421.48 | 545892 | 225438 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1523.19 | 545841 | 358354 | 166 | 2498.61 | 545841 | 218458 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 317.742 | 545841 | 1.71787e+06 | 98 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1294.05 | 281942 | 217875 | 96 | 1917.43 | 281942 | 147042 | 95 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1068.78 | 281891 | 263750 | 165 | 1815.23 | 281891 | 155292 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 175.976 | 281891 | 1.60188e+06 | 297 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2948.65 | 132014 | 44771 | 295 | 2865.98 | 132014 | 46062.5 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1933.03 | 138774 | 71791 | 98 | 3604.52 | 138774 | 38500 | 196 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1709.22 | 138482 | 81020.5 | 98 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1714.06 | 62277 | 36333 | 99 | 1864.83 | 62277 | 33395.5 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1347.06 | 69037 | 51250 | 98 | 2521.9 | 69037 | 27375 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 789.986 | 68745 | 87020.5 | 300 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3270.6 | 6661880 | 2.0369e+06 | 97 | 1622.72 | 6661880 | 4.10538e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 3089.34 | 6661897 | 2.15642e+06 | 98 | 2332.78 | 6661897 | 2.85577e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1182.94 | 6661897 | 5.63167e+06 | 156 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1082.82 | 2090234 | 1.93035e+06 | 99 | 1003.06 | 2090234 | 2.08385e+06 | 99 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1067.61 | 2090217 | 1.95785e+06 | 99 | 763.462 | 2090217 | 2.73781e+06 | 297 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 372.037 | 2090234 | 5.61835e+06 | 296 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 4313.62 | 1420981 | 329417 | 98 | 3459.48 | 1420981 | 410750 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2983.21 | 1439584 | 482562 | 98 | 4208.28 | 1439584 | 342084 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2059.1 | 1425624 | 692354 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 3060.96 | 481718 | 157375 | 169 | 2074.14 | 481718 | 232250 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1635.07 | 500299 | 305980 | 97 | 2371.09 | 500299 | 211000 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 806.949 | 495097 | 613542 | 100 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2466.1 | 524969 | 212874 | 298 | 3187.26 | 524969 | 164708 | 160 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2443.45 | 719139 | 294312 | 161 | 4326.72 | 719139 | 166209 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1443.2 | 659030 | 456646 | 283 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2070.79 | 477706 | 230688 | 163 | 3861.56 | 477706 | 123708 | 96 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1671.96 | 283536 | 169584 | 95 | 2264.52 | 283536 | 125208 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1006.96 | 425043 | 422104 | 99 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 908.137 | 69037 | 76020.5 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 626.897 | 69037 | 110125 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 564.143 | 69037 | 122375 | 99 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1359.66 | 545875 | 401480 | 182 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1273.18 | 545875 | 428750 | 96 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 2214.5 | 118385 | 53459 | 98 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1904.34 | 118385 | 62166 | 98 | 