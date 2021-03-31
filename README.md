# SkottieWrapper
Skottie can only be linked statically on the windows platform. If you use SkottieWrapper, you don’t need to directly link the Skottie library and allow C language projects to use Skottie indirectly.Of course you can also use it on non-Windows platforms

## Build
### Requirments
- [Python 2](https://www.python.org)
- [LLVM](https://llvm.org/)
- [CMake](https://cmake.org/)
- Proxy tool(Optional in some countries and regions)

### Build Step
#### windows  
```bash
git clone https://github.com/xspeed1989/SkottieWrapper.git
cd SkottieWrapper
git submodule init
git submodule update
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE="Release"\
  -DPYTHON2_DIR="F:\\Software\\Python27\\"\
  -DLLVM_DIR="F:\\Software\\LLVM"\
  -DCMAKE_INSTALL_PREFIX="E:\\SkottieWrapper"\
  -G "NMake Makefiles"\
  ..
nmake Build_Skia
nmake && nmake install
```

## Known Issues
Only the release version can be compiled on Windows

## Projects using SkottieWrapper
- [wangwenx190/qtlottie](https://github.com/wangwenx190/qtlottie)
 
## Third Party
- [Skia](https://www.skia.org)