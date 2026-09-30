# Ollama自定义安装位置

[blog原文](https://www.cnblogs.com/LaiYun/p/18696931)
**<font style="color:rgb(51, 102, 255);background-color:rgb(255, 255, 240);">手动创建Ollama安装目录</font>**
<font style="color:rgb(51, 51, 51);background-color:rgb(255, 255, 240);">在CMD窗口输入：</font>
**<font style="color:rgb(51, 102, 255);background-color:rgb(255, 255, 240);">OllamaSetup.exe /DIR=E:\MySoftware\Ollama</font>**
**<font style="color:rgb(255, 0, 0);background-color:rgb(255, 255, 240);">语法：软件名称 /DIR=这里放你上面创建好的Ollama指定目录</font>**
**<font style="color:rgb(255, 0, 0);background-color:rgb(255, 255, 240);"></font>**

# <font style="background-color:rgb(255, 255, 240);">设置大模型位置</font>

右键图标
点击setting
选择模型下载位置
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752033585567-c9f077c8-b72d-4a30-b677-7ba8c37fafc3.png" width="38" alt="" title="" crop="0,0,1,1" id="u81022c74" class="ne-image">
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752033599558-cf7a03f5-7637-4f7d-8592-65bf7273c3c4.png" width="642" alt="" title="" crop="0,0,1,1" id="ucb3ceeba" class="ne-image">

# <font style="color:rgb(0, 0, 0);">Potplayer视频字幕生成与翻译</font>

[参考](https://funglearn.top/00720250307-2/)

## 下载地址

<font style="color:rgb(0, 0, 0);">Potplayer播放器： </font>[<font style="color:rgb(46, 46, 46);">https://potplayer.tv/</font>](https://potplayer.tv/)
<font style="color:rgb(0, 0, 0);">Potplayer插件（开源）：</font>[<font style="color:rgb(46, 46, 46);">https://github.com/Fung-2025/potplayer-translation-openaiapi</font>](https://github.com/Fung-2025/potplayer-translation-openaiapi)
<font style="color:rgb(0, 0, 0);">Ollama：</font>[<font style="color:rgb(46, 46, 46);">https://ollama.com/</font>](https://ollama.com/)
<font style="color:rgb(0, 0, 0);">Ollama 模型地址：</font>[<font style="color:rgb(46, 46, 46);">https://ollama.com/search</font>](https://ollama.com/search)
<font style="color:rgb(46, 46, 46);"></font>
<font style="color:rgb(46, 46, 46);"></font>

## 下载大模型

用的是qwen3:8b(硅基流动上说API免费)（但是我们其实是本地部署，不需要花钱）

### 修改ollama模型路径

<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752052756459-67d7c0e5-29b6-4833-b83b-e67c05b96882.png" width="653" alt="" title="" crop="0,0,1,1" id="u82668559" class="ne-image">
<font style="color:rgb(0, 0, 0);">打开终端输入：</font>
```bash
ollama run qwen3:8b
```
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752036746737-5aa2b70e-4d02-4986-a2fc-06a467f0604c.png" width="979" alt="" title="" crop="0,0,1,1" id="u8baf4bb5" class="ne-image">
等待下载完成
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752046497143-6099a521-5050-4379-ab86-39b3c72d2736.png" width="864" alt="" title="" crop="0,0,1,1" id="ub2d2cd33" class="ne-image">
下载完成
但是要翻译字幕的话需要关闭思考流，下面是关闭思考流的尝试。
## 通过修改modified文件关闭思考流
### 修改配置文件
输入
```plain
ollama show qwen3:8b --modelfile
```
<font style="color:#117CEE;">复制文件内容到证书前一行</font>
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752046711839-b95c0139-b4e6-44bc-8e19-5331154e3eaa.png" width="904" alt="" title="" crop="0,0,1,1" id="ud1094314" class="ne-image">
<font style="color:#117CEE;">找到{{- if eq .Role "user" }}<|im_start|>user这一行</font>
<font style="color:#117CEE;">然后在其下一行的开头添加 (注意后面要添加空格)</font>
```plain
/nothink 
```
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752046897302-88e69cbf-2c84-4d36-87bd-4cdb714872fe.png" width="390" alt="" title="" crop="0,0,1,1" id="uce5f40e1" class="ne-image">
<font style="color:#117CEE;">然后将蓝色部分内容删除</font>
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752047819930-565a5272-07b8-488c-80b7-06229d9be618.png" width="457" alt="" title="" crop="0,0,1,1" id="u9f7de1b5" class="ne-image">
<font style="color:#117CEE;">保存，重命名为Modelfile</font>
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752047034473-4891d297-fd9c-4451-8b19-f6c02938a2f4.png" width="111" alt="" title="" crop="0,0,1,1" id="ud7f9e0cf" class="ne-image">
### 根据内容重新生成模型
<font style="color:#117CEE;">保存到一个文件夹里，复制路径</font>
```plain
D:\Desktop\MyTemp
```
<font style="color:#117CEE;">打开CMD</font>
输入
```plain
ollama create myqwen3 -f "D:\Desktop\MyTemp\Modelfile"
```
其中
myqwen3是自定义的模型名字
-f 选项
双引号中是刚才复制的路径+Modelfile
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752047472565-b2c97f47-6d40-491c-9eae-686d1bb0806f.png" width="696" alt="" title="" crop="0,0,1,1" id="u5443e674" class="ne-image">
创建完成
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752047512103-7ee9abec-f667-4eb2-b435-87396c013247.png" width="713" alt="" title="" crop="0,0,1,1" id="ub22397a0" class="ne-image">
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752047535676-9db178a5-c956-4964-be8c-af469d8a1728.png" width="493" alt="" title="" crop="0,0,1,1" id="u3d9a8ae6" class="ne-image">
删除模型的命令是
```plain
ollama rm （modelname）
```
测试： 
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752048131139-4d0c6567-b8eb-49b4-88f1-63ee791c6f67.png" width="713" alt="" title="" crop="0,0,1,1" id="u00a1d47d" class="ne-image">
发现没有思考流了
**<font style="color:rgb(0, 0, 0);">安装插件</font>**
<font style="color:rgb(0, 0, 0);">将插件文件复制至：</font>
```plain
potplayer安装位置 \DAUM\PotPlayer\Extension\Subtitle\Translate
```
# 字幕生成
打开potplayer
右键选择 字幕->生成有声字幕->选择whip，下载好模型后，点击开始，等待字幕生成完成。
# 启用实时翻译
## 启动Ollama本地服务
输入命令 
```plain
ollama serve
```
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752049724874-b34aa058-7ee5-4798-ac68-44b2315761c1.png" width="693" alt="" title="" crop="0,0,1,1" id="u5dc3e65b" class="ne-image">
<font style="color:#DF2A3F;">注意</font>
需要关闭本地打开的ollama app
就是那个图标点击退出
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752033585567-c9f077c8-b72d-4a30-b677-7ba8c37fafc3.png" width="38" alt="" title="" crop="0,0,1,1" id="LekEP" class="ne-image">
输入Curl地址
<font style="color:rgb(0, 0, 0);">用&隔开：（Model&API URL）</font>
```plain
myqwen3:latest&http://localhost:11434/v1/chat/completions
```
**<font style="color:rgb(0, 0, 0);">以ollama本地模型为例</font>**
**<font style="color:#1DC0C9;">Ollama文档</font>**[<font style="color:#1DC0C9;">：</font>](https://ollama.com/blog/openai-compatibility)
[<font style="color:#117CEE;">https://ollama.com/blog/openai-compatibility</font>](https://ollama.com/blog/openai-compatibility)
**<font style="color:rgb(0, 0, 0);">ModelAPI URL：</font>**
```plain
myqwen3:latest&http://localhost:11434/v1/chat/completions
```
**<font style="color:rgb(0, 0, 0);">（注意使用&隔开）</font>**
**<font style="color:rgb(0, 0, 0);">API key：</font>**
```plain
ollama
```
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752052817513-d2f72bbc-d7bb-4fd3-89a2-28893d510ff8.png" width="441" alt="" title="" crop="0,0,1,1" id="u985373f4" class="ne-image">
成功
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752052827315-2d564ddb-b847-4718-9846-c9860505a3ee.png" width="391" alt="" title="" crop="0,0,1,1" id="u13722785" class="ne-image">
成功
<img src="https://cdn.nlark.com/yuque/0/2025/png/38785100/1752052945983-ffc97038-ec64-4dc2-9f4b-dcb194454405.png" width="646" alt="" title="" crop="0,0,1,1" id="u89b3ec32" class="ne-image">
