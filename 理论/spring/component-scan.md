# component-scan

component-scan的执行过程就是：扫描指定包中的各个类，如果扫描到了@Component以及包含@Component的注解，就创建该类的对象并加入spring容器中。

@Controller、@RestController、@Service、@Repository、@Configuration等都是包含了@Component。如下图所示：

![image-20230312132755462](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230312132755462.png)

@Configuration、@Bean、@ComponentScan都是在org.springframework.context包下的annotation包中。org.springframework.context包是spring的包，所以这些注解都是spring的注解，而不是springboot的注解。



由于@Bean注解中不包含@Component，component-scan会忽略@Bean。但在component-scan找到@Configuration的时候，如果发现了内部的@Bean，则会调用@Bean的这个方法，并将返回的对象放入spring容器中。



