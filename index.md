# Welcome to Mengyuan Li's Emscripten Product Series Website

## If you want to download all the code for these labs,[click here](https://github.com/MengyuanL/CS7345-Lab-Mengyuan-Li).

## Lab1 Emscripten installation and 2 programs(Hello World and algor)

### Emscripten installation

#### Step1（Preparation work）:

Install git, CMake, Python, Visual Studio 2019 and configure environment variables. Here are some configuration screenshots if they are installed successfully.

Git:
[![1.png](https://i.postimg.cc/NfxVdBhX/1.png)](https://postimg.cc/4mmBdCx4)

Cmake and python:
[![2.png](https://i.postimg.cc/9fxwb4bk/2.png)](https://postimg.cc/McQGKph0)

System environment variables(git and CMake)
[![3.png](https://i.postimg.cc/2ySHJBNB/3.png)](https://postimg.cc/47jbHydJ)

User environment variables(python)
[![4.png](https://i.postimg.cc/pdMsvStv/4.png)](https://postimg.cc/DS5rdBZp)

#### Step2: Download Emscripten SDK

Create a new folder called “Emscripten SDK”, click the right button and then click “Git Bash here”. Enter “git clone https://github.com/emscripten-core/emsdk.git” to download the Emscripten SDK. After this, enther “cd emsdk” to enther the emsdk folder. 

[![6.png](https://i.postimg.cc/yWqZRwjY/6.png)](https://postimg.cc/T591MNBZ)

#### Step3: Installing and configuring emscripten

Enter “git pull” to fetch the latest registry of available tools. Enter “./emsdk install latest” to download and install the latest SDK tools.

[![7.png](https://i.postimg.cc/Fstp3q7L/7.png)](https://postimg.cc/MXD18906)

#### Step4: Activate the sdk

Enter “./emsdk activate latest” to make the "latest" SDK "active" for the current user. Enter “source ./emsdk_env.sh” to activate path and other environment variables in the current terminal. Finally enter “emcc -v” to verify whether emscripten has been installed successfully.

[![8.png](https://i.postimg.cc/VkJNw7WK/8.png)](https://postimg.cc/hXqnb1wm)
[![9.png](https://i.postimg.cc/Jn5rxSRz/9.png)](https://postimg.cc/ZB0zK79G)














