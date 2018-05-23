how to compile shared libraries with cmake

## download code
```
git clone https://github.com/lukaspospisil/cmake_shared_library.git
cd cmake_shared_library
```

## compile library with cmake

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
./myexample
```
## compile library without cmake

```
mkdir build
cd build
mkdir lib
c++ -shared -fPIC ../src/myfunctions.cpp -I../include
c++ -fPIC -shared -o lib/libmysamplelibrary.so a.out
```

