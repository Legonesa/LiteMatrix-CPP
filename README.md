# LiteMatrix-CPP 🧮

A lightweight, zero-dependency C++ library for 2D matrix operations. Built originally to support custom Deep Learning frameworks, it provides essential linear algebra tools including dot products, axis-based concatenation, functional mapping, and smart weight initializations.

## 🚀 Features

* **Core Math:** Element-wise addition and robust dot product (matrix multiplication).
* **Matrix Manipulation:** Easy transposition, slicing (extracting sub-matrices), and axis-based concatenation (horizontal/vertical merging).
* **Functional Mapping:** Apply any C++ lambda function element-wise across the matrix using the `map()` method.
* **ML-Ready Initializations:** Built-in uniform randomizer and **Xavier (Glorot) Initialization** for neural network weights.
* **Flat-Array Architecture:** Uses a single 1D `std::vector` under the hood for cache-friendly 2D matrix storage.

## 💻 Usage

Just drop `Matrix.hpp` and `Matrix.cpp` into your project and include the header.

```cpp
#include <iostream>
#include "Matrix.hpp"

int main() {
    // Create a 2x3 matrix and a 3x2 matrix
    Matrix A(2, 3);
    Matrix B(3, 2);

    // Fill with random values [-0.1, 0.1]
    A.randomize();
    
    // Fill with Xavier initialization (fanIn=3, fanOut=2)
    B.randomizeXavier(3, 2);

    // Matrix Multiplication (Dot Product)
    Matrix C = A.multiply(B); // Results in a 2x2 matrix

    // Apply a function to all elements (e.g., multiply by 10)
    Matrix D = C.map([](double val) { return val * 10.0; });

    std::cout << "Resulting Matrix D:" << std::endl;
    D.print();
    return 0;
}
```

🛠️ API Reference

```Table
Method,Description
"Matrix(size_t rows, size_t cols)",Initializes a matrix of the given size with zeros.
randomize(),Fills the matrix with uniform random values between -0.1 and 0.1.
"randomizeXavier(fanIn, fanOut)",Fills the matrix using Xavier initialization.
multiply(const Matrix& target),Returns a new matrix that is the dot product of this and the target.
transpose(),Returns a new matrix with swapped rows and columns.
map(std::function func),Applies a lambda function to every element and returns the result.
"slice(r_off, c_off, r_take, c_take)",Extracts and returns a specific sub-matrix.
"concatenate(Matrix A, Matrix B, axis)",Merges two matrices vertically (axis=0) or horizontally (axis=1).
add(const Matrix& target),Performs element-wise addition.
print(),Prints the matrix to the console for debugging.
"at(r, c)",Returns a reference to the element at the specified row and column.
```

📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
