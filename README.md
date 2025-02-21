# mnist
A mnist demo app.


----------------------------------------------------------
## 改造为一个 PDM 项目
1. 使用 `pdm init` 初始化项目
```shell
pdm init
```
按照提示操作，完成项目初始化。可以看到在项目根目录下生成了 `pyproject.toml` 文件。

2. 设置国内镜像
在项目根目录下的 `pyproject.toml` 文件中添加如下内容：
```toml
[tool.pdm.repositories]
tuna = "https://pypi.tuna.tsinghua.edu.cn/simple/"
ustc = "https://pypi.mirrors.ustc.edu.cn/simple/"
aliyun = "https://mirrors.aliyun.com/pypi/simple/"
default = "https://pypi.org/simple"
```

3. 安装项目中用到的依赖
本项目中的依赖有 torch, torchvision, torchaudio, flask, Pillow。可以使用 `pdm add` 命令安装这些依赖。
```shell
pdm add torch torchvision torchaudio flask Pillow
```
可以看到 pyproject.toml 文件中多了一些内容，这些内容是 PDM 用来管理项目依赖的配置。
并且在项目根目录下生成了一个 `pdm.lock` 文件，这个文件记录了项目依赖的具体版本信息。

这两个文件是 PDM 项目的核心文件，用来管理项目依赖。需要加入到版本控制中，以便团队协作。比如 git 中


