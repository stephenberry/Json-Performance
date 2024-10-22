# Json-Performance
Performance profiling of JSON libraries (Compiled and run on Linux 6.5.0-1025-azure using the Clang 20.0.0 compiler).  

Latest Results: (Oct 22, 2024)
#### Using the following commits:
----
| Jsonifier: [eb38d50](https://github.com/RealTimeChris/Jsonifier/commit/eb38d50)  
| Glaze: [65d45d5](https://github.com/stephenberry/glaze/commit/65d45d5)  
| Simdjson: [3c0d032](https://github.com/simdjson/simdjson/commit/3c0d032)  

 > At least 30 iterations on a (AMD EPYC 7763 64-Core Processor), until coefficient of variance is at or below 1%.


### Json Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1740.53 | 1.40499e+06 | 899801 | 1.26421e+06 | 172 | 1666.12 | 1.46774e+06 | 899801 | 1.32067e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1205.39 | 2.02875e+06 | 899678 | 1.82522e+06 | 99 | 1683.89 | 1.45225e+06 | 899678 | 1.30656e+06 | 297 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 715.357 | 3.6552e+06 | 899678 | 3.2885e+06 | 169 | 

### Json Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Json%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1384.32 | 1.76653e+06 | 609953 | 1.0775e+06 | 183 | 1327.32 | 1.84238e+06 | 609953 | 1.12377e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1056.88 | 2.45396e+06 | 609830 | 1.4965e+06 | 99 | 1428.01 | 1.8162e+06 | 609830 | 1.10757e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 503.368 | 5.1557e+06 | 609830 | 3.1441e+06 | 97 | 

### ABC Test (Out of Sequence Performance - Prettified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>

The JSON documents in the previous tests featured keys ranging from "a" to "z," where each key corresponds to an array of values. Notably, the documents in this test arrange these keys in reverse order, deviating from the typical "a" to "z" arrangement.

This test effectively demonstrates the challenges encountered when utilizing simdjson and iterative parsers that lack the ability to efficiently allocate memory locations through hashing. In cases where the keys are not in the expected sequence, performance is significantly compromised, with the severity escalating as the document size increases.

In contrast, hash-based solutions offer a viable alternative by circumventing these issues and maintaining optimal performance regardless of the JSON document's scale, or ordering of the keys being parsed.

| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1737 | 1.40785e+06 | 899801 | 1.26678e+06 | 99 | 1662.81 | 1.47067e+06 | 899801 | 1.32331e+06 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1206.54 | 2.02682e+06 | 899678 | 1.82349e+06 | 99 | 1683.16 | 1.45288e+06 | 899678 | 1.30712e+06 | 99 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 337.113 | 7.25406e+06 | 899678 | 6.52632e+06 | 99 | 

### ABC Test (Out of Sequence Performance - Minified) [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/Ubuntu-CLANG/JsonData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Abc%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1499.74 | 1.75207e+06 | 609953 | 1.06868e+06 | 97 | 1413.27 | 1.85927e+06 | 609953 | 1.13407e+06 | 98 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 992.821 | 2.46312e+06 | 609830 | 1.50208e+06 | 97 | 1324 | 1.84701e+06 | 609830 | 1.12636e+06 | 161 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 226.303 | 1.0806e+07 | 609830 | 6.58984e+06 | 98 | 

### Discord Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2242.26 | 1.09061e+06 | 138774 | 151348 | 161 | 2187.2 | 1.11807e+06 | 138774 | 155158 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1691.79 | 1.44547e+06 | 138774 | 200594 | 98 | 1859.4 | 1.31518e+06 | 138774 | 182512 | 165 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 409.127 | 6.41652e+06 | 47820 | 306838 | 255 | 

### Discord Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Discord%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 1934.01 | 1.26444e+06 | 69037 | 87293 | 99 | 1491.37 | 1.63973e+06 | 69037 | 113202 | 180 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1378.24 | 1.91069e+06 | 69037 | 131908 | 99 | 1564.67 | 1.68303e+06 | 69037 | 116192 | 173 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 191.559 | 1.27659e+07 | 23197 | 296132 | 97 | 

### Canada Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2459.7 | 994200 | 6661897 | 6.62326e+06 | 98 | 1536.12 | 1.59196e+06 | 6661897 | 1.06055e+07 | 170 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2255.02 | 1.08444e+06 | 6661897 | 7.22445e+06 | 98 | 1575.62 | 1.55204e+06 | 6661897 | 1.03396e+07 | 100 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 749.144 | 3.26431e+06 | 6661897 | 2.17465e+07 | 98 | 

### Canada Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CanadaData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Canada%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 827.951 | 2.9536e+06 | 2090234 | 6.17372e+06 | 97 | 616.677 | 3.9655e+06 | 2090234 | 8.28883e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 803.523 | 3.04339e+06 | 2090234 | 6.3614e+06 | 98 | 610.408 | 4.00623e+06 | 2090234 | 8.37396e+06 | 98 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 237.398 | 1.0301e+07 | 2090234 | 2.15315e+07 | 99 | 

### CitmCatalog Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 4569.74 | 709204 | 1439556 | 1.02094e+06 | 98 | 3531.5 | 917706 | 1439556 | 1.32109e+06 | 201 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 3256.83 | 995838 | 1439584 | 1.43359e+06 | 98 | 3283.46 | 987763 | 1439584 | 1.42197e+06 | 212 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1087.58 | 2.24852e+06 | 1426596 | 3.20772e+06 | 98 | 

### CitmCatalog Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/CitmCatalogData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/CitmCatalog%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3560.72 | 910180 | 500293 | 455356 | 166 | 2302.21 | 1.40773e+06 | 500293 | 704277 | 174 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 1975.3 | 1.64211e+06 | 500299 | 821546 | 188 | 2209.06 | 1.46834e+06 | 500299 | 734608 | 208 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 520.189 | 6.23105e+06 | 496069 | 3.09103e+06 | 97 | 

### Twitter Test (Prettified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Prettified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3673.68 | 882041 | 719230 | 634390 | 97 | 3738.14 | 866832 | 719230 | 623452 | 197 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2512.5 | 1.29036e+06 | 719139 | 927950 | 97 | 3367.5 | 962743 | 719139 | 692346 | 192 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 1380.82 | 2.34712e+06 | 757430 | 1.77778e+06 | 99 | 

### Twitter Test (Minified) Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/TwitterData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Twitter%20Test%20(Minified)_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- | ------------ | ------------------| -------------------- | ----------------| --------------------- |  
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 3651.5 | 887092 | 477797 | 423850 | 165 | 3343.52 | 968803 | 477797 | 462891 | 96 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2200.22 | 1.4738e+06 | 477706 | 704044 | 177 | 3433.35 | 944471 | 477706 | 451180 | 180 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 974.38 | 3.32644e+06 | 523443 | 1.7412e+06 | 180 | 

### Minify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Minify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 978.521 | 3.31495e+06 | 69037 | 228854 | 97 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 920.253 | 3.52504e+06 | 69037 | 243358 | 158 | 
| [simdjson](https://github.com/simdjson/simdjson/commit/3c0d032) | 542.927 | 5.9732e+06 | 69037 | 412372 | 294 | 

### Prettify Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Minified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Prettify%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Write (MB/S) | Write (Cycles/MB) | Write Length (Bytes) | Write Time (ns) | Write Iteration Count |
| ------- | ------------ | ------------------| -------------------- | --------------- | --------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 2293.62 | 1.41419e+06 | 899801 | 1.27249e+06 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2060.99 | 1.57372e+06 | 899801 | 1.41604e+06 | 183 | 

### Validation Test Results [(View the data used in the following test)](https://github.com/RealTimeChris/Json-Performance/blob/main/Json/DiscordData-Prettified.json):

----
<p align="left"><a href="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png" target="_blank"><img src="https://github.com/RealTimeChris/Json-Performance/blob/main/Graphs/Validate%20Test_Results.png?raw=true" 
alt="" width="400"/></p>


| Library | Read (MB/S) | Read (Cycles/MB) | Read Length (Bytes) | Read Time (ns) | Read Iteration Count |
| ------- | ----------- | -----------------| ------------------- | -------------- | -------------------- |   
| [jsonifier](https://github.com/realtimechris/jsonifier/commit/eb38d50) | 4755.56 | 682113 | 118385 | 80752 | 99 | 
| [glaze](https://github.com/stephenberry/glaze/commit/65d45d5) | 2282.31 | 1.42103e+06 | 118385 | 168229 | 99 | 