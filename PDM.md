# PDM

PDM（Python Dependency Management）

https://pdm-project.org/zh-cn/latest/usage/project/

## 快速入门
### 1. 什么是 PDM？

PDM（Python Development Master）是一个现代的 Python 包管理工具，类似于 `pip` 和 `poetry`，它的设计目标是简化依赖管理，支持 PEP 517 和 PEP 518 标准，并且基于 PEP 660 提供了 PEP 517 构建系统的原生支持。相比其他工具，PDM 强调可重复性、版本锁定以及更好的性能。

### 2. 安装 PDM

首先，你需要安装 PDM。使用以下命令可以快速安装：

```bash
pip install pdm
```

或者，如果你使用的是 Mac 或 Linux，也可以用 Homebrew 安装：

```bash
brew install pdm
```

安装完成后，可以通过以下命令验证安装是否成功：

```bash
pdm --version
```

### 3. 创建一个新的项目

进入你的项目目录，并运行以下命令来初始化一个新的 Python 项目：

```bash
pdm init
```

PDM 会引导你完成一些简单的配置，选择项目的 Python 版本、包管理工具等。

### 4. 管理依赖

你可以使用 PDM 来管理项目的依赖包。安装依赖的基本命令如下：

```bash
pdm add <package-name>
```

比如，你要安装 `requests` 库：

```bash
pdm add requests
```

如果你需要安装开发依赖，可以使用 `-d` 参数：

```bash
pdm add -d pytest
```

### 5. 生成 `pyproject.toml`

PDM 使用 `pyproject.toml` 文件来存储项目的元数据、依赖项和构建配置。你可以通过 `pdm init` 或手动编辑该文件。

例如：

```toml
[tool.pdm]
dependencies = [
    "requests >=2.25.0",
]

[build-system]
requires = ["pdm-backend"]
build-backend = "pdm.buildapi"
```

`pyproject.toml` 文件是 PDM 和其他工具的核心配置文件。

### 6. 锁定依赖版本

PDM 会自动生成一个 `pdm.lock` 文件，该文件锁定了项目的所有依赖版本。这确保了团队成员之间安装的依赖版本一致，避免了因依赖版本不同导致的兼容性问题。

如果你想更新所有依赖，使用：

```bash
pdm update
```

### 7. 使用虚拟环境

PDM 会自动为每个项目创建虚拟环境，避免了系统级的依赖冲突。你可以查看当前虚拟环境路径：

```bash
pdm venv info
```

### 8. 多环境支持

PDM 支持多环境（例如：开发、测试、生产等）。你可以为不同的环境安装不同的依赖：

```bash
pdm add <package> --dev
pdm add <package> --prod
```

通过 `pyproject.toml` 中的 `optional-dependencies` 来管理。

### 9. 发布你的包

当你的项目准备好发布时，PDM 也有集成的功能来打包并发布到 PyPI 或其他仓库。你可以使用以下命令来构建和发布：

```bash
pdm build
pdm publish
```

### 10. 常用命令总结

- `pdm init`: 初始化一个新的 Python 项目。
- `pdm add <package-name>`: 安装一个依赖包。
- `pdm add -d <package-name>`: 安装开发依赖。
- `pdm update`: 更新所有依赖。
- `pdm remove <package-name>`: 移除某个依赖包。
- `pdm venv info`: 查看虚拟环境信息。
- `pdm build`: 构建项目包。
- `pdm publish`: 发布项目包。

### 11. 进阶功能（可选）

- **插件支持**：PDM 支持插件，可以通过插件扩展功能，例如集成 `pytest`、`black` 等工具。
- **版本控制**：你可以指定依赖的版本范围，甚至可以从 GitHub 上拉取私有仓库的代码。

### 总结

PDM 是一个现代、灵活且高效的 Python 包管理工具，它使得项目的依赖管理更加简洁和可重复。掌握了 PDM 的基础用法后，你就能够高效地管理 Python 项目的依赖、虚拟环境和版本锁定。


