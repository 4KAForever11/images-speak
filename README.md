### ComfyUI文生图+ChatTTs生成音频+SadTalker让图片说话

让自己生成的虚拟人图片说话

[SadTalker-项目地址](https://github.com/OpenTalker/SadTalker?tab=readme-ov-file)

[SadTalker - 让照片说话安装教程](https://www.learnprompt.pro/zh-Hans/docs/ai-human-generators/sadtalker-speaking-photos/)

[ComfyUI项目地址](https://github.com/comfyanonymous/ComfyUI)

[ChatTTS_colab项目地址](https://github.com/6drf21e/ChatTTS_colab?tab=readme-ov-file)




本人笔记本配置对于跑这个来说不高，跑起来有点吃力(显卡3060 6G显存，16G运行内存)



使用的clip模型：`t5xxl_fp8_e4m3fn.safetensors`和`clip_l.safetensors`



使用的Flux模型：`flux1-schnell.safetensors`




### 生成模型Flux.1

Flux 模型总共有3个，分别是：`Flux Pro`、`Flux Dev`、`Flux Schnell`


1. `[pro]` 是最顶级的模型，但是只能通过 API 调用；
2. `[dev]` 是由`[pro]`提炼，开源但非商用，质量和效果与`[pro]`类似；
3. `[schnell]` 是经过蒸馏的 4 步模型，速度比 `[dev]` 快 10 倍，Apache 2 开源许可。



### 安装使用ComfyUI生成真实的图片

1. 下载最新版 ComfyUI： [官方下载](https://github.com/comfyanonymous/ComfyUI) ，下载后解压出来待用

   

2. 设置中文语言：[点击下载](https://github.com/AIGODLIKE/AIGODLIKE-ComfyUI-Translation)，中文语言包，将 ZIP 包解压到 ComfyUI\custom_nodes 目录中（英语好的可用跳过这一步）

   

3. 下载 Flux 模型：FLUX 模型有四个可选，FLUX.1 [dev] 、FLUX.1 [dev] fp8、FLUX.1 [schnell]、FLUX.1 [schnell] fp8；

- FLUX.1 [dev]：官方满配版，最低显存要求24G；[点击下载](https://huggingface.co/black-forest-labs/FLUX.1-dev/tree/main)

- FLUX.1 [dev] fp8：大佬优化[dev]后版本，最低12G显存可跑；[点击下载](https://huggingface.co/Kijai/flux-fp8/blob/main/flux1-dev-fp8.safetensors)

- FLUX.1 [schnell]：4步蒸馏模型，大多数显卡可跑。[点击下载](https://huggingface.co/black-forest-labs/FLUX.1-schnell/blob/main/flux1-schnell.safetensors)

- FLUX.1 [schnell] fp8：优化版本，适应更低的显卡配置[点击下载](https://huggingface.co/Kijai/flux-fp8/blob/main/flux1-schnell-fp8-e4m3fn.safetensors)

  

**不管你下载上面的哪个模型，都存放在这个：ComfyUI/models/unet/ 目录下**




4.下载 CLIP 模型：需下载 t5xxl_fp16.safetensors 或 t5xxl_fp8_e4m3fn.safetensors （建议选择fp8 版本，如果你显存超过 32G 可选择 fp16 版本）

还有 clip_l.safetensors 放到 ComfyUI/models/clip/ 目录中：[点击前往](https://huggingface.co/comfyanonymous/flux_text_encoders/tree/main)



5.下载 VAE 模型：[点击下载](https://huggingface.co/black-forest-labs/FLUX.1-schnell/blob/main/ae.safetensors) 存放至 ComfyUI/models/vae/ 目录



6.下载Lora 真人模型 [点击下载](https://pan.tuio.cc/s/KKYtL)，放到ComfyUI/models/loras目录



7.下载工作流 [点击下载](https://pan.tuio.cc/s/qE2fL)，使用的时候根据需要的版本选择工作流，打开了ComfyUI把工作流拖进去就可以使用



全部模型下载好，放到指定目录就可以在ComfyUI的文件根目录下运行cpu或者gpu的bat脚本来打开ComfyUI



打开之后把对应版本的工作流拖到ComfyUI的网页里面就会自动加载工作流



模型和我下载的一样的，这些选项和参数都和我一样就行

![show1](https://github.com/4KAForever11/images-speak/blob/main/tu/show1.png)



这里可以改生成图片的分辨率(也就是改宽度和高度)和一次要生成多少张图片(也就是改批次大小)

建议显存小于8G的分辨率不要设太高了



然后我们修改提示词让电脑给我们生成我们想要的图片就行了（提示词最好用英语，英语不好，中文翻译一下就好了）

这里我的提示词翻译过来就是：`这是一张高分辨率的照片，一个时尚的美女站在一个安静的图书馆里，她的皮肤晶莹剔透，匀称的脸，她的身材穿着柔软的针织毛衣和飘逸的裙子，她仔细阅读书架时的表情若有感触，她的姿势优雅而镇定`



英语：`This is a high-resolution photograph, a fashionable beauty with clear, dewy skin and a symmetrical face stands in a tranquil library, her figure adorned in a soft, cable-knit sweater and a flowing skirt, her expression thoughtful as she peruses the shelves, her posture elegant and poised,Young Asian woman.`





![show2](https://github.com/4KAForever11/images-speak/blob/main/tu/show2.png)



所有的设置都完成之后，点击右上角的【`添加提示词队列`】就开始文生图了，具体要跑多久出图主要还是看你的显卡给不给力了
