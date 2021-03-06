# ARM-Linux-Toolchain
ARM 프로세서에서 동작하는 Linux 에서 실행할 C/C++ 프로그램을 빌드하기 위한 컴파일러 셋팅 방법 정리

## Windows : MinGW
### 툴체인 셋팅
다운로드 : wget   

위치 디렉터리 : /mingw64  

사용 Shell : msys
```bash
# 툴체인 다운로드
wget https://developer.arm.com/-/media/Files/downloads/gnu-a/9.2-2019.12/binrel/gcc-arm-9.2-2019.12-mingw-w64-i686-arm-none-linux-gnueabihf.tar.xz

# 압축 풀기
tar -xvf gcc-arm-9.2-2019.12-mingw-w64-i686-arm-none-linux-gnueabihf.tar.xz

# 툴체인 디렉터리 이동
mv gcc-arm-9.2-2019.12-mingw-w64-i686-arm-none-linux-gnueabihf /mingw64

# 해당 툴체인 환경변수에 추가
echo -e '\nexport PATH="/mingw64/gcc-arm-9.2-2019.12-mingw-w64-i686-arm-none-linux-gnueabihf/bin:$PATH"' >> ~/.bashrc

source ~/.bashrc
```

### CMake 셋팅 [검증 필요]
CMakeLists.txt
```cmake
set(CMAKE_C_COMPILER arm-none-linux-gnueabi-gcc)
set(CMAKE_CXX_COMPILER arm-none-linux-gnueabi-g++)
```

## macOS
### 툴체인 셋팅
다운로드 : wget   

위치 디렉터리 : /usr/local   

사용 Shell : zsh (bash 인 경우 마지막 echo에서 환경변수 추가를 .zshrc -> .bashrc로 변경)
```bash
# 툴체인 다운로드
wget https://github.com/thinkski/osx-arm-linux-toolchains/releases/download/8.3.0/arm-unknown-linux-gnueabi.tar.xz

# 압축 풀기
tar -xvf arm-unknown-linux-gnueabi.tar.xz

# 툴체인 디렉터리 이동
mv arm-unknown-linux-gnueabi /usr/local

# 해당 툴체인 환경변수에 추가
echo -e '\nexport PATH=/usr/local/arm-unknown-linux-gnueabi/bin:$PATH' >> ~/.zshrc

source ~/.zshrc
```

### CMake 셋팅
CMakeLists.txt
```cmake
set(ARM_LINUX_TOOLCHAIN_DIR /usr/local/arm-unknown-linux-gnueabi)
set(CMAKE_C_COMPILER ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-gcc)
set(CMAKE_CXX_COMPILER ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-g++)
set(CMAKE_LINKER ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-ld)
set(CMAKE_NM ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-nm)
set(CMAKE_OBJCOPY ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-objcopy)
set(CMAKE_OBJDUMP ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-objdump)
set(CMAKE_RANLIB ${ARM_LINUX_TOOLCHAIN_DIR}/bin/arm-unknown-linux-gnueabi-ranlib)
include_directories(${ARM_LINUX_TOOLCHAIN_DIR}/arm-unknown-linux-gnueabi/sysroot/usr/include)

## macOS : warning: cannot find entry symbol arch_paths_first; 에러 대처
set(HAVE_FLAG_SEARCH_PATHS_FIRST 0)
set(CMAKE_C_LINK_FLAGS "")
set(CMAKE_CXX_LINK_FLAGS "")
```

## Ubuntu
### 툴체인 셋팅
다운로드 : apt-get   

위치 디렉터리 : /usr   

`sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi`    

참고 사이트 : [링크](https://blog.thinkbee.kr/linux/crosscompile-arm/)

### CMake 셋팅
CMakeLists.txt
```cmake
set(CMAKE_C_COMPILER arm-linux-gnueabi-gcc)
set(CMAKE_CXX_COMPILER arm-linux-gnueabi-g++)
```
