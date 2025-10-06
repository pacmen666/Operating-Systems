# MacBook 上如何搭建 apue.3e 环境并运行 myls.c

-----------------------------彭成

1.  先解压 apue.tar.gz 为 apue.3e，把 apue.3e 放到一个合适的文件夹下。

2.  命令行窗口 cd 到 apue.3e 目录。

3.  执行 `make`，这时 lib 目录里面会生成 `libapue.a`。（会有一个 error，不用理会）

4.  复制 apue.h 到 /usr/local/include/

    ```bash
    cd include
    sudo cp apue.h /usr/local/include/
    ```

    验证：

    ```bash
    ls /usr/local/include/apue.h
    ```

    若能显示 `apue.h` 路径，说明复制成功。

5.  复制 libapue.a 到 /usr/local/lib/

    ```bash
    cd ~/Downloads/apue.3e/lib  # 替换为你的实际路径
    sudo cp libapue.a /usr/local/lib/
    ```

    验证：

    ```bash
    ls /usr/local/lib/libapue.a
    ```

6.  创建 `myls.c`。

7.  利用 `-l apue` 链接 `apue libapue.a` 静态库并编译:

    ```bash
    gcc myls.c -o myls -l apue
    ```

8.  无报错则成功，环境正常。

9.  编译成功后会生成 `myls` 可执行文件，执行时需传入一个目录名作为参数（代码要求 `argc == 2`，即 “程序名 + 目录名”）。

10. 示例：

    ```bash
    # 示例1：查看当前用户主目录（~）的内容（Linux/macOS 通用）
    ./myls ~

    # 示例2：查看 /users 目录的内容
    ./myls /users

    # 示例3：查看当前工作目录的上级目录（../）
    ./myls ../
    ```