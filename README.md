how to compile shared libraries with cmake

## download code
```
git clone https://github.com/lukaspospisil/cmake_shared_library.git
cd cmake_shared_library
```

## compile library

```
mkdir build
cd build
cmake ..
make
```

## compile example which uses library
```
cd ..
cd examples
mkdir build
cd build
cmake ..
make
```
