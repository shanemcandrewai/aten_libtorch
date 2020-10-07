# PyTorch ATen minimal build example 

This CMakeLists.txt manages the building of a simple C++ program based on the ATen tensor library and libtorch built from [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6)

## Simple C++ program : `aten_min.cpp` adapted from [PYTORCH C++ API](https://pytorch.org/cppdocs/)

    #include <ATen/ATen.h>

    int main() {
      at::Tensor a = at::ones({2, 2}, at::kInt);
      at::Tensor b = at::randn({2, 2});
      auto c = a + b.to(at::kInt);
    }

## Prerequisites

1. Clone [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6) 
2. Install the [PyTorch prerequisites](https://github.com/pytorch/pytorch/tree/1.6#from-source)
3. Build with `tools\build_libtorch.py`, see [aten_libtorch](https://github.com/shanemcandrewai/aten_libtorch) for an example. Next adjust the [CMakeLists.txt](CMakeLists.txt) variables `PYTORCH_SRC_DIR` and `LIBTORCH_SRC_DIR` to point to the local repositories.


## Usage
### Restore, preprocess, generate the project buildsystem and redirect output to file

    cmake -S . -B build

#### Cmake options

##### RESET

This restores the PyTorch source working tree from HEAD and changes some of the CMake scripts and header files to allow building as a suddirectory. This can be enabled by passing the option `-D RESET=1`.

##### DEBUG

The build has debugging information by default. This can be disabled by passing the option -D DEBUG=0.

### Build the project

    cmake --build build

### Execute

    ./build/aten_min