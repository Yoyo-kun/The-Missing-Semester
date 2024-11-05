# The Missing Semester

****

## The Shell

### 终端提示符与用户信息

- **`UserName@MachineName:~$`**
  - 表示当前位置为：`~`
    - `~` 表示当前用户的主目录（home directory），一般为 `/home/用户名`
      - 例：使用相对路径写法 `cd ~/dev/`
  - `$` 表示当前身份不是 root 用户

### 基础命令

- **`echo`**：用于输出文本或变量的值到终端。
- **`\ `**：用于转义空格。
    - 例如，`echo Hello\ World` 与 `echo Hello World` 的区别在于：
        - Shell 是基于空格分隔命令进行解析的。
- **`$PATH`**：系统环境变量 `PATH`，用于按目录顺序查找可执行文件。
    - 使用 `echo $PATH` 来查看当前路径。

### 路径管理

- **路径分隔符**：
  - Linux 和 macOS 上使用 `/`，而在 Windows 使用 `\`。
  - 在 Linux 下，如果路径以 `/` 开头，则为绝对路径；反之为相对路径。
  - `.` 表示当前目录，`..` 表示上级目录。
    - 示例：`cd .`（进入当前目录），`cd ..`（返回上级目录）。
  - `~` 表示当前用户的主目录，通常为 `/home/用户名`。
    - 示例：`cd ~`（直接进入主目录）。
  - `-` 表示上次切换前的工作目录。
    - 示例：`cd -`（返回到上次的工作目录）。

### 常用文件与目录命令

- **`pwd`**：打印当前工作目录（print working directory）。
- **`clear`**或**`Ctrl + L`**：清屏，清除终端上所有输出。
- **`date`**：显示当前日期和时间。
- **`which`**：查询程序对应的地址，返回可执行文件的路径。
- **`cd`**：切换目录（change directory）。
  - 示例：`cd /home`（切换到 `/home` 目录）。
- **`ls`**：列出当前目录下的文件和子目录（list directory contents）。
  - 示例：使用 `ls --help` 查看帮助信息，输出关于 `ls` 命令的使用说明、可用选项和参数，以及如何使用这些选项的详细描述。
- **`ls -l`**：以长格式列出当前目录下的文件和目录，并显示详细信息。

#### `ls -l` 输出格式

|         列         | 描述                                                         |    示例拆分    |
| :----------------: | :----------------------------------------------------------- | :------------: |
| **文件类型和权限** | 包含 10 个字符，表示文件类型和权限。                         |  `drwxr-xr-x`  |
|    - 第一个字符    | 表示文件类型：`d` 为目录（directory），`-` 为普通文件（regular file），`l` 为符号链接（symbolic link）。 |      `d`       |
| - 接下来的九个字符 | 分为三组，每组三个字符，表示用户（owner）、用户组（group）和其他用户（others）的权限。 | `rwx r-x r-x`  |
|       - `r`        | 表示读权限（read）。                                         |      `r`       |
|       - `w`        | 表示写权限（write）。注意，如果你对一个文件拥有写权限，而对它的目录没有写权限，那么你可以随意改写该文件内容，但不能删除此文件。 |      `w`       |
|       - `x`        | 表示执行权限（execute）。                                    |      `x`       |
|      硬链接数      | 指向该文件或目录的硬链接数量                                 |      `16`      |
|     文件拥有者     | 该文件或目录的拥有者                                         |     `root`     |
|       用户组       | 文件或目录所属的用户组                                       |     `root`     |
|      文件大小      | 文件的大小（以字节为单位）                                   |     `3560`     |
| 最后修改日期和时间 | 文件或目录的最后修改日期和时间                               | `Oct 30 20:09` |
|   文件名或目录名   | 文件或目录的名称                                             |     `dev`      |
|    符号链接目标    | 如果是符号链接，指向的目标位置                               |                |

### 文件操作

- **`mv`**：移动或重命名文件或目录。
    示例：`mv file.txt /home/user/documents/`（将 `file.txt` 移动到指定目录）。
- **`cp`**：复制文件或目录。
    示例：`cp file.txt /home/user/documents/`（将 `file.txt` 复制到指定目录）。
- **`rm`**：删除文件或目录。
    示例：`rm file.txt`（删除 `file.txt` 文件）。
- **`rmdir`**：删除空目录。
    示例：`rmdir mydirectory^C`（删除名为 `mydirectory` 的空目录）。
- **`mkdir`**：创建新目录。
    示例：`mkdir newfolder^C`（创建名为 `newfolder` 的新目录）。
- `^C` 表示使用 `Ctrl + C` 组合键来中断或终止当前运行的命令或进程。

### 特殊字符

-   `<`：输入重定向，用于将文件内容作为命令的输入。
-   `>`：输出重定向，用于将命令的输出写入文件。
    -   示例：`echo hello > file`（将字符串 "hello" 写入名为 file 的文件，如果文件已存在则会覆盖）。
-   `cat`：连接文件并输出其内容。
    -   示例：`cat file`（显示 file 的内容）。
    -   示例：`cat < file`（将 file 的内容作为输入并显示）。
    -   示例：`cat < file > file`（将 file 的内容读取并输出到同一个文件中，注意这将覆盖原有内容）。
-   `>>`：追加重定向，用于将命令的输出追加到文件末尾。
    -   示例：`cat < file >> file`（将 file 的内容读取并追加到同一个文件末尾，这样可能会导致内容重复）。

-   `|`：管道符，用于将左侧命令的输出作为右侧命令的输入。
    -   示例：`ls -l | tail -n 2`（列出当前目录下的文件和目录的详细信息，并通过管道将输出传递给 `tail` 命令，`tail -n 2` 会显示输出的最后两行，即最后两个个文件或目录的信息）。

-   `curl --head --silent google.com`：使用 `curl` 命令发送一个 HTTP HEAD 请求到 google.com，获取响应头信息而不显示进度条。
    -   此命令将返回 google.com 的 HTTP 响应头，包括状态码和其他元信息。

-   `curl --head --silent google.com | grep -i content-length | cut --delimiter='' -f2`：通过管道将第一个命令的输出传递给 `grep`，查找包含 "content-length" 的行，并使用 `cut` 命令提取内容长度的值。
    -   此命令将返回 google.com 的内容长度（如果存在），提取出 `Content-Length` 字段的值。

`sudo`：以超级用户权限执行命令。

-   示例：`sudo command`（在执行命令时请求管理员权限）。
-   `sudo的运作机理`：通过 `sudo` 提供特定用户临时提升权限，通常用于执行需要管理员权限的命令。
-   示例：`sudo su`（切换到超级用户模式，直到退出）。
-   示例：`sudo echo 500 > brightness`（这条命令无法成功，因为 `echo` 在 `sudo` 下的输出仍然尝试在普通用户的权限下重定向输出）。
-   示例：`echo 1060 | sudo tee brightness`（使用 `tee` 命令，可以在超级用户权限下成功写入 `brightness` 文件）。

`tee`：从标准输入读取并将其内容输出到标准输出和一个或多个文件。

-   示例：`echo hello | tee file`（将 "hello" 同时输出到终端和 file 文件中）。

`#`：在命令行中表示注释，后面的内容不会被执行。