## 从 github 上下载了一个 Python 项目，它已经有了 pyproject.toml ，该如何着手？
当你从 GitHub 上下载一个已有 `pyproject.toml` 文件的 Python 项目时，你可以按照以下步骤来开始你的开发工作，确保项目依赖正确安装并正常运行。

### 步骤 1: 安装 PDM

首先，确保你已经安装了 PDM。如果尚未安装，可以使用以下命令安装：

```bash
pip install pdm
```

或者，如果你使用 Homebrew（适用于 macOS 或 Linux）：

```bash
brew install pdm
```

### 步骤 2: 克隆并进入项目目录

如果你还没有将项目克隆到本地，先执行：

```bash
git clone <repository-url>
cd <project-directory>
```

### 步骤 3: 使用 PDM 安装依赖

在项目目录中，`pyproject.toml` 文件已经包含了项目的依赖信息。你可以使用 PDM 安装所有依赖：

```bash
pdm install
```

PDM 会自动创建一个虚拟环境并安装 `pyproject.toml` 中列出的所有依赖。如果你查看虚拟环境的路径，可以使用以下命令：

```bash
pdm venv info
```

这将显示你项目的虚拟环境位置。

### 步骤 4: 激活虚拟环境（可选）

虽然 PDM 会自动处理虚拟环境，你可以手动激活虚拟环境以确保你在正确的环境中工作。如果你想直接进入虚拟环境，可以运行：

```bash
pdm run
```

或者进入虚拟环境后运行 Python：

```bash
pdm run python
```

### 步骤 5: 运行项目或测试

项目依赖安装完成后，通常你会看到项目的入口脚本或者测试配置。例如，如果项目有测试，可以运行以下命令来执行测试：

```bash
pdm run pytest
```

如果有入口脚本，例如 `main.py`，你可以直接运行：

```bash
pdm run python main.py
```

### 步骤 6: 开始开发

一切准备好后，你可以开始进行开发，修改代码，添加功能或修复 bug。如果需要安装额外的开发依赖（如 `pytest` 或 `black`），可以使用以下命令：

```bash
pdm add -d pytest black
```

### 步骤 7: 提交更改并推送

开发完成后，提交你的更改并推送到 GitHub：

```bash
git add .
git commit -m "Add feature/fix bug"
git push origin <branch-name>
```

### 步骤 8: 使用 PDM 进行构建和发布（可选）

如果你准备将项目发布到 PyPI 或其他包管理平台，可以使用以下命令构建和发布项目：

- 构建项目包：

  ```bash
  pdm build
  ```

- 发布到 PyPI：

  ```bash
  pdm publish
  ```

### 总结

1. 克隆项目并进入项目目录。
2. 使用 `pdm install` 安装所有依赖。
3. 使用虚拟环境进行开发（PDM 会自动处理）。
4. 运行项目或执行测试。
5. 提交代码并推送。
6. 如果需要，使用 PDM 进行构建和发布。

这些步骤将帮助你在下载一个有 `pyproject.toml` 文件的 Python 项目时快速开始开发和运行项目。如果你有其他问题或需要更详细的帮助，随时告诉我！


## 一些最佳实践
使用 PDM 时，有一些最佳实践可以帮助你更好地管理项目的依赖、提高开发效率以及保持项目的一致性。以下是一些推荐的最佳实践：

### 1. **使用 `pyproject.toml` 进行统一配置**

`pyproject.toml` 是 PDM 的核心配置文件，所有的项目依赖、构建系统等信息都存储在这个文件里。确保将所有必要的信息都写入 `pyproject.toml`，并且避免手动修改 `pdm.lock` 文件，PDM 会自动为你管理该文件。

- 使用 `[tool.pdm]` 作为项目的配置部分
- 配置 `dependencies`、`dev-dependencies`、`optional-dependencies`，确保依赖分离明确
- 保持项目元数据（如项目名称、版本、描述）更新

例如：

