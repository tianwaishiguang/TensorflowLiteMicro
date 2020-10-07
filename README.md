# Tensorflow Lite Micro

## 1、介绍

本软件包是针对RT-Thread内核的Tensorflow Lite嵌入式推理框架Tensorflow Lite Micro软件包. 通过软件包可以实现在嵌入式系统中实现基于Tensorflow Lite框架训练的深度学习模型的端测部署任务.

### 1.1 目录结构

| 名称 | 说明 |
| ---- | :--- |
| docs  | 文档目录 |
| examples | Tensorflow Lite Micro自带语音历程, 并给出一些说明 |
| fixedpoint | Tensorflow Lite Micro库需要的定点量化库 |
| flatbuffers | Tensorflow Lite Micro库需要的模型解释库flatbuffer |
| ruy | Tensorflow Lite Micro库需要的矩阵加速库ruy |
| tensorflow | Tensorflow Lite Micro主体库 |

### 1.2 许可证

Tensorflow Lite Micro package 遵循 LGPLv2.1 许可，详见 `LICENSE` 文件。

### 1.3 依赖

RT-Thread 3.0+

## 2、如何打开 Tensorflow Lite Micro

使用 hello package 需要在 RT-Thread 的包管理器中选择它，具体路径如下：

```
RT-Thread online packages
    miscellaneous packages --->
        [*] Tensorflow Lite Micro package
```

然后让 RT-Thread 的包管理器自动更新，或者使用 `pkgs --update` 命令更新包到 BSP 中。

## 3、使用 Tensorflow Lite Micro

在打开 Tensorflow Lite Micro package 后:

- 将`packages/TensorflowLiteMicro_xxx`(其中`xxx`为软件包版本号)更改为`packages/TensorflowLiteMicro`,
- 通过menuconfig进行自定义功能配置, 其中menuconfig中的配置选项为:

```
RT-Thread online packages
    miscellaneous packages --->
        [*] Tensorflow Lite Micro package
            Enable Tensorflow Lite Micro
            Select Offical Example(Enable Tensorflow Lite Micro aduio example)
```

Select Offical Example中有三个选项:

```
(X) Enable Tensorflow Lite Micro audio example
( ) No Tensorflow Lite Micro example
```

其中audio example是执行官方携带的语音demo, No example则是不集成example文件, 只使用Tensorflow Lite Micro标准框架.(关于menucofing选项的注意事项请参照4. 注意事项部分!)

- Tensorflow Lite Micro结构比较复杂, 所以请先参考[introduction.md](introduction.md), 然后通过[user-guide.md](user-guide.md)来学习基本的部署结构, 在此基础之上再考虑自定义开发的问题.

*  API 手册可以访问这个[链接](docs/api.md), 其中提供了目前支持算子的情况
* 更多文档位于 [`/docs`](/docs) 下，使用前 **务必查看**

## 4、注意事项

- 如果在menuconfig中选择了audio example选项则工程自带了main函数, 需要手动删除除了`packages/TensorflowLiteMicro/example/audio_main.cc`以外的所有main函数
- 如果选择的是no example时, 系统没有main函数, 需要用户手动添加一个main函数,  
- 本软件包在运行时会占用16KB内存, 同时自带的语音识别案例在运行时总共占用22KB内存, 需要通过menuconfig来修改主函数栈的大小以及内存管理算法 ! ! !
- 本软件包目前只在树莓派4平台上实现成功运行, 其他平台还有待测试.

* 

## 5、联系方式 & 感谢

* 维护：QingChuanWS
* 主页：https://github.com/QingChuanWS
