# learn-opengl 
使用XCode搭建OpenGL开发环境
GLEW：由于 OpenGL 只是一种 标准/规范，并且是由驱动制造上在驱动中予以实现。OpenGL 的大多数函数在编译时（compile-time）是未知状态的，需要在运行时（run-time）来请求。GLEW 的工作就是获取所需的函数的地址，并储存在函数指针中供使用。（还有其他类似的：GLAD）

GLFW：是一个专门针对 OpenGL 的 C 语言库，提供了渲染物体所需的最低限度的接口。其允许用户创建 OpenGL 上下文，定义窗口参数以及处理用户输入，把物体渲染到屏幕所需的必要功能。（注意：OpenGL 并不规定窗口创建和管理的部分，这一部分完全交由 GLFW 来实现；还有其他类似的：GLUT 和 SDL等）

GLAD：是一个开源的库，功能跟 GLEW 类似。GLAD 使用了一个在线服务（能够告诉 GLAD 需要定义的 OpenGL 版本，并且根据这个版本加载所有相关的 OpenGL 函数）




#1.下载安装库文件

通过Homebrew工具安装

```shell
brew install
```
#2.安装glfw和glew库

```shell
brew install glfw
brew install glew
```
3.  生成配置glad

glad的配置与大多数的开源库有些不同
glad使用 在线服务，https://glad.dav1d.de/，告诉glad需要定义的OpenGL版本，
会根据这个版本加载所有的相关的函数
将语言(Language)设置为C/C++，
在API选项中，选择3.3以上的OpenGL(gl)版本。之后将模式(Profile)设置为Core，
并且保证生成加载器(Generate a loader)的选项是选中的。
现在可以先忽略拓展(Extensions)中的内容。都选择完之后，点击生成(Generate)按钮来生成库文件。

```
将两个头文件目录（glad和KHR）复制到/usr/local/include，并添加glad.c到工程中
```

#4. 配置路径
Xcode工程-Build Settings-Search Paths -Header Search Paths

Build Phases-Link Binary With Libraries
#5. 签名库

codesign -f -s "你的证书" /usr/local/lib/*.dylib

```shell
codesign -f -s "Apple Development: bin xie (36RT35CB23)" /usr/local/Cellar/glfw/3.3.8/lib/*.dylib
codesign -f -s "Apple Development: bin xie (36RT35CB23)" /usr/local/Cellar/glew/2.2.0_1/lib/*.dylib
```


/usr/local/opt/glew/lib/libGLEW.2.2.dylib





```cpp
#include <GL/glew.h>
#include <GLFW/glfw3.h>
```

#开发OpenGL简单功能
#opengl hello world

```cpp
#include <GL/glew.h>
#include <GLFW/glfw3.h>
#include <iostream>
using namespace std;

void init(GLFWwindow* window) { }

void display(GLFWwindow* window, double currentTime) 
    glClearColor(1.0, 0.0, 0.0, 1.0);
    glClear(GL_COLOR_BUFFER_BIT);
}

int main(void ) {
    if (!glfwInit()) {
        exit(EXIT_FAILURE);
    }

    GLFWwindow* window = glfwCreateWindow(600, 600, "OpenGL Demo", NULL, NULL);
    glfwMakeContextCurrent(window);

    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);

    
    if (glewInit() != GLEW_OK) {
        exit(EXIT_FAILURE);
    }
    glfwSwapInterval(1);
    init(window);

while (!glfwWindowShouldClose(window)) {
        display(window, glfwGetTime());
        glfwSwapBuffers(window);
        glfwPollEvents();
    }
    glfwDestroyWindow(window);
    glfwTerminate();
    exit(EXIT_SUCCESS);
}
```