-   示例：`# This is a comment`（这行注释不会被执行）。

`$`：通常表示命令行提示符，表示当前用户为普通用户。

-   示例：`$ command`（表示普通用户执行命令）。

`cd /sys`：切换到 `/sys` 目录，通常用于查看和修改系统设备信息。

-   示例：`cd /sys`（进入系统文件目录）。

`xdg-open`：用于在默认应用程序中打开文件或网址。

-   示例：`xdg-open https://www.google.com`（在默认浏览器中打开 Google 网站）。

-   **`ls -l filename.type`**

    ：获取文件信息，如果文件不可执行（如得到形如以下的返回结果）：

    `-rw-r--r-- 1 yoyo yoyo 311 Nov  4 21:54 filename.type`

    使用：

    `chmod +x filename.type`

    权限将变更为：

    `-rwxr-xr-x`

****

## Shell Tool and Scripting

---

### 基本变量操作

-   **变量赋值**： `foo=bar`
    -   `echo $foo`： `$`用于访问变量值。
    -   `foo = bar`（有空格）会引发错误，因为解释器会把 `foo` 作为命令，将 `=` 和 `bar` 作为参数。
    -   带有空格的字符串需用引号包裹，例如 `foo="Hello World"`。

-   **字符串分隔符**：
    -   `echo "Hello"` 和 `echo 'Hello'`都输出 `Hello`，但含义不同：
    -   `echo "Value is $foo"` 输出变量 `foo` 的值，而 `echo 'Value is $foo'` 输出字面值 `$foo`。

