<!-- TOC GFM -->

* [目录的相关操作](#目录的相关操作)
    - [切换目录](#切换目录)
    - [显示当前目录](#显示当前目录)
    - [新建目录](#新建目录)
    - [删除空目录](#删除空目录)
    - [PATH 变量](#path-变量)
* [文件与目录管理](#文件与目录管理)
    - [文件与目录的查看](#文件与目录的查看)
    - [复制、删除与移动](#复制删除与移动)
        + [cp](#cp)
        + [rm](#rm)
        + [mv](#mv)
    - [文件内容查看](#文件内容查看)
        + [直接查看文件内容](#直接查看文件内容)
        + [可翻页查看](#可翻页查看)
        + [数据截取](#数据截取)
        + [非纯文本文件](#非纯文本文件)
        + [修改文件时间或创建新文件](#修改文件时间或创建新文件)
    - [默认权限与隐藏权限](#默认权限与隐藏权限)
        + [文件默认权限：umask](#文件默认权限umask)
        + [文件隐藏属性](#文件隐藏属性)
        + [文件特殊权限](#文件特殊权限)
* [---](#---)
* [---](#----1)
    - [命令与文件的查找](#命令与文件的查找)
        + [脚本文件的查找](#脚本文件的查找)
    - [文件查找](#文件查找)

<!-- /TOC -->
## 目录的相关操作

**比较特殊的目录**  

| 符号     | 目录                       |
|----------|----------------------------|
| .        | 代表此层目录               |
| \.\.     | 代表上一层目录             |
| \-       | 代表前一个工作目录         |
| ~        | 代表目前使用者所在的家目录 |
| ~account | 代表 account 用户的家目录  |

> 在所有目录下面都会存在两个目录，分别是`.` 与 `..` 分别代表此层与上层目录的意思  
>
> 根目录下也存在这两个目录，但是这两个根目录都**表示根目录自己**，与其他目录有些不同



### 切换目录

**命令**  
```bash
cd 目录名称
```

cd 是 Change Directory 的缩写，用来切换工作目录  

如果仅是单单输入命令 `cd` ，代表的就是 `cd ~` 的意思  




### 显示当前目录

**命令**  
```bash
pwd [-P]
```

选项：  
* `-P`：显示出真正的路径，而非使用链接（link）路径

pwd 是 Print Working Directory 的缩写，用来显示当前所在目录  

`-P` 选项可以显示出正确的目录名，而不是以链接文件的路径来显示  



### 新建目录

**命令**  
```bash
mkdir [-mp] 目录名称
```

选项：
* `-m`：设置文件的权限、直接设置，不使用默认权限（umask）
* `-p`：帮助你直接将所需要的目录（包含上层目录）递归创建


mkdir 是 Make Directory 的缩写，用来新建目录  


**选项使用说明**  

`-p` 选项：
此时需要创建目录 `test1/test2/test3`，但是还没有创建 `test1` 目录  

```bash
mkdir -p test1/test2/test3
```

> 在默认情况下，所需要的目录得**一层一层**地建立才行  
> 如果没有使用 `-p` 选项，由于都没有 `test1` 目录，所以会报错  
> 并且如果前面的目录都存在，使用这个选项也不会报错  
> **但是不建议常用 `-p` 选项**，放置打错字而弄乱目录  


`-m` 选项：

```bash
mkdir -m 711 test
```

> 在创建目录时，不使用系统的默认权限，自己指定  



### 删除空目录

**命令**  
```bath
rmdir [-p] 目录名称
```

选项：
* `-p`：连同上层的**空**目录也一起删除


rmdir 是 remove directory 的缩写，用于删除**空目录**  
> 空目录：被删除的目录里面必定不能存在其他的目录或文件  


此命令不常用  




### PATH 变量

当我们在执行一个 command 时，系统会依照 PATH 的设置去每个 PATH 定义的目录下查找文件名为该 command 的可执行文件  
如果在 PATH 定义的目录中含有多个文件名为该 command 的可执行文件，那么先查找到的同名 command 先被执行  

可以使用 `echo` 命令来查看 PATH 变量  
```bash
echo $PATH
```

PATH 变量的内容是由一堆目录所组成，每个目录中间用冒号（:）来隔开，每个目录**有顺序之分**  

**不建议将 `.` 目录加入到 PATH 中**  
> 如果有人在公共目录中（例如 /tmp 目录）写入了一个病毒文件（命名为 `ll`），此时如果将 `.` 目录加入到了 PATH 中，那么在我们想使用 ll 命令时就很可能会中招  

---

**总结**  

* 不同身份用户默认的 PATH 不同，默认能够随意执行的命令也不同
* PATH 是可以修改的
* 使用绝对路径或相对路径直接指定某个命令的文件名来执行，会比查找 PATH 来的正确
* 命令应该要放置到正确的目录下，执行才会比较方便
* 本目录 `.` 最好不要放到 PATH 当中




## 文件与目录管理


### 文件与目录的查看

使用 `ls` 命令来查看  

**命令格式：**  

```bash
ls [-aAdfFhilnrRSt] 文件名或目录名

ls [--color={never, auto, always}] 文件名或目录名

ls [--full-time] 文件名或目录名
```

**选项：**  
* `-a`：全部的文件，连同隐藏文件一起列出来
* `-d`：仅列出目录本身，而不是列出目录内的文件数据
* `-l`：详细信息显示，包含文件的属性与权限等数据
* `-A`：全部的文件，连同隐藏文件，但不包括 `.` 与 `..` 这两个目录
* `-f`：直接列出结果，而不进行排序（ls 默认会以文件名排序）
* `-F`：根据文件、目录等信息，给予附加数据结构
    > 例如：*：代表可执行文件； /：代表目录； =：代表 socket 文件； |：代表 FIFO 文件  

* `-h`：将文件内容以人类较易读的方式（如 GB、KB）列出来
* `-i`：列出 inode 号码
* `-n`：列出 UID 与 GID 而非使用者与用户组的名称
* `-r`：将排序结果反向输出，例如：原本文件名有小到大，反向则有大到小
* `-R`：连同子目录内容一起列出来
* `-S`：以文件容量大小排序，而不是用文件名排序
* `-t`：依时间排序，而不是用文件名
* `--color=never`：不要依据文件特性给予颜色显示
* `--color=always`：显示颜色
* `--color=auto`：让系统自行依据设置来判断是否给予颜色
* `--full-time`：以完整时间模式（包含年、月、日、时、分）输出
* `--time={atime, ctime}`：输出 access 时间或改变权限属性时间（ctime），而非内容修改时间（modification time）



### 复制、删除与移动

#### cp

使用 cp 来复制文件或目录  
> 英文缩写：copy  

**命令格式**  

```bash
cp [options] source1 source2 source3 .... directory

cp [-adfilprsu] 源文件(source) 目标文件(destination)
```

**选项**
* `-a`：相当于 -dr --preserve=all 的意思
* `-d`：若源文件为链接文件的属性（link file），则复制链接文件属性而非文件本身
* `-f`：（force）强制的意思，若目标文件已经存在且无法开启，则删除后再尝试一次
* `-i`：若目标文件已经存在时，在覆盖时会先询问操作的进行
* `-l`：进行硬链接的链接文件建立，而非复制文件本身
* `-p`：连同文件的属性（权限、用户、时间）一起复制过去，而非使用默认属性
* `-r`：递归复制，用于目录的复制操作
* `-s`：复制成为符号链接文件
* `-u`：destination 比 source 旧才更新 destination，或 destination 不存在的情况下才复制
* `--preserve=all`：除了 -p 的权限相关参数外，还加入 SELinux 的属性，links、xattr 等也复制


**如果源文件有两个以上，则最后一个目标文件一定要是“目录”才行**  


**在默认条件中，cp 的源文件与目标文件的权限是不同的，目标文件的拥有者通常会是命令操作者本身**  
由于具有这个特性，当进行备份的时候，有些特殊权限的文件以及一些配置文件，就不能直接以 cp 来复制，而必须要加上 `-a` 或 `-p` 来完整复制文件权限  

在你复制文件给其他的用户时，也必须要注意到文件的权限  


**与拥有者、用户组相关的，执行 cp 的用户无法进行的操作，即使加上 -a 选项，也是无法完成完整权限的复制**  


**在复制时，需要考虑的：**  
* 是否需要完整的保留源文件的信息
* 源文件是否为符号链接文件
* 源文件是否为特殊的文件，例如 FIFO、socket 等
* 源文件是否为目录


---



#### rm

使用 rm 来删除文件或目录  
> 英文缩写：remove  

**命令格式**  

```bash
rm [-fir] 文件或目录
```

**选项**  

* `-f`：force 的意思，忽略不存在的文件，不会出现警告信息
* `-i`：交互模式，在删除前会询问使用者是否操作
* `-r`：递归删除，是常用于目录的删除

---


#### mv

使用 mv 移动文件与目录，或重命名  
> 英文缩写：move  

**命令格式**  

```bash
mv [-fiu] source destination

mv [options] source1 source2 source3 .... directory
```

**选项**  

* `-f`：force 的意思，如果目标文件已经存在，不会询问而直接覆盖
* `-i`：若目标文件 (destination) 已经存在时，就会询问是否覆盖
* `-u`：若目标文件已经存在，且 source 比较新，才会更新




### 文件内容查看


#### 直接查看文件内容

直接查看文件的内容可以使用 cat/tac/nl 这几个命令  

---

**cat**

> 是 concatenate 的缩写
> 
> 主要功能是将一个文件的内容连续打印在屏幕上  


**命令格式**  

```bash
cat [-AbEnTv] 文件名称
```

**选项**  

* `-A`：相当于 `-vET` 的整合选项，可列出一些特殊字符而不是空白
* `-b`：列出行号，仅针对非空白行做行号显示，空白行不标行号
* `-E`：将结尾的换行符 $ 显示出来
* `-n`：打印出行号，连同空白行也会有行号，与 `-b` 的选项不同
* `-T`：将 [tab] 按键以 ^I 显示出来
* `-v`：列出一些看不出来的特殊字符



**在查看一般的 DOS 文件时，由于有一些符号与 linux 不同，所以最好加上 `-A` 选项**
> 一般 cat 用的比较少，当文件的内容超过 40 行以上，根本来不及在屏幕上看到结果，更何况在纯终端下不能往上翻阅  

---

**tac**  
> 与 cat 命令相反  
> tac 是由最后一行到第一行反向在屏幕上显示出来  

**命令格式**  

```bash
tac [options] 文件名
```

**选项与 cat 一样**  

---

**nl**  
> nl 可以将输出的文件内容自动地加上行号，其默认的结果与 cat -n 有点不太一样，nl 可以将行号做比较多的显示设计，包括位数与是否自动补齐 0 等的功能  


```bash
nl [-bnw] 文件名
```

**选项**  

* `-b`：指定行号指定的方式，主要有两种：
    * `-b a`：表示不论是否为空行，也同样列出行号
    * `-b t`：如果有空行，空的那一行不要列出行号（默认值）
* `-n`：列出行号表示的方法，主要有三种：
    * `-n ln`：行号在屏幕的最左方显示
    * `-n rn`：行号在自己栏位的最右方显示，且不加 0
    * `-n rz`：行号在自己栏位的最右方显示，且加 0
* `-w`：行号栏位的占用的字符数


举例：

```bash
nl /etc/issue

nl -b a /etc/issue

nl -b a -n rz /etc/issue

nl -b a -n rz -w 3 /etc/issue
```




#### 可翻页查看


**more**  

**命令格式**  

```bash
more 文件名
```

**功能键**  
* `空格键（space）`：代表向下翻页
* `Enter`：代表向下翻一行
* `/字符串`：代表在这个显示的内容当中，向下查找字符串这个关键词
* `:f`：立刻显示出文件名以及目前显示的行数
* `q`：代表立刻离开 more，不再显示该文件的内容
* `b`或`[Ctrl]-b`：代表往回翻页，不过这操作只对文件有用，对管道无用

---

**less**  
> 比起 more 更有弹性，more 不能往前翻，只能往后翻  
>
> 但是 less 往前往后翻都可以  
> 同时增加了其他有用的功能键  

**命令格式**  

**功能键**  
* `空格键`：向下翻动一页
* `[pagedown]`：向下翻动一页
* `[pageup]`：向上翻动一页
* `/字符串`：向下查找字符串的功能
* `?字符串`：向上查找字符串的功能
* `n`：重复前一个查找（与/或?有关）
* `N`：反向的重复前一个查找（与/或?有关）
* `g`：前进到这个数据的第一行
* `G`：前进到这个数据的最后一行
* `q`：离开 less 这个程序


> man 命令就是调用的 less 来显示说明文件的内容  




#### 数据截取


**head**  

> 显示出一个文件的前几行  


**命令格式**  

```bash
head [-n number] 文件
```

**选项**  

* `-n`：后面接数字，代表显示文件前面几行


**如果 `-n` 后面接的是负数，-100 代表列出前面所有行，但不包括后面 100 行**

**默认显示前 10 行**  


举例：  

```bash
head -n 20 /etc/man_db.conf         // 显示文件的前 20 行

head -n -100 /etc/man_db.conf       // 显示文件的所有内容，除了最后的 100 行不显示
```

---


**tail**  

> 与 head 相反，显示的是后面的几行


**命令格式**  

```bash
tail [-n number] 文件
```

**选项**  

* `-n`：后面接数字，代表显示几行的意思
* `-f`：表示持续刷新显示后面所接文件中的内容，要等到按下 `<Ctrl-c>` 才会结束


**如果 `-n` 后面接的是 `+` 数，+100 代表从第 100 行开始，显示文件后面剩下的内容**  

**如果想要监视一个文件，也就是当这个文件改动时，将改动的内容同步到屏幕输出，监视范围是根据 tail 的显示范围决定的**  

**默认显示最后 10 行**  



举例：  

```bash
tail -n 20 /etc/man_db.conf        // 显示最后 20 行

tail -n +100 /etc/man_db.conf      // 从 100 行开始，显示出文件后面的内容
```

---


#### 非纯文本文件


**od**  

> 对于二进制文件，使用普通的查看文本文件的命令查看会出现**乱码**  

> od 的用途就是用来查看二进制文件  


**命令格式**  

```bash
od [-t TYPE] 文件
```

**选项**  

* `-t`：后面可接各种类型 (TYPE) 的输出，例如：
    * `a`：利用默认的字符来输出
    * `c`：使用 ASCII 字符来输出
    * `d[size]`：利用十进制（decimal）来输出数据，每个整数占用 size Bytes
    * `f[size]`：利用浮点数值（floating）来输出数据，每个数占用 size Bytes
    * `o[size]`：利用八进制（octal）来输出数据，每个整数占用 size Bytes
    * `x[size]`：利用十六进制（hexadecimal）来输出数据，每个整数占用 size Bytes



举例：  

```bash
od -t c /usr/bin/passwd
```

> 将内容使用 ASCII 方式显示  
>
> 最左边第一列以八进制来表示这一行第一列的 Bytes 数  

```bash
od -t oCc /etc/issue
```

> 将 /etc/issue 文件的内容以八进制列出存储值与 ASCII 的对照表  



---


#### 修改文件时间或创建新文件

**touch**  

> 命令作用：  
> * 建立一个空文件
> * 将某个文件日期自定义为目前（mtime 与 atime）





关于时间参数：  

* 修改时间（modification time，mtime）  
    当该文件的**内容数据**变更时，就会更新这个时间，内容数据指的是文件的内容，而不是文件的属性或权限  

* 状态时间（status time，ctime）  
    当该文件的**状态（status）**改变时，就会更新这个时间，举例来说，像是**权限与属性被更改了**，都会跟新这个时间  

* 读取时间（access time，atime）  
    当**该文件的内容被读取**时，就会更新这个读取时间（access），举例来说，使用 cat 读取 /etc/man_db.conf ，就会更新这个文件的 atime  



当用 `ls` 命令来查看文件的时间状态时，`ls` 默认显示出来的是该文件的 **mtime**

如果想要使 `ls` 显示其他的时间信息：  

```bash
ls -l --time=atime 文件名

ls -l --time=ctime 文件名

ls -l --time=mtime 文件名
```

---

**命令格式**  

```bash
touch [-acdmt] 文件
```

**选项**  

* `-a`：仅自定义 access time
* `-c`：仅修改文件的时间，若该文件不存在则不建立新文件
* `-d`：后面可以接欲自定义的日期而不用目前的日期，也可以使用 `--date="日期或时间"`
* `-m`：仅修改 mtime
* `-t`：后面可以接欲自定义的时间而不是目前的时间，格式为`[YYYYMMDDhhmm]`





### 默认权限与隐藏权限




#### 文件默认权限：umask

umask就是**指定目前用户在建立文件或目录时候的权限默认值**  


查看 umask 值的方法  

```bash
umask [-S]
```

**选项**  

* `-S`：Symbolic，以符号的类型的方式来显示权限


> umask 默认是以数字显示  

```bash
umask
```

此时 umask 的结果为 022 表示：
* 第一个 0：user 的默认权限需要减去的权限
* 第二个 2：group 的默认权限需要减去的权限
* 第三个 2：other 的默认权限需要减去的权限




---


对于默认权限的属性：  

* 若用户建立为文件则默认没有可执行（x）权限，即只有 rw 这两个选项，也就是最大为 666，默认权限就是  
    ```bash
    -rw-rw-rw-
    ```

* 若用户建立为目录，则由于 x 与是否可以进入此目录有关，因此默认为所有权限均开放，即 777，默认权限就是  
    ```bash
    drwxrwxrwx
    ```


umask 的数字指的是**该默认值需要减掉的权限**  

这里 umask 默认为 002，所以 user 没有被拿掉任何权限，group 和 others 的权限被拿掉了 2（也就是 w 权限），那么当用户：  

* 建立文件时：(-rw-rw-rw-) - (-----w--w-) ==> -rw-r--r--
* 建立目录时：(drwxrwxrwx) - (d----w--w-) ==> drwxr-xr-x




#### 文件隐藏属性


**chattr**  

> 用于配置文件的隐藏属性  


**命令格式**  

```bash
chattr [+-=] [ASacdistu] 文件或目录名称
```

**选项**  

* `+`：增加某一个特殊参数，其他原本存在的参数则不动
* `-`：删除某一个特殊参数，其他原本存在参数则不动
* `=`：直接设置参数，且仅有后面接的参数
* `A`：当设置了 A 这个属性时，若在存取此文件（或目录）时，它的存取时间 atime 将不会被修改，可避免 I/O 较慢的机器过度的读写磁盘（建议使用文件系统挂载参数处理这个项目）
* `S`：一般文件是非同步写入磁盘的，如果加上 S 这个属性时，当进行任何文件的修改，该修改会**同步**写入磁盘中
* `a`：当设置 a 之后，这个文件将只能增加数据，而不能删除也不能修改数据，只有 root 才能设置这属性
* `c`：这个属性设置之后，将会自动的将此文件**压缩**，在读取的时候将会自动解压缩，但是在存储的时候，将会先进行压缩后再存储（对于大文件有用）
* `d`：当 dump 程序被执行的时候，设置 d 属性将可使该文件（或目录）不会被 dump 备份
* `i`：当设置 i 属性之后，可以让一个文件**不能被删除、改名，设置链接也无法写入或新增数据**，对于系统安全性有相当大的助益，只有 root 能设置此属性
* `s`：当文件设置了 s 属性时，如该文件被删除，它将会被完全的从硬盘删除，所以如果误删，完全无法恢复
* `u`：与 s 相反的，当使用 u 来配置文件时，如果该文件被删除了，则数据内容其实还存在于磁盘中，可以使用来恢复该文件


**属性设置常见的是 a 与 i 的设置值，而且很多设置值必须要是 root 才能设置**  

**xfs 文件系统仅支持 Aadis**  


例如：  

```bash
touch test
sudo chattr +i test
```

> 之后此文件就不能被删除，甚至是 root 也不行  
>
> 只要这个属性存在，该文件不管怎样都不能被删除

```bash
sudo chattr -i test
rm test
```

> 现在就可以删除此文件了

---


**lsattr**  

> 显示文件的隐藏属性  


**命令格式**  

```bash
lsattr [-adR] 文件或目录
```

**选项**  

* `-a`：将隐藏文件的属性也显示出来
* `-d`：如果接的是目录，仅列出目录本身的属性而非目录内的文件名
* `-R`：连同子目录的数据也一并列出来




#### 文件特殊权限


**SUID**  
表示 Set UID  

当 s 这个标志出现在文件拥有者的 x 权限上时：  
```bash
-rwsr-xr-x
```

此时就被称为 Set UID，简称为 SUID 的特殊权限  

SUID 的限制与功能：  

* SUID 权限仅对于二进制程序（binary program）有效
* 执行者对于该程序需要具有 x 的可执行权限
* 本权限仅在执行该程序的过程中有效（run-time）
* 执行者将具有该程序拥有者（owner）的权限


**SUID 仅可用在二进制文件上，不能够用在 shell 脚本上**  
> 因为 shell 脚本只是将很多的二进制执行文件调用执行而已  
> 所以 SUID 的权限部分，还是要看 shell 脚本调用进来的程序的设置，而不是 shell 脚本本身  


**SUID 对于目录也是无效的**



举例：  
> liunx 中，所有账号的密码都记录在 /etc/shadow 文件里，这个文件的权限为：  
> 
> ```bash
> ---------- 1 root root
> ```
>
> 意思是这个文件仅有 root 可读且仅有 root 可强制写入  
> 既然此文件仅有 root 可修改，那么平时一般用户更改自己的密码时，是如何能够更改的？（修改密码也就是修改 /etc/shadow 文件内容）
>
> 这里就是 SUID 的作用在生效了：  
> * 一般用户对于 /usr/bin/passwd 这个程序来说具有 x 的权限，表示一般用户能执行 passwd
> * passwd 的拥有者是 root
> * 一般用户在执行 passwd 的过程中，会**暂时**获得 root 的权限
> /etc/shadow 就可以被一般用户所执行的 passwd 所修改


> 如果使用 cat 去读取 /etc/shadow 时，是不能读取的  
> 因为 cat 不具有 SUID 的权限，所以一般用户执行 cat 时是不能读取 /etc/shadow 的  


---
---


**SGID**  
表示 Set GID  


当 s 这个标志出现在文件用户组的 x 权限上时：  
```bash
-rwx--s--x
```

此时就被称为 Set GID，简称为 SGID 的特殊权限  


SGID 对于文件的功能：  

* SGID 对二进制程序有用
* 程序执行者对于该程序来说，需具备 x 的权限
* 执行者在执行的过程中将会获得该程序用户组的支持


举例：  
> 假设需要使用一般用户查看文件 test，test 的权限属性如下：  
> ```bash
> -rw-r-----. 1 root slocate
> ```
>
> 此时需要使用 locate 程序来读取文件 test 的内容，locate 的权限属性如下：  
> ```bash
> -rwx--s--x. 1 root slocate
> ```
>
> 这样，一般用户在使用 locate 时，就会取得 slocate 用户组的支持，而 test 文件对于 slocate 用户组具有读权限，因此一般用户使用 locate 也就可以读取文件 test 了  



SGID 对于目录的功能：  

* 用户若对此目录具有 r 与 x 的权限时，该用户能够进入此目录
* 用户在此目录下的有效用户组（effective group）将会变成该目录的用户组
* 用途：若用户在此目录下具有 w 的权限时，则用户所建立的新文件，该新文件的用户组与此目录的用户组相同


**SGID 对于项目开发来说非常重要，因为这涉及用户组权限的问题**  


---
---


**SBIT**  
表示 Sticky Bit  

SBIT 目前只针对**目录有效**，对于文件已经没有效果了  


SBIT 对于目录的功能：  

* 当用户对于此目录具有 w、x 权限，即具有写入的权限
* 当用户在该目录下建立文件或目录时，仅有自己与 root 才有权力删除该文件


举例：  

> 当甲用户对于 A 目录具有用户组或其他人的身份，并且拥有该目录 w 的权限，这表示甲用户对该目录内任何人建立的目录或文件均可删除、更名、移动等操作  
>
> **但如果将 A 目录加上了 SBIT 的权限选项时，则甲只能够针对自己建立的文件或目录进行删除、更名、移动等操作，而无法删除它人的文件**  



---

---



**SUID/SGID/SBIT 权限设置**  

通过数字形式更改权限的方式  

* 4：SUID
* 2：SGID
* 1：SBIT


对于三个基本权限使用数字表示是**三个数字**，每个数字都是对应的权限累加，特殊权限设置也遵循这个规则，并将这个相加的数字放到三个基本权限的前面，形成四个权限数字  

例如：  
> 假设要将一个文件权限改为 `-rwsr-sr-x` 时，由于 s 在用户权限中，所以是 SUID，因此，在原先的 755 之前还要加 6（4+2+0）  
> 就是 `chmod 6755 filename` 来设置  


对于 S 与 T 的产生  

当文件的 owner 没有 x 权限时，即使添加了 SUID 权限，也同样没有效果  
当文件的 group 没有 x 权限时，即使添加了 SGID 权限，也同样没有效果  
当文件的 other 没有 x 权限时，即使添加了 SBIT 权限，也同样没有效果  
对于没有效果的，使用 S 或 T 表示  

> SUID 是表示该文件在执行的时候，具有文件拥有者的权限，但是文件的拥有者都无法执行了，也就没有权限给其他人使用，就是空的  

---


通过符号形式更改权限的方式  

* SUID：u+s
* SGID：g+s
* SBIT：o+t


例如：  
> ```bash
> chmod u=rwxs,go=x test
>
> chmod g+s,o-t test
> ```
>
> 分别指定权限与加减权限




### 命令与文件的查找



#### 脚本文件的查找


**which**  

> 用来查找**执行文件**  


**命令格式**  

```bash
which [-a] command
```

**选项**  

* `-a`：将所有由 PATH 目录中可以找到的命令均列出，而不止第一个被找到的命令名称


这个命令是根据 PATH 这个环境变量所规范的路径，去查找**执行文件**的文件名  




### 文件查找


**whereis**  

> 由一些特定的目录中查找文件  


**命令格式**  

```bash
whereis [-bmsu] 文件或目录名
```

**选项**  

* `-l`：可以列出 whereis 会去查询的几个主要目录
* `-b`：只找 binary 格式的文件
* `-m`：只找在说明文件 manual 路径下的文件
* `-s`：只找 source 源文件
* `-u`：查找不在上述三个项目当中的其他特殊文件


`whereis` 查找速度快的原因是 `whereis` 只找几个特定的目录，并没有全系统去查询  
可以使用命令 `whereis -l` 来列出 whereis 在查找时会查询的目录  


---


**locate / updatedb**  



**命令格式**  

```bash
locate [-ir] keyword
```

**选项**  

* `-i`：忽略大小写的差异
* `-c`：不输出文件名，仅计算找到的文件数量
* `-l`：仅输出几行的意思，例如输出五行则是 `-l 5`
* `-s`：输出 locate 所使用的数据库文件的相关信息，包括该数据库记录的文件/目录数量等
* `-r`：后面可接正则表达式的显示方式


locate 寻找数据特别快，这是因为 locate 寻找的数据是由已建立的数据库 /var/lib/mlocate 里面的数据所查找到的，不用去硬盘查询  

但是有一个限制，由于数据库的建立默认是在每天执行一次，所以当新建文件时，如果此数据库没有更新，那么就会导致找不到这个新建立的文件，必须要更新数据库  


**手动更新数据库**  

直接执行 `updatedb` 命令即可，`updatedb` 命令会去读取 `/etc/updatedb.conf` 这个配置文件，然后再去硬盘里进行查找文件名的操作，最后更新整个数据库  


**流程**  

* `updatedb`：根据 `/etc/updatedb.conf` 的设置去查找系统硬盘内的文件，并更新 `/var/lib/mlocate` 内的数据库文件
* `locate`：依据 `/var/lib/mlocate` 内的数据库记录，找出用户所输入关键词的文件名


---


**find**  


**命令格式**  

```bash
find [PATH] [option] [action]
```

**options**  

1. 与时间有关的选项，共有 -atime、-ctime 与 -mtime，以 -mtime 为例：
    * `-mtime n`：n 为数字，意义为在 n 天之前的（一天之内）被修改过内容的文件
    * `-mtime +n`：列出在 n 天之前（不含 n 天本身）被修改过内容的文件
    * `-mtime -n`：列出在 n 天之内（含 n 天本身）被修改过内容的文件
    * `-newer file`：file 为一个存在的文件，列出比 file 还要新的文件
    > 关于时间参数：  
    > * +4 代表大于等于 5 天前的文件：`ex > find /var -mtime +4`  
    > * -4 代表小于等于 4 天内的文件：`ex > find /var -mtime -4`  
    > * 4 代表 4-5 那一天的文件：`ex > find /var -mtime 4`  


2. 与使用者或用户组名称有关的参数：  
    * `-uid n`：n 为数字，这个数字是使用者的账号 ID，亦即 UID，这个 UID 记录在 /etc/passwd 里面
    * `-gid n`：n 为数字，这个数字是用户组名称的 ID，亦即 GID，这个 GID 记录在 /etc/group 里面
    * `-user name`：name 为使用者账号名称
    * `-group name`：name 为用户组名称
    * `-nouser`：查找文件的拥有者不在 /etc/passwd
    * `-nogroup`：查找文件的拥有用户组不存在于 /etc/group 的文件
        > 在自行安装软件时，很可能该软件的属性当中并没有文件拥有者，这是可能的，此时就可以使用 -nouser 或 -nogroup 查找  


3. 与文件权限及名称有关的参数：
    * `-name filename`：查找文件名称为 filename 的文件
    * `-size [+-]SIZE`：查找比 SIZE 还要大(+) 或小(-) 的文件，这个 SIZE 的规格有：
        * c：代表 Bytes
        * k：代表 1024Bytes
    * `-type TYPE`：查找文件的类型为 TYPE 的，类型主要有：
        * f：一般正规文件
        * b，c：设备文件
        * d：目录
        * l：链接文件
        * s：socket
        * p：FIFO
    * `-perm mode`：查找文件权限 **刚好等于** mode 的文件，这个 mode 为类似 chmod 的属性值
    * `-perm -mode`：查找文件权限 **必须要全部囊括 mode 的权限** 的文件
    * `-perm /mode`：查找文件权限 **包含任一 mode 的权限** 的文件


**actions** 
* 额外可进行的操作：  
    * `-exec command`：command 为其他命令，-exec 后面可再接额外的命令来处理查找到的结果
    * `-print`：将结果打印到屏幕上，这个操作是**默认操作**


```bash
find / -perm /7000 -exec ls -l {} \;
```

* `{}`：代表由 find 找到的内容，这里是 `find / -perm /7000` 的结果
* `-exec` 一直到 `\;` 是关键词，代表 find 额外操作的开始（-exec）到结束（\;），在这中间的就是 find 命令内的额外操作：
    * 这里就是 `ls -l {}`
* 因为 `;` 在 bash 环境下有特殊的意义，所以需要用反斜杠 `\` 来转义



**由于 find 在查找数据时相当消耗硬盘资源，所以没事不要使用 find**




