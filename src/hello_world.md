# Hello World

#### main.cpp

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

#### CMakeLists.txt

```sh
cmake_minimum_required(VERSION 3.10)

project(HelloWorld)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(hello main.cpp)
```

#### Compiling

```sh
mkdir build
cd build

cmake ..

cmake --build .

./hello
```