### Shell 函数与例子

-   **`vim mcd.sh`** ：用于在 Vim 编辑器中打开（或创建）一个名为 `mcd.sh` 的脚本文件，以便进行编辑。
-   `source mcd.sh` ：在当前 shell 环境中执行 `mcd.sh` 脚本文件的内容。

-   **定义函数 `mcd`**：创建目录并切换到该目录。
    
    ```bash
    mcd () 
    {
        mkdir -p "$1"  # 创建路径（包括必要的父目录）
        cd "$1"        # 进入该路径
    }
    
    # mcd $1
    # 如果使用 ./mcd.sh 进行调用加上这个
    ```
    -   `mkdir -p "$1"`： `-p`选项允许递归创建不存在的父目录。
    -   `"$1"`：第一个参数，指定路径。
    -   **使用示例**：
        ```bash
        mcd /path/to/directory
        ```
        执行后会创建 `/path/to/directory` 及其必要的父目录，然后进入该路径。

### 特殊变量

- `$0` - 脚本名。

- `$1` 到 `$9` - 第 1 到第 9 个参数。

- `$@` - 所有参数。

    - 有点像 `python` 中的 `args`。

- `$#` - 参数个数。

- `$?` - 前一个命令的返回状态码（执行情况）。

    - ```bash
        >>> grep foobar mcd.sh
        >>> echo $?
        1
        >>> true
        >>> echo $?
        0
        >>> faluse
        >>> echo $?
        1
        ```

- `$$` - 当前脚本进程号。

- `!!` - 完整的上一条命令。

    - **`sudo !!`**，当原有命令权限不足时，使用这个。

- `$_` - 上一条命令的最后一个参数。

    - **`cd $_`**


### 条件与退出码

-   **条件判断**： `&&` 和 `||` 操作符用于条件判断。
    - `false || echo "Oops, fail"` 输出 `Oops, fail`。
    - `true && echo "Things went well"` 输出 `Things went well`。
    - `;` 用于将多个命令写在同一行中。
    -   **例子**：
        ```bash
        true && echo "All good"  # 执行 echo
        false || echo "Something failed"  # 失败时执行 echo
        false ; echo "This will always print"
        ```

### 命令与进程

- **命令替换**：将命令输出赋值给变量。
    ```bash
    foo=$(pwd) ; echo "We are in $foo"
    
    current_date=$(date)
    echo "Today is $current_date"
    
    cat < (ls) < (ls ..)
    ```
    
- **进程替换**：将命令结果作为临时文件，便于传递给命令。
  
    ```bash
    diff <(ls foo) <(ls bar)  # 比较 foo 和 bar 目录中的内容
    ```
    
