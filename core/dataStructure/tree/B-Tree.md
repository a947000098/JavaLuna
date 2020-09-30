B-Tree性质

1. 结点最多含有m颗子树{指针), m-1 个关键字(数据) (m>=2);
2. 除根结点和叶子结点外，其它每个结点至少有ceil(m/2)个子节点(子树)，ceil 为上取整:5/2=2.5取整,分裂  Ceil取上整数2.5=>3 ; 2.1=>3
3. 若根节点不是叶子节点，则至少有两颗子树。

BTree有一个非常重要的操作:当一颗树不满足以上性质的时候会进行 分裂(B-Tree)

紅黑树不满足性质的时候需要左旋、右旋、变颜色来满足性质

例子：创建一个5阶的Btree.插入的数据有:3、14、7、1、8、5、11、17、13、6、23、12、20、26、4、16、18、24、25、19 (数据库的Userld)根据Btree特性，5阶则一个磁盘空间最多有5个指针(存的查找路径), 4个关键字(mysql存的数据)。那么具体的插入如下所示:

第一步：依次插入3、14、7、1

![图片](https://uploader.shimo.im/f/0YaB7B0Sy7dPSID6.png!thumbnail)

第二步：当插入8的时候进行分裂，插入数据结点使用的是插入算法

![图片](https://uploader.shimo.im/f/SzO6rXEdvFbJu4q2.png!thumbnail)

第三步：插入5、11、17

![图片](https://uploader.shimo.im/f/ixQOZHW2Ntu1cWkM.png!thumbnail)

第四步：插入13的时候再次分裂

![图片](https://uploader.shimo.im/f/p125YHsAVpdPd2Yx.png!thumbnail)

最后同理依次将剩余的插入会发现第一层会变成4、7、13、17、20又满足了5阶所以最后分裂后最终结果如下

![图片](https://uploader.shimo.im/f/UMDsEA7qeXVpkeg0.png!thumbnail)

B-Tree的数据结构解决了什么问题？

* 减少了磁盘的访问
* 减少了磁盘的浪费（红黑树每个节点只存一个值）

缺点：

* 无法进行范围查找 如user_id < 9 需要遍历一遍左子树 使索引失效
* 即存储了数据还需要存储地址比较浪费空间 （索引+数据）因此引出了B+Tree
