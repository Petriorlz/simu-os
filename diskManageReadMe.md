## 外部函数

### 目录管理：删除文件

删除目录中某个文件，删除其在磁盘中的数据，并删除目录项。

以文件名为参数，在FAT表中查找文件开始磁盘块号和其余盘块号，在磁盘中逐步删除整个文件。同时更新FAT表和空闲盘块。

```
void DeallocateBlocks(string fileName);
```

### 线程管理：数据生成线程

该线程负责生成外存数据，给定数据大小（按字节计算）、数据信息（英文字母）、存储目录、文件名后，该线程调用磁盘管理中空闲磁盘管理功能，申请所需大小的外存块，如果盘块不够给出提示。按照要求的数据组织方式，将数据存入磁盘块（按块分配磁盘），并调用目录管理功能为其在目录中建立目录项，更改空闲盘块信息。注意，目录本身不需要分配盘块。

```
/** 
*@param size 数据大小（按字节计算）
*@param data 数据信息（英文字母）
*@param filename 文件名
*@return 磁盘块是否充足， 或分配的首个磁盘块
*/
int DiskManager::AllocateBlocks(int size, string data, string fileName);
```

### 线程管理:删除数据线程

该线程调用目录管理中删除文件功能删除数据（正在内存中的中文件不能被删除）。并回收外存空间，更新空闲盘块信息。

### 线程管理：执行进程

根据目录中文件存储信息将文件数据从外存读入内存，此间如果8块内存不够存放文件信息，需要进行换页（选择的换页策略见分组要求），换出的页面存放到磁盘兑换区。

```
     // 读取兑换区块
    void readSwapBlock(int blockNum, char *buffer);
    // 写入兑换区块
    void writeSwapBlock(int blockNum, char *buffer);
```

## 内部函数



## 用户接口

可以动态查看外存信息



