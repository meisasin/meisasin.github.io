---

layout: post

title:  "Maven 和 Gradle 全局排除依赖及引用外部依赖"

date:   2021-02-09 14:00:00 +0800

categories: gradle

---

<br>

#### 最近公司项目数据库及 web 容器要替换成国产的，数据库替换为神通，tomcat 替换为宝兰德，所以需要排除 Spring boot 自带的一些 Jar 包同时把国产的 Jar 包添加到项目中，国产的 Jar 包没有在 Maven 中央仓库中 。


> Maven 版本：3.6.0
>
> Gradle 版本：6.4.1

##### Maven 排除依赖

- War 包排除依赖

在 `pom.xml` 文件中添加 `maven-war-plugin` 插件, 使用 `packagingExcludes` 标签进行排除

```
		<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.6</version>
                <configuration>
                    <webResources>
                        <resource>
                            <directory>${project.basedir}/lib</directory>
                            <targetPath>WEB-INF/lib</targetPath>
                            <filtering>false</filtering>
                        </resource>
                    </webResources>
                    <dependentWarExcludes>
                        **/services/*.json
                    </dependentWarExcludes>
                    <packagingExcludes>
                        WEB-INF/lib/tomcat-embed-*.jar
                    </packagingExcludes>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

其中 `packagingExcludes` 标签里面的是用来排除不需要的依赖的，这里表示排除以 `tomcat-embed` 开头的`Jar` 包

##### Maven 引用外部依赖(自有依赖)

- War 包引用自有依赖

在 `pom.xml` 文件中添加 `maven-war-plug` 插件, 使用 `webResources` 标签进行引用

```
		<build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>2.6</version>
                <configuration>
                    <webResources>
                        <resource>
                            <directory>${project.basedir}/lib</directory>
                            <targetPath>WEB-INF/lib</targetPath>
                            <filtering>false</filtering>
                        </resource>
                    </webResources>
                    <dependentWarExcludes>
                        **/services/*.json
                    </dependentWarExcludes>
                    <packagingExcludes>
                        WEB-INF/lib/tomcat-embed-*.jar
                    </packagingExcludes>
                </configuration>
            </plugin>
        </plugins>
        <finalName>cas</finalName>
    </build>
```

其中 `webResources` 标签里面的是用来引用自有依赖的，这里表示将 `${project.basedir}/lib` 目录下的内容放到 `WEB-INF/lib` 目录下

##### Gradle 排除依赖

在 `build.gradle` 文件中配置 `configurations` 进行排除

```
configurations {
    compile {
        exclude group: 'org.apache.tomcat.embed'
        exclude group: 'org.springframework.boot', module: 'spring-boot-starter-tomcat'
    }
}
```

`group` 同 `maven`  中的 `groupId`

`module` 同 `maven` 中的 `artifactId`

这里表示排除 `group` 为 `org.apache.tomcat.embed` 的依赖及 `group` 为 `org.springframework.boot` 并且 `module` 为 `spring-boot-starter-tomcat` 的依赖

##### Gradle 引用外部依赖(自有依赖)

在 `build.gradle` 文件中 `dependencies` 进行引用

```
compile fileTree(dir: 'lib', includes: ['*.jar'])
```

表示将 `lib` 目录 (以项目根路径为基准) 下所有以 `jar` 结尾的都引用 

---

参考

- [https://www.imooc.com/article/13041/](https://www.imooc.com/article/13041/)

- [http://www.bubuko.com/infodetail-1876689.html](http://www.bubuko.com/infodetail-1876689.html)

- [https://blog.csdn.net/qq_36838191/article/details/82731158](https://blog.csdn.net/qq_36838191/article/details/82731158)

