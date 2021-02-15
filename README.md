# dictionaries

Benchmarks for dictionary data structures: hash tables, maps, tries,
etc.

The `judy` package was removed from this test suite for instability;
it segfaults the program.

## Running

For all benchmarks:

    $ stack bench :space

For just space:

    $ stack bench :space

For just time:

    $ stack bench :time

## Insert Int keys space use

|Case|                                              Bytes|    GCs|
|---|---|---|
|Data.Map.Strict.insert mempty                        |64      |0  |
|Data.Map.Lazy.insert mempty                          |64      |0  |
|Data.HashMap.Strict.insert mempty                    |64      |0  |
|Data.HashMap.Lazy.insert mempty                      |48      |0  |

## Pure maps fromList space use

| Case                                     | Total bytes   | Max residency | Final live | GCs   |
|------------------------------------------|---------------|---------------|------------|-------|
| Data.Map.Strict.fromList     (1 million) | 1,016,187,152 | 55,394,296    | 31,864     | 1,942 |
| Data.Map.Lazy.fromList       (1 million) | 1,016,187,152 | 55,394,296    | 31,864     | 1,942 |
| Data.IntMap.Strict.fromList  (1 million) | 776,852,648   | 55,207,424    | 31,864     | 1,489 |
| Data.IntMap.Lazy.fromList    (1 million) | 776,852,648   | 55,207,424    | 31,864     | 1,489 |
| Data.HashMap.Strict.fromList (1 million) | 161,155,384   | 40,358,064    | 0          | 314   |
| Data.HashMap.Lazy.fromList   (1 million) | 161,155,384   | 40,358,064    | 0          | 314   |

## IO maps fromList space use

| Case                                          | Total bytes | Max residency | Final live | GCs |
|-----------------------------------------------|-------------|---------------|------------|-----|
| Data.HashTable.IO.BasicHashTable (1 million)  | 424,214,184 | 47,254,400    | 1,120      | 672 |
| Data.HashTable.IO.CuckooHashTable (1 million) | 173,581,848 | 1,328         | 1,328      | 244 |
| Data.HashTable.IO.LinearHashTable (1 million) | 281,294,784 | 22,373,256    | 0          | 545 |

<!-- RESULTS -->

## Insert Int (Randomized)

|Name|10|100|1000|10000|
|---|---|---|---|---|
|Data.Map.Lazy|584.9 ns|11.83 μs|200.3 μs|3.433 ms|
|Data.Map.Strict|639.1 ns|13.32 μs|224.0 μs|3.930 ms|
|Data.HashMap.Lazy|409.6 ns|5.415 μs|78.43 μs|2.897 ms|
|Data.HashMap.Strict|408.6 ns|5.411 μs|78.57 μs|2.474 ms|
|Data.IntMap.Lazy|202.0 ns|3.253 μs|47.61 μs|1.391 ms|
|Data.IntMap.Strict|242.7 ns|4.363 μs|63.32 μs|1.549 ms|

## IO Insert Int (Randomized)

|Name|10|100|1000|10000|
|---|---|---|---|---|
|Data.HashTable.IO.BasicHashTable|534.8 ns|4.949 μs|50.40 μs|625.1 μs|
|Data.HashTable.IO.LinearHashTable|910.8 ns|9.744 μs|105.4 μs|862.3 μs|
|Data.HashTable.IO.CuckooHashTable|919.2 ns|8.823 μs|88.42 μs|985.6 μs|
|Data.HashTable.IO.Swiss|400.9 ns|3.760 μs|40.03 μs|698.7 μs|

## Intersection (Randomized)

|Name|10|100|1000|10000|100000|1000000|
|---|---|---|---|---|---|---|
|Data.Map.Lazy|469.5 ns|5.864 μs|88.55 μs|966.7 μs|14.89 ms|170.1 ms|
|Data.Map.Strict|468.7 ns|5.859 μs|82.78 μs|917.4 μs|9.828 ms|100.5 ms|
|Data.HashMap.Lazy|165.1 ns|1.815 μs|26.12 μs|332.4 μs|3.834 ms|44.68 ms|
|Data.HashMap.Strict|164.6 ns|1.811 μs|25.92 μs|331.2 μs|3.844 ms|44.60 ms|
|Data.IntMap.Lazy|94.93 ns|0.634 μs|7.060 μs|178.4 μs|2.300 ms|28.53 ms|
|Data.IntMap.Strict|94.47 ns|0.637 μs|6.930 μs|179.9 μs|2.288 ms|28.63 ms|

