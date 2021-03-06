# Padma-Index
Index-as-code for Padma. 

```
TextIndex('Padma-Index.pkl').final_index['ཟུ་']
```
This will return a dictionary where each key is document id where the word is found, and the value is a list of location ids where in that document id the word appears. `location_id` is same as saying that a given word is the "nth token" in the entire text.

```
{260: [6282],
 400: [6535],
 457: [22705],
 475: [2979],
 492: [2246, 2465],
 539: [419],
 555: [7429],
 609: [339, 387, 1899, 1952, 3061],
 690: [3262],
 831: [194],
 845: [2770],
 906: [3071],
 1038: [926],
 1055: [6073],
 1163: [860],
 1192: [1153],
 1311: [10592],
 1349: [110],
 1398: [4139],
 1416: [7561],
 1515: [711, 4147, 5554],
 1517: [8082, 15035, 18565],
 1541: [645],
 1606: [11073],
 1621: [1416,
  1478,
  5105,
  5217,
  5233,
  5332,
  6055,
  10285,
  12397,
  18910,
  27802,
  32302,
  32322,
  32388,
  32394,
  32534,
  32557,
  32596,
  34280,
  34572],
 1706: [370],
 1783: [767, 819, 883, 942, 987, 1856, 1903],
 1805: [5329],
 1836: [11063],
 1863: [5716, 6266],
 1870: [688],
 1949: [99, 451],
 1956: [973, 975],
 2002: [1715],
 2034: [8174],
 2081: [1137, 2773, 2849, 2927],
 2164: [475],
 2191: [3904, 4018, 6241],
 2271: [10881],
 2306: [4538, 4737, 4854],
 2312: [4465],
 2315: [1123, 1499, 1542, 3246, 4198, 4347, 4644, 4792],
 2459: [2302],
 2697: [2762, 2763],
 2810: [6481],
 2877: [1492, 1835, 1860, 1885, 1911, 2392, 2750],
 3003: [1230, 7643],
 3041: [370]}
 ```
 
 ## Performance 

It takes less than a second to query a word from the index. Every query takes the same time to perform.

``` 
%timeit TextIndex('Padma-Index.pkl').final_index['ཟུ་']
855 ms ± 8.84 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
```
