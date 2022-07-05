# 


# 準備工作

kernel文件似乎是zimage格式文件。所以我們先要用工具將它解包

https://github.com/work4blue/unpack-mkbootimg

下載這個後放在home目錄，進去編譯一下

make

# 解包內核

然後多出來兩個命令，一個用來解包一個用來打包的。我們先解包

unpackbootimg -i kernel.img -o ~/out

out目錄（在你自己的home下面）必須提前創建

如果沒有提示出錯信息，會解壓縮出來幾個文件

kernel.img-zImage (内核文件）
kernel.img-ramdisk.gz (根文件系统打包文件）
kernel.img-cmdline (mkbootimg cmdline参数)
kernel.img-pagesize (mkbootimg pagesize参数)
kernel.img-base (mkbootimg base参数)

此外執行過程中會有類似以下的命令

BOARD_KERNEL_CMDLINE 
BOARD_KERNEL_BASE 01078000
BOARD_PAGE_SIZE 2048

記得要將這個記下來

# 處理文件

這裏我們要用7zip，解壓縮kernel.img-ramdisk.gz，注意其中會提示該文件並不是gzip，用cpio解壓。

然後我們將它放到out下面的一個目錄（隨便新建一個），修改完裏面需要改的文件後，在這個新建的下層目錄下執行以下命令

find . | cpio -c -o > ../kernel.img-ramdisk2.gz

這樣就剛好在上層生成一個kernel.img-ramdisk2.gz

然後我們再將kernel.img-zImage解壓，裏面有個kernel文件，將它重命名爲zkernel。

# 打包

./mkbootimg --cmdline 'no_console_suspend=1 console=null' --kernel zkernel --ramdisk kernel.img-ramdisk2.gz -o ~/boot.img --base 01078000

这句含义是把内核文件zzkernel和boot目录下的根文件压缩包 kernel.img-ramdisk2.gz打包成home目錄下的boot.img.其中cmdline和base的值均来源于unpackbootimg的结果。


