# 使用VSCODE打造自己的IDE

## Theme

颜值才是最大的生产力!

### Vscode Theme

配置IDE的第一件事就是提高颜值，我常用的两个主题：

- DokiTheme
- Gruvbox

<https://vscodethemes.com/>

### Terminal

#### Install zsh

```sh
sudo apt update
sudo apt install zsh -y
# Set zsh as the default shell: 
chsh -s $(which zsh)
```

#### Install Oh My Zsh

```sh
# 安装 Oh My Zsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
# 以上命令可能不好使，可使用如下两条命令
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh
bash ./install.sh
```

#### Install powerlevel10k

- 下载powerlevel10k:
  - Clone the repository:
  
    ```sh
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
    ```

  - Users in China can use the official mirror on gitee.com for faster download.
  
    ```sh
    git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k"
    ```

- 参见官方文档安装即可:
  - Install the recommended font. Optional but highly recommended.
    - Terminal.fontFamily="Cascadia code NF"
  - Install Powerlevel10k itself.  选择Manual安装

    ```sh
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
    echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
    ```

    中国用户可以使用以下命令：

    ```sh
    git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ~/powerlevel10k
    echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
    ```

  - Restart Zsh with exec zsh.
  - Type **p10k configure** if the configuration wizard doesn't start automatically.

#### Set Dircolors

download dir_colors,link it to ~/.dir_colors

```sh
ln -sr "$PWD/src/dir_colors" "~/.dir_colors"
```

add following snippet to .zshrc

```sh
test -r "~/.dir_colors" && eval $(dircolors ~/.dir_colors)
alias ls='ls --color=auto'
```

### Beauty has its own power

作为集美貌与实力于一身的最直接体现就是zsh + oh my zsh 组合下的目录跳转了。

#### Directory autojump

- 切换至最近路径
  - cd - enter，切换至前一个目录
  - cd - tab， 列出最近使用过的目录
    - 可输入数字、使用tab或是上下箭头选择要跳转的目录
  
    ```sh
    $ cd -<tab>  # cd -2 就跳转至iwiki                                                                                                                                                                                           ✔  09:49:47  
    1 -- ~
    2 -- ~/iwiki
    3 -- ~/workspace 
    ```

- 跳转最近历史目录
  - d 回车；输入数字 回车；
  
  ```sh
   $ d                                                                                                                                                                           ✔  12:09:25  
   0       ~/workspace/lib/GSL
   1       ~
   2       ~/workspace/lib
   3       ~/workspace
   4       ~/iwiki
   5       ~/mymooc
   $ 2 # 进入~/workspace/lib目录
  ```

- 跳转至匹配的目录(使用率最高的匹配目录)
  - 安装: 在.zshrc的plugins行z增加 plugins=(git z)即可
  - z 列出zsh启动以来的所有访问过的目录
  - z key 进入包含key使用频率最高的目录
  - z -l key; 列出访问过的且路径中包含key的目录
  
  ```shell
  $ z  # 列出zsh启动以来的所有访问过的目录                                                                                                                                                                                               ✔  09:52:01  
  36845      /home/felix/mymooc
  91360      /home/felix/workspace
  94911      /home/felix/workspace/lib
  237712     /home/felix/iwiki
  
  $ z iwiki # 进入/home/felix/iwiki目录
  $ z worksapce lib # 进入包含 workspace 和lib的目录
  ```

#### Beauty is cold

安装zsh后最让人烦恼的就是 **zsh: no matches found**

```sh
find . -name file.*                                                                                                                                                                               ✔  09:31:18  
zsh: no matches found: file.*
```

解决方法,用括号包裹通配符：

```sh
find . -name 'design_mode.*'                                                                                                                                                                       INT ✘  09:31:42  
./iwiki/file.md
# 或者使用noglob
noglob apt install linux-*
```

### Program Font

在wins下安装字体：

- Victor Mono thin
- Cascadia Code

## C++

作为IT民工家里只能放得下一台台式机，既要给娃玩游戏，还要照顾下老婆情绪，最后又还得做开发，WSL就是满足这一切的神器。

### Install WSL manually

- Win10 install WSL
  - <https://learn.microsoft.com/zh-cn/windows/wsl/install>
  - 访问MicroStore有问题可以参阅"旧版WSL手动安装步骤"安装wsl2
  - 安装完成后，重启电脑
