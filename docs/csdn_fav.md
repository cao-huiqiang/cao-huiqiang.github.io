# linux
- tar解压到指定的目录```tar -vxf 包名 -C 解压目录```
- Ubuntu安装deb文件包
    ```shell script
    shell> sudo dpkg -i *.deb
    
    #如果报依赖错误执行下面语句再试
    sehll> sudo apt-get -f --fix-missing install
    
    ```
- grep 命令使用
```shell script
# 找出filename中带有keyword的行，输出中除显示该行外，还显示之后的一行(After 1)
shell> grep -A1 keyword filename
# 找出filename中带有keyword的行，输出中除显示该行外，还显示之前的一行(Before 1)
shell> grep -B1 keyword filename
# 找出filename中带有keyword的行，输出中除显示该行外，还显示之前的一行(After 1)和显示之后的一行(After 1）
shell> grep -1 keyword filename
```  

- 查看与停止进程
    ```shell script
    # 在Linux下查看所有java进程命令
    shell> ps -ef | grep java
    # 停止所有java进程命令
    shell> pkill - 9 java
    # 停止特定java进程命令
    shell>kill -9 java进程序号
    ``` 
- Linux终端下显示急驶而过的火车
    ```shell script
    shell>sudo apt install sl
    shell>sl
    ```  
  
# Ubuntu
- Ubuntu16.04完全卸载Mysql 5.7
    ```shell script
    shell> sudo apt purge mysql-*
    shell> sudo rm -rf /etc/mysql/ /var/lib/mysql
    shell> sudo apt autoremove
    shell> sudo apt autoreclean
    ```  
- vi编辑器的方向键无法使用
    ```shell script
    # vi不支持
    shell> sudo apt-get remove vim-common
    shell> sudo apt-get install vim
    ```  
- Ubuntu 用命令行打开当前文件夹 ```nautilus .```  
- nautilus 关闭所有窗口 ```nautilus -q```
 

# vscode
- vscode 如何移除文件夹 ```文件>移除文件夹```

