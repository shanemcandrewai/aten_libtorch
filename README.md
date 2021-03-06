# PyTorch ATen minimal build from prebuilt libraries
This CMakeLists.txt manages the building of a simple C++ program based on the ATen tensor library and libtorch built from [PyTorch 1.7](https://github.com/pytorch/pytorch/tree/v1.7.0)
## Simple C++ program : `aten_min.cpp` adapted from [PYTORCH C++ API](https://pytorch.org/cppdocs/)
    #include <ATen/ATen.h>

    int main() {
      at::Tensor a = at::ones({2, 2}, at::kInt);
      at::Tensor b = at::randn({2, 2});
      auto c = a + b.to(at::kInt);
    }
## Prerequisites
1. Clone [PyTorch 1.7](https://github.com/pytorch/pytorch/tree/v1.7.0) and adjust the [CMakeLists.txt](CMakeLists.txt) variable `PYTORCH_SRC_DIR` to point to the local repository, for example `set(PYTORCH_SRC_DIR ../pytorch)`
2. Install the [PyTorch prerequisites](https://github.com/pytorch/pytorch/tree/1.6#from-source)
3. Build libtorch, see [pytorch_setup](https://github.com/shanemcandrewai/pytorch_setup) for an example
## Usage
### Copy required files from `PYTORCH_BUILD_DIR` and generate the project buyldsystem
    cmake -S . -B build
### Build the project
    cmake --build build
### Execute
#### GCC
    ./build/aten_libtorch
#### MSVC
    build\[CMAKE_BUILD_TYPE]\aten_libtorch.exe
### Example
    cmake -DCMAKE_CXX_FLAGS=-Og -DCMAKE_BUILD_TYPE=Debug -S . -B build
    cmake --build build
    ./build/aten_libtorch
#### Cmake options
##### CMAKE_BUILD_TYPE 
The default build type is `Release`. For a debug build pass option `-D CMAKE_BUILD_TYPE=Debug`
##### CMAKE_CXX_FLAGS
###### GCC
`-Og` enables optimizations that do not interfere with debugging
##### LINK_SHARED_LIBS 
###### GCC
The default build links against shared libraries. For a static build pass option `-D LINK_SHARED_LIBS=0`
### Cleaning / trouble-shooting
#### Linux
    rm build/CMakeCache.txt
    rm -rf build
    diff --color=always -u file1 file2 | less -r
#### Windows
    del build/CMakeCache.txt
    rmdir /s /q build
    mklink /d build d:\build
#### Clean PyTorch source without using standard ignore rules
    git clean -dfx
