# OpenMP MD

## How to compile
```
g++ -std=c++11 -fopenmp OMP_MD_vector.cpp -o OMP_MD_vector
OMP_NUM_THREADS=4 ./OMP_MD_vector
```

## Basic MD

### OMP_MD_basic_v0
fully implemented **very bad performance**

### OMP_MD_basic_v1
update `calcVerlet` 

### OMP_MD_basic_v2
update `calcAccel`


## Neighborhood with vector

### OMP_MD_vector_v0
For comparison

### OMP_MD_vector_v1
fully implemented with omp parallel clause, not fine tuned.

### ~~OMP_MD_vector_v2~~ **deprecated** 
~~final version~~ 

data result: 

| L    | np   | 1    | 2    | 4    | 8    | 16   | 
|------|------|------|------|------|------|------|
|64    |64    |0.47878376|0.377148343|0.372746554|0.429837683|0.48495589|
|      |128   |1.847976344|1.134697654|0.956766383|0.777583345|0.782326381|
|      |256   |7.147095021|4.497076088|2.797208179|2.253166442|1.99271713|
|      |512   |28.783580862|18.124845884|9.618808516|5.965392881|4.243118874|
|128   |128   |1.334958096|0.894949861|0.704597455|0.613159713|0.698897277|
|      |256   |5.34482324|3.13247733|1.931456682|1.876773731|1.738029761|
|      |512   |20.84896922|12.898651051|7.098345956|4.590486369|3.499529336|
|      |1024  |82.101149166|48.91325651|25.131638661|14.020853522|8.535498132|
|256   |256   |4.531546642|2.318951403|1.86372693|1.681474746|1.633219584|
|      |512   |17.945409165|10.374174059|6.149046839|4.205575331|3.155660214|
|      |1024  |70.679522295|38.610905872|22.040908397|12.713775165|7.800162771|
|      |2048  |284.568302196|150.136077656|82.719277239|42.560098573|23.628369235|
|      |4096  |1142.414023005|598.999013|318.085554837|165.174650572|84.219420654|
|512   |512   |16.758234626|8.865179005|5.972666627|3.99665798|3.214189716|
|      |1024  |66.217876943|34.07163675|21.110742785|11.581873345|7.757724698|
|      |2048  |264.700392812|134.626257365|78.236059859|40.100275382|23.236195909|
|      |4096  |1063.977918004|539.174075036|297.234731589|147.946676395|78.995807392|
|      |8192  |4245.15053262|2117.964584861|1085.036455755|571.753400088|287.33511735|
|1024  |1024  |64.984694487|33.042102252|20.026664824|11.438993701|7.530271853|
|      |2048  |258.003763751|131.056341909|72.972602199|39.540227558|21.998210606|
|      |4096  |1022.870339486|535.39201369|283.309959015|149.127658804|74.83412329|
|      |8192  |4078.491357335|2068.315010458|1100.195738936|561.580696775|288.86252223|
|      |16384 |16275.190270335|8151.566852157|4245.007864962|2224.315245165|1104.189243976|
|2048  |2048  |248.9620306|142.777476727|70.305548958|37.959935229|21.133626077|
|      |4096  |999.576284011|526.986318189|264.257248414|139.202678692|73.488625578|
|      |8192  |3989.084080649|2004.025373987|1026.535528506|540.27385761|271.350939544|
|      |16384 |15956.605043583|8009.35156591|4105.448799259|2163.297445277|1115.042069256|
|4096  |4096  |989.24635456|528.498519729|265.0651471|139.134409949|73.805171212|
|      |8192  |3953.362561162|2009.290547843|1014.062948055|535.268092976|268.800710967|
|      |16384 |15786.834208298|7992.484435364|4057.701719598|2145.319107067|1073.528508838|


### OMP_MD_vector_v3
Fixed one bug related to R_skin and R_cut

**Current Best Version**

### OMP_MD_vector_v4
- update `calcVerlet` 
- result is not as good as v3 in test case with L=64


data result: 

| L    | np   | 1    | 2    | 4    | 8    | 16   | 
|------|------|------|------|------|------|------|
|64    |64    |0.506785037|0.295652716|0.319002619|0.385763155|0.486576568|
|      |128   |1.977147812|1.021618428|0.760413996|0.733175214|0.784183449|
|      |256   |7.306382144|3.928533154|2.962066957|2.210108851|2.038658813|
|      |512   |29.276682311|16.385037382|9.838938661|6.209994732|4.155843655|
|128   |128   |1.352274034|0.777367044|0.612694245|0.651532166|0.726285371|
|      |256   |5.399131853|2.776013731|2.267177614|1.878580524|1.753325561|
|      |512   |21.25110988|11.231072607|7.374935821|4.89072129|3.583031764|
|      |1024  |83.032846548|48.985310297|25.368781322|14.036479764|10.141467031|
|256   |256   |4.485056761|2.319454129|1.67216043|1.656345887|1.628592126|
|      |512   |17.828207894|10.094531742|6.07039808|4.144745074|3.289291419|
|      |1024  |70.295610124|37.821852505|22.238756474|12.522260055|7.96842978|
|      |2048  |281.506270643|147.598716083|82.048225645|42.542208464|23.185949435|
|      |4096  |1137.035540188|589.549559442|317.025973113|163.481036477|81.091181349|
|512   |512   |16.672079669|8.919584556|5.887238361|4.132886622|3.17456318|
|      |1024  |65.832386151|33.943139384|20.569584806|11.992980949|8.085177755|
|      |2048  |262.688670443|133.160469413|76.913320035|40.028582701|22.356181304|
|      |4096  |1055.896753354|536.23546213|292.694154654|147.319025305|78.620892373|
|      |8192  |4215.739040826|2102.84481782|1104.481657181|568.269153397|285.351445798|
|1024  |1024  |62.814925593|38.259848629|19.181522082|11.341846623|7.478571489|
|      |2048  |251.330056241|145.043421733|72.950991124|38.109563675|21.448406363|
|      |4096  |1012.27655291|529.203709982|274.574573288|141.248545263|76.534629355|
|      |8192  |4038.891010684|2029.546905649|1046.653753832|548.741688213|276.89280493|
|      |16384 |16154.790299643|8100.503812699|4148.206483733|2226.026998357|1099.792672448|
|2048  |2048  |248.661316799|127.710626662|72.514989143|39.206727846|21.741784484|
|      |4096  |991.659812765|511.794148111|276.222156812|143.592718274|74.983002722|
|      |8192  |3966.715195467|2018.570345983|1090.025111502|553.103875206|276.750435104|
|      |16384 |15852.624674657|8068.622062656|4294.804373887|2202.606316682|1106.040732883|
|4096  |4096  |983.215294772|523.438548534|260.227621013|137.596517189|72.798548853|
|      |8192  |3929.200540298|1968.56657284|1004.003723189|532.074934922|266.993326665|
|      |16384 |15712.500965424|7873.289721252|4039.527978634|2128.106883133|1065.829052463|

