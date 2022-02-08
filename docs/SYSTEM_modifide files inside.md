# 如何修改SYSTEM文件

SYSTEM镜像使用的是squashfs，仅可只读，无法直接修改。

mkdir /mnt/src-squashfs #创建该文件的“源”挂载文件夹

sudo mount -t squashfs -o loop ~/SYSTEM  /mnt/src-squashfs/  #挂载原始squashfs，假定SYSTEM文件放在用户的家目录

rsync -a /mnt/src-squashfs/ /mnt/squashfs/ #将源挂载文件夹的内容同步到/mnt/squashfs/

后续我们的编辑会在/mnt/squashfs/里面做，做好后我们需要将文件重新打包为SYSTEM文件

mksquashfs /mnt/squashfs/ ~/SYSTEM_NEW -comp lzo -b 131072 -no-fragments #打包到家目录文件SYSTEM_NEW

然后将文件复制到emuelec分区中，取代原来的SYSTEM文件。原来的文件或者可以命名为SYSTEM_old，然后把SYSTEM_NEW改名为SYSTEM

