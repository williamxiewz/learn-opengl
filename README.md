# learn-opengl 

使用xCode搭建OpenGL开发环境
下载安装库文件
创建xCode工程，与第三方库文件链接
开发OpenGL简单功能
1、安装GLFW，和GLEW库
通过Homebrew工具安装

再安装glfw和glew库


Xcode工程-Build Settings-Search Paths -Header Search Paths

Build Phases-Link Binary With Libraries

#include <GL/glew.h>
#include <GLFW/glfw3.h>




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