- Win10 install Ubuntu
  - <https://learn.microsoft.com/en-us/windows/wsl/install-manual>
  - 找到Downloading distributions部分，然后点击相应的版本进行下载

    ```html
    Downloading distributions
    There are some scenarios in which you may not be able (or want) to, install WSL Linux distributions using the Microsoft Store. You may be running a Windows Server or Long-Term Servicing (LTSC) desktop OS SKU that doesn't support Microsoft Store, or your corporate network policies and/or admins do not permit Microsoft Store usage in your environment. In these cases, while WSL itself is available, you may need to download Linux distributions directly.
    
    If the Microsoft Store app is not available, you can download and manually install Linux distributions using these links:
    
    Ubuntu
    Ubuntu 24.04
    Ubuntu 22.04 LTS
    Ubuntu 20.04
    Ubuntu 20.04 ARM
    Ubuntu 18.04
    Ubuntu 18.04 ARM
    Ubuntu 16.04
    ...
    
    ```

  - 选择一个版本，比如Ubuntu 24.04 LTS
    - 会下载一个Ubuntu2204-221101.AppxBundle文件
  - 使用7z解压AppxBundle文件中对应架构的appx，比如机器架构为x86_64
    - 解压Ubuntu_2204.1.7.0_x64.appx
  - 继续使用7z解压Ubuntu_2204.1.7.0_x64.appx
    - 进入解压后目录，执行.\ubuntu.exe开始安装
  - 安装完成后会提示输入用户名和密码

### Ubuntu C++ dev-env

```sh
sudo apt update

# 安装编译器gcc,g++和调试器gdb
sudo apt install build-essential gdb 
gcc --version
g++ --version
gdb --version

# 安装CMake 是个一个开源的跨平台自动化建构系统
sudo apt install cmake
cmake --version
# cmake需要依赖ninja
sudo apt-get install ninja-build -y

# 测试框架
## 安装gtest(或boost.test)
sudo apt-get install libgtest-dev
## 编译gtest
cd /usr/src/gtest
sudo cmake .
sudo make
sudo cp *.a /usr/lib
```

### Vscode

#### Offline download Extension

25年后在官网已经无法直接点击离线下载插件，如果你只能在公司内网使用，通过如下地址下载插件：

```html
https://marketplace.visualstudio.com/_apis/public/gallery/publishers/{Publisher}/vsextensions/{VSextension}/{Version}/vspackage
```

以cpptools插件为例,下载地址如下：

```html
https://marketplace.visualstudio.com/_apis/public/gallery/publishers/ms-vscode/vsextensions/cpptools-extension-pack/1.3.1/vspackage
```

点击vscode已安装插件，Publishers 和VSexteions分别填写identifier中的前后两部分即可：

```html
Installation
Identifier
ms-vscode.cpptools-extension-pack  {Publisher}.{VSextension}
Version
1.3.1 {Version}
Last Updated
2025-03-01, 12:28:42
Size
10.55KB
```

打开vscode官网，点击插件查看插件信息：

```html
More Info
Version 1.3.1 
Released on 2020/9/9 04:28:11 
Last updated 
2025/2/25 02:58:04
Publisher Microsoft 
Unique Identifier ms-vscode.cpptools-extension-pack
```

## Extension

### C++ Dev Extension

- C/C++ Extension Pack
  - C++ Intellisense Microsoft
- CMake Microsoft
- 单元测试驱动工具
  - CTest
    - CMake自带单元测试驱动工具，无需单独安装
    - 测试失败后会在终端窗口显现哪一行失败，但不会自动跳转到失败行
  - C++ TestMate
    - 独立安装的vscode插件
    - 测试失败后可以自动跳转到失败行

### Extension Compatibility

- 将插件后缀vsix修改为zip, 打开压缩包中的文件**extesion/package.json**
- 搜索engines

  ```json
      "engines": {
          "vscode": "^1.93.0"
      }
  ```

### Editor Extension

- Vim
- Text Power Tools

### Markdown Extension

#### Recommended Extension for Markdown

- Markdown Extension Pack 一组markdown相关的插件
- markdownlint
- Draw.io Integration
- Markdown Table
- Markedown Snippets

#### Table Common Command

- 创建表格
  - 输入snippet **NxM** Markdown Snippet创建N*M列的表格
  - 输入表头 **|id|name|age|回车** markdown table 生成表格
- 插入表格
  - 右侧插入列 markdown table insert column to the right
  - 左侧插入列 markdown table insert column to the left
  - 向右移动列 markdown table move to right
  - 向左移动列 markdown table move to left
- 删除列
  - format表格后，选择vscode列模式进行清除某一列

### Big Module Extension

- DeepSeek R1
- Copilot

## HelloWorld

### 创建一个HelloWorld工程

ctrl+shift+p选择cmake quick start配置好,cmake即可开始工作啦。

```text
├── CMakeLists.txt
├── CMakePresets.json
├── build
├── main.cpp
├── quick_sort.h
└── unittest
    ├── CMakeLists.txt
    └── test_quick_sort.cpp
```

### 工程中的CMakeList

```cmake
cmake_minimum_required(VERSION 3.10)
project(HelloWorld)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(helloworld main.cpp quick_sort.h)


enable_testing()
# 包含测试目录
add_subdirectory(unittest)
```

### 测试用例目录的CMakeList

```cmake
# 添加 Google Test
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# 添加测试可执行文件
add_executable(TestQuickSort test_quick_sort.cpp)

# 链接主项目的库（如果需要）
target_link_libraries(TestQuickSort gtest gtest_main)

# 添加测试
add_test(NAME TestQuickSort COMMAND TestQuickSort)
```
