# Code Concatenation

> This repository contains implementations of the following error-correcting codes: Reed-Solomon, Reed-Muller, BCH, and Repetition code.

## Structure

The project is structured in the following way:

* `ProductCode.ipynb`: Construct product code.
* `ConcatenatedCode.ipynb`: Construct concatenated code.
* `RS.ipynb`, `RM.ipynb`, `BCH.ipynb`, and `Repetition.ipynb`: Implementations of codes.

## Usage
Two examples are given:

### Product Code
An example of how to construct a product code is shown below:

```python

C = ProductCode(RSCode(n = 9, k = 5, q = 2**4), RSCode(n = 7, k = 3, q = n**4))
```

The code replies:

```python
Out[]:  "Preferred message data type is: int"
```

Define some message:
```python
m = [1, 2, 3, 4, 5, 6, 7]
c = C.Encoding(m, out = 'pol')
print("Codeword: ", c)
```

```python
Out[]:  Codeword: [0, z4 + 1, z4^2 + 1, z4^3 + 1, z4, z4^2 + z4 + 1, z4^3 + z4^2 + 1, z4^3, z4 + 1, z4^2 + z4, z4^3 + z4^2, z4^3 + z4 + 1, z4^2 + 1, z4^3 + z4, z4, z4^3 + z4, z4^3 + 1, z4^3 + z4^2 + z4 + 1, z4 + 1, z4^3, z4^3 + z4^2 + 1, z4^2 + z4, z4^3, z4^2 + z4 + 1, z4^3 + z4, z4 + 1, z4, 0, z4^2, z4^2 + z4, z4, z4^3 + z4, z4^3 + 1, z4^3 + z4^2 + z4 + 1, z4 + 1, z4^3 + z4, z4 + 1, z4, 0, z4^2, z4^3 + z4^2, z4^3 + z4^2 + z4 + 1, z4^3 + z4^2 + z4, z4, z4^3 + 1, z4^3 + z4^2, z4^2 + z4, 1, z4^3 + z4^2 + z4 + 1, z4^2 + z4 + 1, 1, z4^3 + z4^2 + 1, z4^2 + z4, z4 + 1, z4^3 + 1, z4^3 + z4^2 + z4, z4^3 + z4, z4^3 + z4 + 1, z4^3 + 1, z4^3 + z4^2 + 1, z4^2 + 1, z4^2 + z4, 0]
```

```python
d = C.Decoding(c, out = 'int')
print("Decoded word: ", d)
```

```python
Out[]:  Decoded word: [1, 2, 3, 4, 5, 6, 7, 0, 0, 0, 0, 0, 0, 0, 0]
```

### Concatenated Code
An example of how to construct a concatenated code is shown below:

```python

C = ConcatenatedCode(RSCode(n = 15, k = 7, q = 2**4), RMCode(r = 1, m = 3))
```

The code replies:

```python
Out[]:  "Preferred message data type is: int"
```

Define some message:
```python
m = [1, 2, 3, 4, 5, 6]
c = C.Encoding(m, out = 'bin')
print("Codeword: ", c)
```

```python
Out[]:  Codeword: '011010010110100111001100110000111010101010101010101010100011001101011010110000111001100110101010101010100000111110010110'
```

```python
d = C.Decoding(c, out = 'int')
print("Decoded word: ", d)
```

```python
Out[]:  Decoded word: [1, 2, 3, 4, 5, 6, 0]
```

### Error-Correcting Codes
Code functions:

#### Reed-Solomon
* `C = RSCode(n = 15, k = 7, q = 2**4)`:
An instance of the Reed-Solomon code class is created. The following inputs are given: The length `n`, the dimension `k`, and the (extension) field `q`. Furthermore, a vector of `n` code locators `alpha` can be given, but if not then the code generates it itself.

* `def Encoding(m, zeropad = True, out = 'bin', concatenated_dimension = None)`:
Encode with the Reed-Solomon code. The message `m` which is given as input can either be a list of integers less than `q = 2**4`, e.g. `m = [1,2,3,4,5,6,7]`, or it can be a string of bits, e.g. `m = '0001001000110100010101100111'`. 





