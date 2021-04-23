# os.scandir

```python
for  i in os.scandir('E:\Download'):
    print('文件名:',i.name)
    print('文件绝对路径：',i.path)
    print('是否文件夹:',i.is_dir())
    print('是否文件：',i.is_file())
    print('文件属性：',i.stat())
    print('----------')
```