# 谷歌浏览器
- Octotree插件：树形展示Githu项目
- chrome浏览器刷新不清空控制台 ```F12 consle > prserve log```
- json格式化插件: [JSON-Handle插件](http://jsonhandle.sinaapp.com/)
- 重新打开关闭的网页 ```Ctrl+Shift+T```

# Java
- String转JsonObject对象
    ```java
    // fastjson
    public class Test{
        JSONObject jsonObject =JSONObject.parseObject(string);
    }
    ```
- java判断集合list是否为空
    ```java
    public class test{
        if(list!=null && list.size()>0){
        }
        if(list!=null && list.isEmpty()){
        }
    }
    ```
- switch合并相同功能的case语句  
    ```java
    public class test{
        switch (conditon){
            case 1:
            case 2:
                break;
            case 3:
                break;
            default:
        }
    }
    ```
- int转double
    ```java
    int a = 1;
    double c = a;
    ```

- list倒序
    ```java
    Collections.reverse(list);
    ```

# Java8
- lambda 获取list下标
    ```java
    public class Test{
        List<String> list = new ArrayList<>();
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5"); 
        Stream.iterate(0, i -> i + 1).limit(list.size()).forEach(i -> {
            System.out.println(list.get(i));
        });
     
        IntStream.range(0,list.size()).forEach(i->{
            System.out.println(list.get(i));
        });
    
    }
    ```
# spring boot
- spring boot引入内部jar包，打包报错
    - 原pom文件
    ```xml
    <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </build>
    ```
    - 修改后pom文件
    ```xml
    <build>
            <plugins>
                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <configuration>
                        <source>1.8</source>
                        <target>1.8</target>
                        <encoding>UTF-8</encoding>
                    </configuration>
                </plugin>
            </plugins>
        </build>
    ```
    - 原因
    ```text
    pom中定义spring-boot-maven-plugin插件，这个SpringBoot插件会在Maven的package后进行二次打包
    ```
- SpringBoot 配置文件注意事项
    - 如果同一个目录下，有application.yml也有application.properties，默认先读取application.properties。
    - 如果同一个配置属性，在多个配置文件都配置了，默认使用第1个读取到的，后面读取的不覆盖前面读取到的。

    原文地址：(https://my.oschina.net/sdlvzg/blog/1612703) 

- spring boot banner
    - 修改
        0. 在src/main/resources 下新建banner.txt
        0. 通过 http://patorjk.com/software/taag 生成文字
        0. 复制生成文字到新建的banner.txt中
    - 使用自带变量
        ```text
        #这个是MANIFEST.MF文件中的版本号 
        ${application.version}              
        #这个是上面的的版本号前面加v后上括号 
        ${application.formatted-version}
        #这个是springboot的版本号 
        ${spring-boot.version}             
        #这个是springboot的版本号 
        ${spring-boot.formatted-version}
        ```
    - 重写接口Banner实现
        ```text
        SpringBoot提供了一个接口org.springframework.boot.Banner，
        它的实例可以被传给SpringApplication的setBanner(banner)方法
        ``` 
    - 禁用/启用   
        - 启动类main方法禁用
            ```java
            SpringApplication app = new SpringApplication(xxxxxx.class);
            // app.setShowBanner(false); // spring boot 1.x 用法？
            app.setBannerMode(Banner.Mode.OFF);
            app.run(args);
            ```
        - 使用fluent API禁用
            ```java
            new SpringApplicationBuilder(xxxxxx.class)
                .showBanner(false)
                .run(args);
            ```
        - 配置禁用 
        ```properties
        spring.main.banner-mode=off
        spring.main.show-banner=false
        ``` 
    
##  spring boot 2.x      
- Spring Boot 2.0 的Actuator暴露端点 
    ```properties
    management.endpoints.web.exposure.include=*
  #  management.endpoints.web.exposure.include=env,health
    ```  
- Spring Boot 2.0 的Actuator接口访问需要添加```/actuator```
- Spring Boot 文件上传大小设置
    ```text
    The field file exceeds its maximum permitted size of 1048576 bytes
    ```
    - spring boot 1.x
        ```properties
        # MULTIPART (MultipartProperties)
        spring.http.multipart.enabled=true # Enable support of multi-part uploads.
        spring.http.multipart.file-size-threshold=0 # Threshold after which files will be written to disk. Values can use the suffixed "MB" or "KB" to indicate a Megabyte or Kilobyte size.
        spring.http.multipart.location= # Intermediate location of uploaded files.
        spring.http.multipart.max-file-size=1MB # Max file size. Values can use the suffixed "MB" or "KB" to indicate a Megabyte or Kilobyte size.
        spring.http.multipart.max-request-size=10MB # Max request size. Values can use the suffixed "MB" or "KB" to indicate a Megabyte or Kilobyte size.
        spring.http.multipart.resolve-lazily=false # Whether to resolve the multipart request lazily at the time of file or parameter access.
        ```
    - spring boot 2.x
        ```properties
        # MULTIPART (MultipartProperties)
        spring.servlet.multipart.enabled=true # Whether to enable support of multipart uploads.
        spring.servlet.multipart.file-size-threshold=0 # Threshold after which files are written to disk. Values can use the suffixes "MB" or "KB" to indicate megabytes or kilobytes, respectively.
        spring.servlet.multipart.location= # Intermediate location of uploaded files.
        spring.servlet.multipart.max-file-size=1MB # Max file size. Values can use the suffixes "MB" or "KB" to indicate megabytes or kilobytes, respectively.
        spring.servlet.multipart.max-request-size=10MB # Max request size. Values can use the suffixes "MB" or "KB" to indicate megabytes or kilobytes, respectively.
        spring.servlet.multipart.resolve-lazily=false # Whether to resolve the multipart request lazily at the time of file or parameter access.
        ```
     ```https://docs.spring.io/spring-boot/docs/```
     
- 查看路由信息 ```http://localhost:8088/actuator/gateway/routes```
- 查看限流熔断 ```http://localhost:8088/actuator/sentinel```



# idea
- idea中添加try/catch的快捷键
 ```选中需要被try/catch包围的语句，按下Ctrl+Alt+T```
 
- idea向上建立一空行 ```Ctrl+Alt+Enter，行首，Ctrl + Enter```

- idea向下建立一空行 ```Ctrl+Shift+Enter```

- 查看过期插件
```idea插件搜索框输入，/outdated ```

- idea社区 (https://intellij-support.jetbrains.com/hc/en-us/community/posts)

- idea for 循环 快捷键 ```list.for Tab```
- idea 变量拆分 ```Alt+Enter```

- idea 代码抽取 ```右键 > refactor > extract```

- idea alt+8 可以跳出services ，添加application后和run dashboard 类似

- idea 注释```//```后添加空格
```ctrl + / -> settings->java-> code geration-> line comment,  add a space```


# mysql 
- sql脚本注释问题 ```-- 注释内容（注意要有空格）```
- MySQL workbench几个常用快捷键
    ```text
    执行整篇或选中sql脚本， ctrl+shift+enter
    执行当前行，ctrl+enter
    注释/取消注释， ctrl+/
    格式化sql语句（美化sql语句）， ctrl+b
    自动补全，ctrl+space
    ```
- MySQL中清屏幕 
    - windows wu
    - linux ```clear或\c```  

# other

- 链接收藏  
    [v2ex](https://www.v2ex.com/) 
    [HelloGitHub](https://github.com/521xueweihan/HelloGitHub) 

- WebStorm设置Ctrl+滚轮调整字体大小
    ```text
    File > setting > Editor > General > Change font size (Zoom) with Ctrl+Mouse Wheel
    ```    
- vim 操作  
    - 定位至首行： ```:0, :1, gg```
    - 定位至末行：```:$ Enter, :G```
    - 移动至行首：```:^```
    - 移动至行尾：```:1$```
    - 移动至下一行行尾：```:2$```
    - 暂时显示行数：```:set number``
    - 永久显示行数：```/etc/vim/vimrc 文件中添加set number```
    - 跳转到指定行数：```:number```
    
- Xshell不能使用退格、删除键
    ```文件-->打开--->属性-->终端 -->键盘 把delete和backspace序列改为 ASCII 127```  
    
- Sublime Text3 设置自动保存
    ```text
    preference > settings , 右侧添加
    {
        "font_size": 14,
        "save_on_focus_lost": true
    }
    ``` 

- windows命令
    - 切换盘目录 ```>d:```  
    - 清屏 ```cls```
- ```&apos;```===```'```
- windows 下使用tree命令
    - 打开cmd （git Bash不行）
    - 输入```tree```或```tree /f```
- 微软拼音简繁体切换```ctrl+shift+f```，可设置关闭
- redis设置密码
    ```shell script
    shell> config set requirepass password
    shell> auth password
    shell> confg get requirepass
    ```
    
