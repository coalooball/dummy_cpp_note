# 编写 Python 内置模块

# ChatGPT

#### 简单的示例

###### 提问

使用 C++ 编写一个 Python 内置模块示例

###### 回答

下面是一个简单的 C++ 编写的 Python 扩展模块示例,实现了一个简单的加法函数:

```cpp
// example.cpp
#define PY_SSIZE_T_CLEAN
#include <Python.h>

// 实现加法的C++函数
static PyObject* add_numbers(PyObject* self, PyObject* args) {
    int a, b;
    
    // 解析Python传入的参数
    if (!PyArg_ParseTuple(args, "ii", &a, &b)) {
        return NULL;
    }
    
    // 返回计算结果
    return PyLong_FromLong(a + b);
}

// 模块方法定义
static PyMethodDef ExampleMethods[] = {
    {"add", add_numbers, METH_VARARGS, "Add two numbers."},
    {NULL, NULL, 0, NULL}  // 结束标记
};

// 模块定义结构体
static struct PyModuleDef examplemodule = {
    PyModuleDef_HEAD_INIT,
    "example",   // 模块名
    NULL,        // 模块文档
    -1,          // 模块状态
    ExampleMethods
};

// 模块初始化函数
PyMODINIT_FUNC PyInit_example(void) {
    return PyModule_Create(&examplemodule);
}
```

要编译这个模块，还需要一个setup.py文件:

```py
# setup.py
from setuptools import setup, Extension

module = Extension('example',
                  sources=['example.cpp'])

setup(name='example',
      version='1.0',
      description='Example module written in C++',
      ext_modules=[module])
```

编译和安装步骤:

```sh
python setup.py build
python setup.py install
```

使用示例:
```py
import example
result = example.add(5, 3)  # 返回 8
print(result)
```



# Tips

#### 在 VSCode 中为 C/C++ 项目设置 include 路径

c_cpp_properties.json

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/include",
                "/usr/local/include",
                "/path/to/your/include"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}
```