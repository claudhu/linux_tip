# 什麼是硬連結 什麼是軟連結
![圖表解釋](https://i.stack.imgur.com/f7Ijz.jpg)

reference link: [ubuntuAsk](http://askubuntu.com/questions/108771/what-is-the-difference-between-a-hard-link-and-a-symbolic-link)

> 透過實際案例直接了解，應該比長篇大論的說明更有效吧

在Linux底下創建兩個檔案  
```bash
touch blah1
touch blah2
```

我們將這兩個檔案加入一些資料  
```bash
echo "Cat" > blah1
echo "Dog" > blah2
```

透過`cat`來看一下檔案輸出的內容為何?
```bash
cat blah1;cat blah2
Cat
Dog
```

我們現在可以創建一個`hard link`以及`soft link`看看...
```bash
ln blah1 blah1-hard
ln -s blah2 blah2-soft
```

接著我們來看看究竟發生了什麼事情
```bash
ls

## 將會顯示
blah1
blah1-hard
blah2
blah2-soft
```

改變blah1的檔案名稱，都將不會影響我們的原本`hard link`的結果呀...  
```bash
mv blah1 blah1-new
cat blah1-hard
#輸出: Cat
```

因為hard link是直接針對`inode`進行綁定bind，因此將不會影響原先連結檔的結果

```bash
mv blah2 blah2-new
ls blah2-soft
blah2-soft
cat blah2-soft
cat: blah2-soft: No such file or directory
```

發現soft link已經無法找到原本內容了，因為soft link是跟`檔案名稱`進行綁定的工作，當檔案名稱改變了，自然我們也無法找到原有的路徑使用。

簡單來說就是，假如blah1被刪除了，blah1-hard仍然可以保有inode上面的內容。然而blah2如果被刪除了，這個檔案的連結將會不再存在。
