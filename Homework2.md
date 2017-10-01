### 1.

|Xi|Code 1|Code 2|Code 3|Code 4|
|:---:|:---:|:---:|:---:|:---:|
|X1|0|0|0|00|
|X2|10|01|01|01|
|X3|110|001|011|10|
|X4|1110|0010|110|110|
|X5|1111|0011|111|111|

_prefix free_ code : 1, 4



### 2.
  a) <br>
  b)

|title|_s<sub>1</sub>_|_s<sub>2</sub>_|_s<sub>3</sub>_|_s<sub>4</sub>_|_s<sub>5</sub>_|_s<sub>6</sub>_|_s<sub>7</sub>_|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|_c(x)_|00|01|100|101|110|1110|1111|
|_p(x)_|0.25|0.25|0.125|0.125|0.125|0.0625|0.0625|
|      |   |   |   |   |   |0\ |/1 |
|      |   |   |   |   |   |0.125|   |
|      |0\ | /1|0\ | /1|0\ |/1 |   |
|      |0.5|   |0.25|   |0.25|   |   |
|      |   |   |0\ |   |/1 |   |   |
|      |   |   |   |0.5|   |   |   |
|      |0\ |   |   |/1 |   |   |   |
|      |   |1.0|   |   |   |   |   |

c) <br>
L = 0.25 * 2 + 0.25 * 2 + 0.125 * 3 + 0.125 * 3 + 0.125 * 3 + 0.0625 * 4 + 0.0625 * 4 <br>
  = 0.5 + 0.5 + 0.375 + 0.375 + 0.375 + 0.25 + 0.25 <br>
  = 2.625
  
d) <br>
H = (0.25 * log<sub>2</sub>(1/0.25)) * 2 + (0.125 * log<sub>2</sub>(1/0.125)) * 3 + (0.0625 * log<sub>2</sub>(1/0.0625)) * 2 <br>
  = (0.25 * 2) * 2 + (0.125 * 3) * 3 + (0.0625 * 4) * 2 <br>
  = 2.625

### 3.
- source: abcabcabcabcabcabcabcabcabcabcabcabc
- encode:

|Current|Next|Output|Add to dictionay|Comments|
|:---:|:---:|:---:|:---:|:---|
|a 97|b 98|a 97|ab 256|'ab' not exist, add it to table|
|b 98|c 99|b 98|bc 257|'bc' not exist, add it to table|
|c 99|a 97|c 99|ca 258|'ca' not exist, add it to table|
|ab 256|c 99|ab 256|abc 259|'abc' not exist, add it to table|
|ca 258|b 98|ca 258|cab 260|'cab' not exist, add it to table|
|bc 257|a 97|bc 257|bca 261|'bca' not exist, add it to table|
|abc 259|a 97|abc 259|abca 262|'abca' not exist, add it to table|
|abca 262|b 98|abca 262|abcab 263|'abcab' not exist, add it to table|
|bca 261|b 98|bca 261|bcab 264|'bcab' not exist, add it to table|
|bcab 264|c 99|bcab 264|bcabc 265|'bcabc' not exist, add it to table|
|cab 260|c 99|cab 260|cabc 266|'cabc' not exist, add it to table|
|cabc 266|a 97|cabc 266|cabca 267|'cabca' not exist, add it to table|
|abc 259|-|abc 259|-|end|

- code: 97, 98, 99, 256, 258, 257, 259, 262, 261, 264, 260, 266, 259.
