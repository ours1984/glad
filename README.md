# glad

![badge](https://img.shields.io/badge/-c++-yellow?style=flat&logo=c)
![badge](https://img.shields.io/badge/-opengl-orij?style=flat&logo=opengl)
[![license](https://img.shields.io/github/license/xiaoqide/glad.svg)](LICENSE)
[![glad](https://img.shields.io/badge/glad-c++-brightgreen.svg?style=flat-square)](https://github.com/xiaoqide/opengl-note-code)

GL/GLES/EGL/GLX/WGL C/C++ Loader generated based on the official specs

## 目录

- [glad](#glad)
  - [目录](#目录)
  - [背景](#背景)
  - [安装](#安装)
  - [使用](#使用)
  - [贡献](#贡献)

## 背景

为了项目的纯粹性,把项目[opengl-note-code](https://github.com/xiaoqide/opengl-note-code)的glad依赖单独列出一个仓库

## 安装

直接git克隆就可以了.

```bash
git clone https://github.com/xiaoqide/glad.git 
```

## 使用

打开GLAD的[在线服务](http://glad.dav1d.de/)，将语言(Language)设置为C/C++，在API选项中，选择3.3以上的OpenGL(gl)版本。

之后将模式(Profile)设置为Core，并且保证选中了生成加载器(Generate a loader)选项。

扩展(Extensions)选中GL_ARB_point_sprite。都选择完之后，点击生成(Generate)按钮来生成库文件。

<https://glad.dav1d.de/#profile=core&language=c&specification=gl&loader=on&api=gl%3D3.3&extensions=GL_ARB_point_sprite>

```c
struct gladGLversionStruct {
    int major;
    int minor;
};

extern struct gladGLversionStruct GLVersion;

typedef void* (* GLADloadproc)(const char *name);

/*
 * Load OpenGL using the internal loader.
 * Returns the true/1 if loading succeeded.
 *
 */
int gladLoadGL(void);

/*
 * Load OpenGL using an external loader like SDL_GL_GetProcAddress.
 *
 * Substitute GL with the API you generated
 *
 */
int gladLoadGLLoader(GLADloadproc);

/**
 * WGL and GLX have an unload function to free the module handle.
 * Call the unload function after your last GLX or WGL API call.
 */
void gladUnloadGLX(void);
void gladUnloadWGL(void);
```

把 glad.h 替换掉任意的 gl.h or gl3.h 只能 include glad.h.

```c
    if(!gladLoadGL()) { exit(-1); }
    printf("OpenGL Version %d.%d loaded", GLVersion.major, GLVersion.minor);

    if(GLAD_GL_EXT_framebuffer_multisample) {
        /* GL_EXT_framebuffer_multisample is supported */
    }

    if(GLAD_GL_VERSION_3_0) {
        /* We support at least OpenGL version 3 */
    }
```

## 贡献

PRs 是可以接受的.
