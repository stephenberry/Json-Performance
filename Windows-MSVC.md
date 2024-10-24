# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Windows 10.0.20348 using the MSVC 19.41.34123.0 compiler).  

Latest Results: (Oct 24, 2024)
#### Using the following commits:
----
| Jsonifier: [ced96ae](https://github.com/RealTimeChris/Jsonifier/commit/ced96ae)  
| Glaze: [9d6f9c4](https://github.com/stephenberry/glaze/commit/9d6f9c4)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1388.3 | 1.76143e+06 | 964914 | 1.69963e+06 | 99 | 1429.92 | 1.71019e+06 | 964914 | 1.65018e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 749.193 | 3.26405e+06 | 964790 | 3.14912e+06 | 98 | 1418.47 | 1.72398e+06 | 964790 | 1.66328e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 304.507 | 8.03063e+06 | 964790 | 7.74787e+06 | 297 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1030.35 | 2.37337e+06 | 650795 | 1.54458e+06 | 169 | 1151.42 | 2.12383e+06 | 650795 | 1.38218e+06 | 300 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 568.914 | 4.29837e+06 | 650671 | 2.79682e+06 | 94 | 1077.97 | 2.26854e+06 | 650671 | 1.47608e+06 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 209.049 | 1.16977e+07 | 650671 | 7.61135e+06 | 97 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1400.92 | 1.74557e+06 | 964914 | 1.68433e+06 | 97 | 1403.74 | 1.74207e+06 | 964914 | 1.68094e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 748.043 | 3.26906e+06 | 964790 | 3.15396e+06 | 99 | 1410.75 | 1.73342e+06 | 964790 | 1.67238e+06 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 83.8387 | 2.91678e+07 | 964790 | 2.81408e+07 | 97 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Windows-MSVC/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1023.02 | 2.39037e+06 | 650795 | 1.55564e+06 | 97 | 1151.25 | 2.12415e+06 | 650795 | 1.38239e+06 | 207 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 568.591 | 4.30079e+06 | 650671 | 2.7984e+06 | 184 | 1068.19 | 2.28931e+06 | 650671 | 1.48959e+06 | 227 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 56.867 | 4.30021e+07 | 650671 | 2.79802e+07 | 96 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1434.04 | 1.70526e+06 | 138774 | 236646 | 98 | 2000.94 | 1.22214e+06 | 138774 | 169602 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1028.54 | 2.37755e+06 | 138774 | 329942 | 99 | 1927.15 | 1.26893e+06 | 138774 | 176094 | 227 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 369.891 | 6.61117e+06 | 138482 | 915528 | 98 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 900.759 | 2.71484e+06 | 69037 | 187424 | 99 | 1449.32 | 1.68728e+06 | 69037 | 116485 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 698.791 | 3.49949e+06 | 69037 | 241594 | 99 | 1271.36 | 1.92346e+06 | 69037 | 132790 | 97 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 187.827 | 1.30194e+07 | 68745 | 895022 | 161 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1514.78 | 1.61436e+06 | 6661897 | 1.07547e+07 | 97 | 1164.82 | 2.09939e+06 | 6661897 | 1.39859e+07 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1093.25 | 2.23682e+06 | 6661897 | 1.49015e+07 | 99 | 1118.46 | 2.18642e+06 | 6661897 | 1.45657e+07 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 450.138 | 5.43257e+06 | 6661897 | 3.61912e+07 | 188 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 489.664 | 4.99404e+06 | 2090234 | 1.04387e+07 | 98 | 452.214 | 5.40767e+06 | 2090234 | 1.13033e+07 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 354.139 | 6.9052e+06 | 2090234 | 1.44335e+07 | 99 | 436.725 | 5.59946e+06 | 2090234 | 1.17042e+07 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 143.04 | 1.70959e+07 | 2090234 | 3.57345e+07 | 97 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2848.75 | 858412 | 1439556 | 1.23573e+06 | 98 | 2358.99 | 1.03664e+06 | 1439556 | 1.4923e+06 | 164 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1417.12 | 1.72562e+06 | 1439584 | 2.48418e+06 | 97 | 2394.93 | 1.02109e+06 | 1439584 | 1.46994e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 637.494 | 3.83598e+06 | 1425381 | 5.46773e+06 | 97 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1590.79 | 1.53723e+06 | 500293 | 769068 | 96 | 1635.57 | 1.49514e+06 | 500293 | 748010 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 714.954 | 3.42036e+06 | 500299 | 1.7112e+06 | 99 | 1309.67 | 1.8672e+06 | 500299 | 934160 | 171 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 231.368 | 1.05693e+07 | 494854 | 5.23026e+06 | 98 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1606.42 | 1.52228e+06 | 719230 | 1.09487e+06 | 98 | 2544.11 | 961207 | 719230 | 691329 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1068.38 | 2.28889e+06 | 719139 | 1.64603e+06 | 216 | 2396.6 | 1.02037e+06 | 719139 | 733787 | 184 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 296.46 | 8.24867e+06 | 604930 | 4.98987e+06 | 158 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1316.55 | 1.85743e+06 | 477797 | 887476 | 97 | 2412.2 | 1.01377e+06 | 477797 | 484377 | 175 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 849.285 | 2.87937e+06 | 477706 | 1.37549e+06 | 97 | 2036.27 | 1.20093e+06 | 477706 | 573692 | 162 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 212.152 | 1.15266e+07 | 425643 | 4.90624e+06 | 99 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 550.25 | 4.44419e+06 | 69037 | 306814 | 244 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 505.542 | 4.83722e+06 | 69037 | 333947 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 285.551 | 8.56384e+06 | 69037 | 591222 | 99 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1421.96 | 1.71975e+06 | 964914 | 1.65941e+06 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1277.06 | 1.91488e+06 | 964914 | 1.84769e+06 | 180 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2344.79 | 1.04291e+06 | 123050 | 128330 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1454.44 | 1.68135e+06 | 123050 | 206890 | 99 | 