## IO Intersection (Randomized)

|Name|10|100|1000|10000|100000|
|---|---|---|---|---|---|
|Data.HashTable.IO.BasicHashTable|324.7 ns|2.560 μs|37.39 μs|509.8 μs|8.260 ms|
|Data.HashTable.IO.LinearHashTable|323.7 ns|3.138 μs|34.12 μs|402.2 μs|10.80 ms|
|Data.HashTable.IO.CuckooHashTable|1078 ns|9.311 μs|91.33 μs|949.0 μs|14.44 ms|
|Data.HashTable.IO.Swiss|450.7 ns|5.483 μs|54.74 μs|650.4 μs|13.94 ms|

## Lookup Int (Randomized)

|Name|10|100|1000|10000|100000|1000000|
|---|---|---|---|---|---|---|
|Data.Map.Lazy|148.3 ns|2.380 μs|76.07 μs|1.491 ms|27.95 ms|592.3 ms|
|Data.Map.Strict|151.1 ns|2.494 μs|74.06 μs|1.481 ms|26.23 ms|551.6 ms|
|Data.HashMap.Lazy|218.0 ns|2.725 μs|34.16 μs|0.566 ms|11.83 ms|324.8 ms|
|Data.HashMap.Strict|217.4 ns|2.692 μs|33.77 μs|0.565 ms|11.82 ms|315.3 ms|
|Data.IntMap.Lazy|169.8 ns|2.531 μs|76.88 μs|1.396 ms|24.69 ms|595.9 ms|
|Data.IntMap.Strict|169.5 ns|2.542 μs|78.45 μs|1.400 ms|25.11 ms|665.0 ms|

## IO Lookup Int (Randomized)

|Name|10|100|1000|10000|100000|1000000|
|---|---|---|---|---|---|---|
|Data.HashTable.IO.BasicHashTable|26.23 ns|31.44 ns|25.50 ns|25.81 ns|25.09 ns|25.33 ns|
|Data.HashTable.IO.LinearHashTable|62.54 ns|69.90 ns|70.42 ns|62.45 ns|63.53 ns|142.3 ns|
|Data.HashTable.IO.CuckooHashTable|56.32 ns|56.59 ns|56.39 ns|55.98 ns|55.10 ns|55.70 ns|
|Data.HashTable.IO.Swiss|32.62 ns|61.90 ns|32.34 ns|32.04 ns|32.26 ns|32.13 ns|

## FromList ByteString (Monotonic)

|Name|10000|
|---|---|
|Data.Map.Lazy|4.679 ms|
|Data.Map.Strict|5.363 ms|
|Data.HashMap.Lazy|2.692 ms|
|Data.HashMap.Strict|2.696 ms|
|Data.Trie|11.34 ms|

## FromList ByteString (Randomized)

|Name|10|100|1000|10000|
|---|---|---|---|---|
|Data.Map.Lazy|698.7 ns|16.16 μs|324.9 μs|5.900 ms|
|Data.Map.Strict|729.7 ns|17.65 μs|345.0 μs|6.466 ms|
|Data.HashMap.Lazy|597.1 ns|8.432 μs|126.4 μs|3.245 ms|
|Data.HashMap.Strict|609.5 ns|8.403 μs|124.1 μs|3.273 ms|
|Data.Trie|1032 ns|19.06 μs|464.7 μs|18.48 ms|

## Lookup ByteString Monotonic

|Name|10000|
|---|---|
|Data.Map.Lazy|102.7 ns|
|Data.Map.Strict|101.9 ns|
|Data.HashMap.Lazy|39.01 ns|
|Data.HashMap.Strict|38.91 ns|
|Data.Trie|191.2 ns|

## Lookup ByteString Randomized

|Name|10000|
|---|---|
|Data.Map.Lazy|2.616 ms|
|Data.Map.Strict|2.570 ms|
|Data.HashMap.Lazy|0.923 ms|
|Data.HashMap.Strict|1.015 ms|
|Data.Trie|3.504 ms|

