![image-20230114144933006](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230114144933006.png)

![image-20230114145015376](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230114145015376.png)

这就说明，git设置邮箱的时候，111@gmail.com被别人已经用了，导致了我push到github后，记录中显示的是别人的名字。

git是不会检查这个邮箱是否真实存在、这个邮箱是否已经被别人设置。

解决办法就是，git config --global 设置一个其他的email。