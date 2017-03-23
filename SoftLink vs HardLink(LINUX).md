# ����O�w�s�� ����O�n�s��
![�Ϫ����](https://i.stack.imgur.com/f7Ijz.jpg)

reference link: [ubuntuAsk](http://askubuntu.com/questions/108771/what-is-the-difference-between-a-hard-link-and-a-symbolic-link)

> �z�L��ڮרҪ����F�ѡA���Ӥ���g�j�ת������󦳮ħa

�bLinux���U�Ыب���ɮ�  
```bash
touch blah1
touch blah2
```

�ڭ̱N�o����ɮץ[�J�@�Ǹ��  
```bash
echo "Cat" > blah1
echo "Dog" > blah2
```

�z�L`cat`�Ӭݤ@�U�ɮ׿�X�����e����?
```bash
cat blah1;cat blah2
Cat
Dog
```

�ڭ̲{�b�i�H�Ыؤ@��`hard link`�H��`soft link`�ݬ�...
```bash
ln blah1 blah1-hard
ln -s blah2 blah2-soft
```

���ۧڭ̨Ӭݬݨs���o�ͤF����Ʊ�
```bash
ls

## �N�|���
blah1
blah1-hard
blah2
blah2-soft
```

����blah1���ɮצW�١A���N���|�v�T�ڭ̪��쥻`hard link`�����G�r...  
```bash
mv blah1 blah1-new
cat blah1-hard
#��X: Cat
```

�]��hard link�O�����w��`inode`�i��j�wbind�A�]���N���|�v�T����s���ɪ����G

```bash
mv blah2 blah2-new
ls blah2-soft
blah2-soft
cat blah2-soft
cat: blah2-soft: No such file or directory
```

�o�{soft link�w�g�L�k���쥻���e�F�A�]��soft link�O��`�ɮצW��`�i��j�w���u�@�A���ɮצW�٧��ܤF�A�۵M�ڭ̤]�L�k���즳�����|�ϥΡC

²��ӻ��N�O�A���pblah1�Q�R���F�Ablah1-hard���M�i�H�O��inode�W�������e�C�M��blah2�p�G�Q�R���F�A�o���ɮת��s���N�|���A�s�b�C
