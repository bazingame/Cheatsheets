## Linux

#### 删除指定大小的文件

```shell
find *.txt -size +5K -exec rm {} \;  # 删除大于5k的txt类型的文件
```



#### 替换字符串

```shell
find . -type f -exec sed -i 's/dev.sky31.com/dev.sky31.com/g' {} +
```

