# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Darwin 23.6.0 using the AppleClang 15.0.0.15000309 compiler).  

Latest Results: (Oct 24, 2024)
#### Using the following commits:
----
| Jsonifier: [ced96ae](https://github.com/RealTimeChris/Jsonifier/commit/ced96ae)  
| Glaze: [9d6f9c4](https://github.com/stephenberry/glaze/commit/9d6f9c4)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (Apple M1 (Virtual)), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2118.38 | 492876 | 232667 | 94 | 2397.94 | 492876 | 205542 | 263 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1570.11 | 492817 | 313875 | 164 | 2464.86 | 492817 | 199938 | 299 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 768.7 | 492817 | 641104 | 169 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1293.16 | 255669 | 197708 | 98 | 1803.92 | 255669 | 141730 | 206 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1050.09 | 255610 | 243417 | 204 | 1852.25 | 255610 | 138000 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 426.742 | 255610 | 598980 | 98 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2073.45 | 492876 | 237708 | 97 | 2374.36 | 492876 | 207583 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1585.47 | 492817 | 310834 | 161 | 2472.32 | 492817 | 199334 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 335.907 | 492817 | 1.46713e+06 | 96 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/MacOS-GNUCXX/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1258.42 | 255669 | 203166 | 99 | 1818.62 | 255669 | 140584 | 93 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1054.33 | 255610 | 242438 | 300 | 1824.97 | 255610 | 140062 | 259 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 180.936 | 255610 | 1.41271e+06 | 97 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2939.07 | 132014 | 44917 | 98 | 2462.74 | 132014 | 53604.5 | 297 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1973.07 | 138774 | 70334 | 95 | 3550.75 | 138774 | 39083 | 290 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1738.73 | 138482 | 79645.5 | 97 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1727.9 | 62277 | 36042 | 99 | 1857.85 | 62277 | 33521 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1351.47 | 69037 | 51083 | 212 | 2521.9 | 69037 | 27375 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 928.46 | 68745 | 74042 | 96 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3262.1 | 6661880 | 2.04221e+06 | 96 | 1637.95 | 6661880 | 4.06721e+06 | 169 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 3090.44 | 6661897 | 2.15565e+06 | 96 | 2314.38 | 6661897 | 2.87848e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1172.26 | 6661897 | 5.68296e+06 | 96 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1080.2 | 2090234 | 1.93504e+06 | 204 | 999.574 | 2090234 | 2.09112e+06 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1066.57 | 2090217 | 1.95975e+06 | 96 | 771.321 | 2090217 | 2.70992e+06 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 370.02 | 2090234 | 5.64898e+06 | 158 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 4433.64 | 1420981 | 320500 | 98 | 3186.5 | 1420981 | 445938 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2977.3 | 1439584 | 483520 | 99 | 4164.66 | 1439584 | 345666 | 94 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 2060.71 | 1425624 | 691812 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 3051.26 | 481718 | 157875 | 224 | 2076.19 | 481718 | 232020 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1615.93 | 500299 | 309604 | 173 | 2354.81 | 500299 | 212458 | 94 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 811.497 | 495097 | 610104 | 181 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 2584.2 | 524969 | 203146 | 192 | 2730.07 | 524969 | 192292 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2465.44 | 719139 | 291688 | 98 | 4306.22 | 719139 | 167000 | 95 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1548.24 | 659130 | 425729 | 98 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2081.69 | 477706 | 229480 | 97 | 3864.79 | 477706 | 123604 | 155 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1684.38 | 283536 | 168333 | 94 | 2270.94 | 283536 | 124854 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1046.18 | 425143 | 406375 | 292 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 909.878 | 69037 | 75875 | 198 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 626.663 | 69037 | 110166 | 96 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 490.059 | 69037 | 140875 | 300 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | -------------------- | --------------- | --------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 1329.1 | 492848 | 370812 | 162 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1270.7 | 492848 | 387854 | 98 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | ------------------- | -------------- | -------------------- |   
| [glaze](https://github.com/stephenberry/glaze/commit/9d6f9c4) | 2211.11 | 118385 | 53541 | 97 | 
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/ced96ae) | 1906.85 | 118385 | 62084 | 97 | 