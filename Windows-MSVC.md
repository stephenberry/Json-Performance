# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Windows 10.0.20348 using the MSVC 19.41.34123.0 compiler).  

Latest Results: (Oct 23, 2024)
#### Using the following commits:
----
| Jsonifier: [135affd](https://github.com/RealTimeChris/Jsonifier/commit/135affd)  
| Glaze: [2d5deae](https://github.com/stephenberry/glaze/commit/2d5deae)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1404.84 | 1.7407e+06 | 865559 | 1.50668e+06 | 298 | 1448.04 | 1.68879e+06 | 865559 | 1.46174e+06 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 823.935 | 2.96796e+06 | 865439 | 2.56859e+06 | 98 | 1407.83 | 1.73702e+06 | 865439 | 1.50328e+06 | 202 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 306.405 | 7.98094e+06 | 865439 | 6.90702e+06 | 297 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1041.25 | 2.34852e+06 | 588625 | 1.3824e+06 | 219 | 1157.93 | 2.1119e+06 | 588625 | 1.24312e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 633.849 | 3.85802e+06 | 588505 | 2.27046e+06 | 160 | 1080.17 | 2.26393e+06 | 588505 | 1.33234e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 211.795 | 1.15461e+07 | 588505 | 6.79494e+06 | 162 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1385.03 | 1.76559e+06 | 865559 | 1.52822e+06 | 97 | 1426.81 | 1.71391e+06 | 865559 | 1.48349e+06 | 300 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 821.974 | 2.97504e+06 | 865439 | 2.57472e+06 | 95 | 1398.99 | 1.74799e+06 | 865439 | 1.51278e+06 | 300 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 84.6201 | 2.88986e+07 | 865439 | 2.501e+07 | 278 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1048.1 | 2.33319e+06 | 588625 | 1.37337e+06 | 98 | 1159.75 | 2.10859e+06 | 588625 | 1.24117e+06 | 259 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 632.362 | 3.8671e+06 | 588505 | 2.27581e+06 | 99 | 1076.26 | 2.27215e+06 | 588505 | 1.33717e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 57.9059 | 4.22307e+07 | 588505 | 2.4853e+07 | 99 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1464.82 | 1.66942e+06 | 138774 | 231672 | 159 | 1990.01 | 1.22885e+06 | 138774 | 170532 | 188 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1047.05 | 2.33553e+06 | 138774 | 324110 | 99 | 1900.33 | 1.28684e+06 | 138774 | 178580 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 364.573 | 6.70759e+06 | 138482 | 928881 | 233 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 913.528 | 2.67688e+06 | 69037 | 184804 | 98 | 1460.38 | 1.67452e+06 | 69037 | 115604 | 278 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 756.23 | 3.23369e+06 | 69037 | 223244 | 99 | 1271.71 | 1.92293e+06 | 69037 | 132753 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 184.765 | 1.32352e+07 | 68745 | 909857 | 98 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1515.83 | 1.61325e+06 | 6661897 | 1.07473e+07 | 241 | 1140.7 | 2.14379e+06 | 6661897 | 1.42817e+07 | 288 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1080.29 | 2.26364e+06 | 6661897 | 1.50802e+07 | 97 | 1105.33 | 2.21238e+06 | 6661897 | 1.47386e+07 | 185 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 449.808 | 5.43657e+06 | 6661897 | 3.62179e+07 | 298 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 488.959 | 5.00125e+06 | 2090234 | 1.04538e+07 | 97 | 445.459 | 5.48969e+06 | 2090234 | 1.14747e+07 | 179 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 346.585 | 7.05572e+06 | 2090234 | 1.47481e+07 | 97 | 434.678 | 5.62581e+06 | 2090234 | 1.17593e+07 | 191 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 136.768 | 1.78799e+07 | 2090234 | 3.73732e+07 | 191 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2873.2 | 851110 | 1439556 | 1.22522e+06 | 97 | 2427.76 | 1.00728e+06 | 1439556 | 1.45003e+06 | 189 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1960 | 1.24766e+06 | 1439584 | 1.79611e+06 | 96 | 2436 | 1.00386e+06 | 1439584 | 1.44514e+06 | 195 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 639.845 | 3.82187e+06 | 1425381 | 5.44762e+06 | 158 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1693.39 | 1.44409e+06 | 500293 | 722468 | 98 | 1645.5 | 1.48613e+06 | 500293 | 743501 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1092.04 | 2.23931e+06 | 500299 | 1.12032e+06 | 225 | 1272.35 | 1.92198e+06 | 500299 | 961564 | 176 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 231.18 | 1.05779e+07 | 494854 | 5.23454e+06 | 95 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1629.9 | 1.50034e+06 | 719230 | 1.07909e+06 | 96 | 2528.44 | 967168 | 719230 | 695616 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1048.32 | 2.33269e+06 | 719139 | 1.67753e+06 | 97 | 2367.87 | 1.03275e+06 | 719139 | 742692 | 167 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 320.187 | 7.63743e+06 | 657230 | 5.01955e+06 | 97 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1316.19 | 1.85795e+06 | 477797 | 887721 | 98 | 2380.6 | 1.02723e+06 | 477797 | 490808 | 157 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 823.528 | 2.96943e+06 | 477706 | 1.41851e+06 | 97 | 2038.72 | 1.1995e+06 | 477706 | 573006 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 200.195 | 1.22151e+07 | 402443 | 4.91589e+06 | 97 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 559.588 | 4.37002e+06 | 69037 | 301693 | 100 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 514.62 | 4.75188e+06 | 69037 | 328056 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 291.414 | 8.39154e+06 | 69037 | 579327 | 98 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 1449.99 | 1.68649e+06 | 865559 | 1.45976e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1316.34 | 1.85773e+06 | 865559 | 1.60797e+06 | 98 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/135affd) | 2352.65 | 1.03944e+06 | 123050 | 127902 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/2d5deae) | 1224.77 | 1.99664e+06 | 123050 | 245686 | 296 | 