- ```bash
    #!/bin/bash
    
    # Date will be sustisuted
    echo "Starting program at $(date)"
    
    echo "Running program $0 with $# arguments with pid $$"
    
    for file in "$@"; do
            grep foobar "$file" >> ~/Demo/first.txt 2>> ~/Demo/second.txt
            # 进行匹配，如果在 file 中找到了 foobar，则将所有含有这个单词的行都输出到 ~/Demo/first.txt 中
            # 如果没有匹配到，那么运行状态就是 2，所以会将错误信息输出到 ~/Demo/second.txt 中
            # 这里也可以把不需要的数据流传递给 /dev/null，这是 Unix/Linux 系统中的一个特殊设备文件，常被称为“空设备”或“黑洞”。通过将输出或错误信息重定向到 /dev/null，您可以有效地“丢弃”这些数据。
            # 丢弃标准输出：command > /dev/null
            # 丢弃标准错误：command 2> /dev/null
            # 同时丢弃标准输出和标准错误可以使用：command > /dev/null 2>&1
            if [[ "$?" -ne 0 ]]; then
            # 注意，这里的 [[]] 必须要和中间内容用空格隔开
            # 这里的 -ne 意思是： not equal
                    echo "File $file does not have any foobar,adding one"
                    echo "# foobar" >> "$file"
            fi
    done
    ```

### 通配符与花括号展开

- **通配符 `?` 和 `*`**：`?`匹配文件或目录的一个字符；`*`匹配文件或目录的多个字符。

    - **`*.sh`**代指所有以  `.sh`结尾的文件
        - **`ls *.sh`**

    - 对于文件 `foo`, `foo1`, `foo2`, `foo10` 和 `bar`：
        - `rm foo*` 删除所有以 `foo` 开头的文件。
        - `rm foo?` 这条命令会删除 `foo1` 和 `foo2` ，而 `rm foo*` 则会删除除了 `bar` 之外的所有文件。

- **`rm -rf *`**删除当前目录内的内容；
- **`rm -rf filename*`**删除当前目录下，以 filename 开头的目录及其中内容；
- **花括号 `{}`**：展开命令。
    ```bash
    convert image.{png,jpg}
    # 会展开为
    convert image.png image.jpg
    
    cp /path/to/project/{foo,bar,baz}.sh /newpath
    # 会展开为
    cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath
    
    # 也可以结合通配使用
    mv *{.py,.sh} folder
    # 会移动所有 *.py 和 *.sh 文件
    
    cp file.{txt,doc} /backup/  # 复制 file.txt 和 file.doc 到 backup 目录
    
    mkdir -p project{1,2}/src/test && echo "GOOD" && touch project{1,2}/src/test/test{1,2,3} && echo "WELL"
    ```
- **数字范围**： `{a..h}` 创建一系列文件。

    ```bash
    mkdir foo bar
    
    # 下面命令会创建 foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h 这些文件
    touch {foo,bar}/{a..h}
    touch foo/x bar/y
    # 比较文件夹 foo 和 bar 中包含文件的不同
    diff <(ls foo) <(ls bar)
    # 输出
    # < x
    # ---
    # > y
    
    touch project{1,2}/src/test/test{1,2,3}.py
    
    ```

### 文件查找与代码搜索工具

- **查找文件**：`find` 查找文件并执行操作。
    ```bash
    find . -name '*.tmp' -exec rm {} \;  # 删除所有 .tmp 文件
    ```
- **更友好的 `find` 替代工具 `fd`**：语法更简单，支持正则和 unicode。
    ```bash
    fd PATTERN
    ```
- **查找内容**：`grep` 搜索文本内容，`rg` 是快速替代工具。
    ```bash
    rg -t py 'import requests'  # 查找 Python 文件中的 "import requests"
    ```

### 历史命令与模糊查找

- **历史命令回溯**：`history | grep find` 查找历史中含 `find` 的命令。
- **模糊查找工具 `fzf`**：增强 `Ctrl+R` 搜索命令历史的功能。

### 目录导航优化

- **目录快捷工具 `fasd` 和 `autojump`**：基于访问频率和时效，快速跳转。
    ```bash
    z cool  # 跳转到最常访问的目录
    ```

****

在 Shell 中，不同的命令和操作方式确实会导致在当前 Shell 或新建的子 Shell 中执行。下面是关键字和常见操作的行为总结，以便你判断何时是在当前 Shell 运行，何时会新建一个子 Shell。

