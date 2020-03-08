# ARM-Linux-Toolchain
ARM 프로세서에서 동작하는 Linux 에서 실행할 C/C++ 프로그램을 빌드하기 위한 컴파일러 셋팅 방법 정리

### Windows : MinGW
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

### macOS
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

### Ubuntu
다운로드 : apt-get   

위치 디렉터리 : /usr   

`sudo apt-get install -y gcc-arm-linux-gnueabi g++-arm-linux-gnueabi`    

참고 사이트 : [링크](https://blog.thinkbee.kr/linux/crosscompile-arm/)