```toml
[tool.pdm]
name = "your_project"
version = "0.1.0"
description = "A description of your project"
dependencies = [
    "requests >=2.25.0",
]
dev-dependencies = [
    "pytest",
    "black",
]

[build-system]
requires = ["pdm-backend"]
build-backend = "pdm.buildapi"
```

### 2. **确保依赖版本锁定**

PDM 会生成一个 `pdm.lock` 文件，这个文件确保了依赖版本的锁定，并在团队之间保证一致性。**不要手动编辑 `pdm.lock` 文件**，而是通过 PDM 的命令来添加、更新或删除依赖。

- 使用 `pdm add <package>` 来添加依赖。
- 使用 `pdm update` 来更新依赖。
- 使用 `pdm remove <package>` 来删除不需要的依赖。

这样可以确保依赖版本在不同机器上保持一致，避免因为版本不同导致的潜在问题。

### 3. **在开发和生产环境中分离依赖**

在开发过程中，通常有些包只在开发环境中需要，比如 `pytest`、`black` 或 `mypy`，而不需要在生产环境中安装。这时，PDM 的 `dev-dependencies` 可以帮助你清晰地区分开发依赖和生产依赖。

例如，在 `pyproject.toml` 中配置：

```toml
[tool.pdm]
dependencies = [
    "requests >=2.25.0",
]

dev-dependencies = [
    "pytest",
    "black",
]
```

安装生产环境依赖时使用：

```bash
pdm install --prod
```

安装开发环境依赖时使用：

```bash
pdm install --dev
```

### 4. **避免全局安装依赖，使用虚拟环境**

PDM 会自动为每个项目创建虚拟环境，因此，不需要担心依赖污染系统环境。确保你总是在项目的虚拟环境中工作，而不是全局安装依赖。

- 使用 `pdm venv info` 查看当前虚拟环境的信息。
- 确保你的 IDE（如 VSCode）指向正确的虚拟环境。

### 5. **使用 `pdm` 管理多个 Python 版本**

PDM 支持通过 `pyproject.toml` 配置多版本支持，如果你的项目支持多个 Python 版本，确保在文件中明确声明支持的版本范围。

```toml
[tool.pdm]
python = ">=3.7,<3.11"
```

你可以使用 `pdm` 配合 `pyenv` 或其他工具来管理不同的 Python 版本，这样你可以确保项目在不同版本的 Python 下都能顺利运行。

### 6. **定期更新依赖**

为了避免依赖版本过时导致的安全隐患和兼容性问题，定期更新项目中的依赖是很重要的。可以使用 `pdm update` 来更新所有依赖，或者单独更新某个依赖：

```bash
pdm update <package-name>
```

### 7. **使用 PDM 的插件系统扩展功能**

PDM 支持插件，可以安装并配置各种功能来增强项目的管理和开发体验。比如：

- `pdm-mypy`: 集成 `mypy` 进行类型检查。
- `pdm-black`: 集成 `black` 进行代码格式化。

例如，安装并配置 `black` 插件：

```bash
pdm plugin add black
```

在 `pyproject.toml` 中配置 `black`：

```toml
[tool.black]
line-length = 88
```

### 8. **正确使用版本控制**

确保将 `pyproject.toml` 和 `pdm.lock` 文件纳入版本控制。这样可以保证团队成员在不同的机器上安装相同版本的依赖。

不要将虚拟环境文件夹（通常是 `.venv`）和 `__pycache__` 等临时文件加入版本控制。你可以通过 `.gitignore` 忽略这些文件夹。

```gitignore
.venv/
__pycache__/
```

### 9. **使用 PDM 的构建和发布功能**

当项目完成并准备发布时，PDM 提供了简便的构建和发布工具。例如，使用以下命令生成分发包：

```bash
pdm build
```

然后可以使用 `pdm publish` 将包发布到 PyPI：

```bash
pdm publish
```

确保在发布之前，已经通过 `pdm build` 生成了正确的包。

### 10. **文档化依赖管理流程**

确保团队成员了解如何使用 PDM 管理项目的依赖。如果你使用的是 CI/CD 流程，确保配置好相关的 PDM 安装和依赖安装步骤。比如，可以在 `.github/workflows` 或 `gitlab-ci.yml` 等文件中配置：

