# 通用Mapper

## 1.1   为什么用通用Mapper?

​	       解放双手，不写sql，也不用写Mapper接口中的内容。只需要Mapper接口 extends Mapper<T>即可，接口中不需要写任何东西。这个T要写Bean类。Bean类中要用到@Id(表示主键) , @Column。

