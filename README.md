# installing_cuda_pytorch_cpp
How to install cuda and pytorch cpp on Ubuntu

1. Use sudo add-apt-repository ppa:graphics-drivers/ppa
2. sudo apt update
3. Download the latest driver (should show up in the Software Update 3rd party drivers app on Ubuntu)
4. Check release notes for cuda toolkit - check driver and cuda toolkit compatibility - https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html
5. Reboot after installing latest driver and if new drivers from ppa are not showing up
6. Add nvcc to path using (need to change version to the correct ones, from https://askubuntu.com/questions/885610/nvcc-version-command-says-nvcc-is-not-installed):  export PATH="/usr/local/cuda-8.0/bin:$PATH" and  export LD_LIBRARY_PATH="/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH"
7. Now you should be able to do nvcc --version
8. Go to https://pytorch.org/get-started/locally/ and get the C++ Cuda version (this will get a libtorch directory). Make sure CUDA driver matches
9. Unzip the libtorch to a directory
10. In VSCode, need to set up `c_cpp_properties.json` file. Need to have `includePath` and `browse` set up. Add something like `"/home/julian/tools/libtorch"`
11. Get something like the cofig file below
12. Set up CMAKE and CMakeLists.txt using `CMAKE_PREFIX_PATH`, add the TorchConfig.cmake which is located at `...../libtorch/share/cmake/Torch/TorchConfig.cmake`
```
{
    "version": 4,
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}",
                "/home/julian/tools/libtorch"
            ],
            "cStandard": "c11",
            "cppStandard": "c++17",
            "browse": {
                "path": [
                    "${workspaceFolder}",
                    "/home/julian/tools/libtorch"
                ]
            }
        }
    ]
}
```