```yaml
steps:
  - name: Set up Python
    uses: actions/setup-python@v2
    with:
      python-version: "3.8"
  
  - name: Install dependencies
    run: |
      pip install pdm
      pdm install
```

### 总结

PDM 是一个强大的工具，遵循这些最佳实践可以帮助你更高效地管理项目的依赖，保持代码的一致性和可维护性。如果你习惯了这些做法，PDM 将成为你日常开发中不可或缺的工具。

## 国内源
在中国使用 PDM 时，由于访问 PyPI 等国外源可能较慢，因此配置国内镜像源可以显著提升依赖安装的速度。PDM 允许你通过配置文件指定使用国内的镜像源。

### 1. 配置国内镜像源

你可以在 `pyproject.toml` 文件中指定 PDM 使用的国内源。常见的国内镜像源有：

- **清华大学**: `https://pypi.tuna.tsinghua.edu.cn/simple/`
- **中国科技大学**: `https://pypi.mirrors.ustc.edu.cn/simple/`
- **阿里云**: `https://mirrors.aliyun.com/pypi/simple/`

#### 配置方法：

打开你的 `pyproject.toml` 文件，并在 `[tool.pdm]` 部分中添加 `index-url` 字段来指定镜像源。

例如，配置使用阿里云镜像源：

```toml
[tool.pdm]
name = "your_project"
version = "0.1.0"
description = "A description of your project"
dependencies = [
    "requests >=2.25.0",
]

# 设置国内镜像源
# 清华大学镜像源
[tool.pdm.repositories]
default = "https://pypi.tuna.tsinghua.edu.cn/simple/"
```

#### 其他镜像源配置示例：
- 中国科技大学镜像源：
```toml
[tool.pdm.repositories]
default = "https://pypi.mirrors.ustc.edu.cn/simple/"
```

- 阿里云镜像源：
```toml
[tool.pdm.repositories]
default = "https://mirrors.aliyun.com/pypi/simple/"
```

### 2. 临时使用国内源（命令行配置）

如果你不想修改 `pyproject.toml` 文件，你可以在使用 PDM 安装依赖时，通过 `PDM` 命令行临时指定国内镜像源。使用 `--repository` 选项：

例如：

```bash
pdm add <package-name> --repository https://mirrors.aliyun.com/pypi/simple/
```

### 3. 配置多个镜像源

你还可以配置多个镜像源，PDM 会按照顺序查找依赖。如果你希望配置多个源，可以按以下方式设置：

```toml
[tool.pdm.repositories]
tuna = "https://pypi.tuna.tsinghua.edu.cn/simple/"
ustc = "https://pypi.mirrors.ustc.edu.cn/simple/"
aliyun = "https://mirrors.aliyun.com/pypi/simple/"
default = "https://pypi.org/simple"
```

然后可以指定使用不同的源：

```bash
pdm add <package-name> --repository tuna
```

### 4. 配置全局镜像源（适用于所有项目）

如果你希望全局配置镜像源，可以修改 PDM 的配置文件。PDM 的配置文件通常位于用户的主目录下：`~/.config/pdm/config.toml`。

例如，在 `config.toml` 中添加如下配置来设置默认的国内镜像源：

```toml
[global]
repositories = [
    "https://pypi.tuna.tsinghua.edu.cn/simple",
    "https://pypi.mirrors.ustc.edu.cn/simple",
    "https://mirrors.aliyun.com/pypi/simple/",
    "https://pypi.org/simple"
]
```

### 5. 测试镜像源是否配置成功

配置完成后，你可以使用以下命令来安装依赖并测试是否能够从国内源成功下载：

```bash
pdm install
```

如果速度显著提高，说明国内镜像源已经成功配置。

### 总结

通过修改 `pyproject.toml` 文件或 `config.toml` 文件，你可以轻松地将 PDM 配置为使用国内镜像源，以提高依赖包安装的速度和稳定性。
