# maven 中实现Junit测试 #
一.在项目的pom.xml下加入以下代码
```
//这个为Junit的依赖，它嵌套在<dependencies>标签中
<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<version>4.12</version>
</dependency>

//其中build标签和<dependencies>标签同级
<build>
    <pluginManagement>
        <plugins>
            <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>2.20</version>
            </plugin>
        </plugins>
    </pluginManagement>
</build>

```

二.在src\test\resources下面创建测试代码，注意这里的测试代码的目录，maven的Junit插件会自动找到这个目录下的测试代码。
```
public class TestJenkins {
	@Test
	public void jenkinsTest(){
		int i;
		String a;
		Devops d=new Devops("我的devops","devops-poc1");
		System.out.println(d.getJenkins()+d.getName());
	}
}

```