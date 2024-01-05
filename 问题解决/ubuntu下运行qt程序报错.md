报错：
```
libEGL warning: MESA-LOADER: failed to open radeonsi: /usr/lib/dri/radeonsi_dri.so: 无法打开共享对象文件: 没有那个文件或目录 (search paths /u..........
```
类似这样，除了radeonsi_dir.so还有swrast

解决方案：
```
conda install -c conda-forge gcc    
```