### 1. `source` 或 `.`

- **在当前 Shell 中执行**：`source script.sh` 或 `.`（即 `.` 也是 `source` 的简写）会将脚本中的所有命令在当前 Shell 中执行，而不会启动新的子 Shell。
- **作用**：`source` 常用于需要更改当前 Shell 状态的脚本，例如设置环境变量、切换目录等，因为它直接在当前 Shell 环境中执行。

### 2. 直接调用脚本 (`./script.sh` 或 `bash script.sh`)

- **启动一个子 Shell 执行**：当用 `./script.sh` 或 `bash script.sh` 调用脚本时，会启动一个新的子 Shell。
- **作用**：在子 Shell 中执行时，脚本中的所有变量、目录更改等只对这个子 Shell 有效，不会影响当前的 Shell。

### 3. 使用括号 `(...)` 执行命令组

- **在子 Shell 中执行**：当使用小括号 `(...)` 包裹一组命令时，这些命令会在一个新的子 Shell 中执行。
- **作用**：括号中执行的命令不会影响当前 Shell 的状态，比如目录或变量值。适用于隔离性操作，不影响主环境的状态。
  
  ```bash
  (cd /other/path; echo "Inside sub-shell: $PWD")
  echo "Outside sub-shell: $PWD"
  ```

### 4. 使用大括号 `{...}` 执行命令组

- **在当前 Shell 中执行**：当使用大括号 `{...}` 包裹一组命令时，所有命令会在当前 Shell 中顺序执行。
- **作用**：大括号适用于希望在当前 Shell 中一次性运行一组命令并保持所有更改的情况。
  
  ```bash
  { cd /other/path; echo "Inside current shell: $PWD"; }
  echo "Still in current shell: $PWD"
  ```

### 5. 使用管道 `|`

- **每个命令在自己的子 Shell 中执行**：管道将命令的输出传递给下一个命令，但每个管道段的命令都会在单独的子 Shell 中执行。
- **作用**：使用管道时，子 Shell 之间传递数据，但变量、目录等状态不会共享或保留在当前 Shell 中。
  
  ```bash
  echo "test" | read var
  echo "$var" # 输出为空，因为 read 运行在子 Shell 中
  ```

  如果你想让管道中的变量在当前 Shell 中可用，可以使用 `while` 循环和重定向的方式：
  
  ```bash
  echo "test" | while read var; do
      echo "$var"  # 在子 Shell 输出，但通常在循环外不可用
  done
  ```

### 6. 子 Shell 中运行的其他情况

- **命令替换**：例如 `$(command)` 或 `` `command` `` 运行在子 Shell 中。这是因为命令替换是在当前 Shell 中获取子 Shell 的输出，而不更改当前 Shell 本身。
  
  ```bash
  current_dir=$(cd /other/path; pwd)
  echo "$current_dir"  # /other/path，但当前 Shell 没有改变目录
  ```

### 7. `export` 命令和当前 Shell

- **在当前 Shell 中执行**：`export` 用于声明环境变量，并在当前 Shell 中生效。变量被 `export` 后可以在任何子 Shell 中继承使用。
  
  ```bash
  export VAR="value"
  ```

### 8. 函数调用

- **在当前 Shell 中执行**：定义在当前 Shell 的函数执行不会创建子 Shell。函数内部更改当前 Shell 的状态（例如 `cd`）会对当前 Shell 生效。

### 关键总结

| 操作                | 当前 Shell | 子 Shell |
| ------------------- | :--------: | :------: |
| `source script.sh`  |     ✅      |          |
| `./script.sh`       |            |    ✅     |
| `(command group)`   |            |    ✅     |
| `{ command group }` |     ✅      |          |
| `command | command` |            |    ✅     |
| `$(command)`        |            |    ✅     |
| 函数调用            |     ✅      |          |
| `export`            |     ✅      |          |

****











































