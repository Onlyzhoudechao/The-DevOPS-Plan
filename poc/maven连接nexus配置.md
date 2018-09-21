# maven连接nexus配置 #

1.第一需要修改maven的setting这个配置文件
```
  <servers>
	<server>
        <id>maven-releases</id>
        <username>admin</username>
        <password>admin123</password>
        </server>
        <server>
        <id>maven-snapshots</id>
        <username>admin</username>
        <password>admin123</password>
    </server>
  </servers>


 
```

2.在pom.xml中加入以下配置
```
<distributionManagement>  
        <repository>  
            <id>仓库id</id>  
            <name>nexus</name>  
            <url>http://139.219.102.213:8081/repository/maven-releases/</url>  
        </repository>  
        <snapshotRepository>
            <id>nexus-snapshot</id>
            <url>http://139.219.102.213:8081/repository/maven-snapshots/</url>
        </snapshotRepository>
</distributionManagement>

这个标签和build同级的
```

3.maven同jenkins的Junit配置，需要在pom.xml下面加入以下内容
```
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

//这个为Junit的依赖
<dependencies>
  	<!-- junit -->
		<!-- https://mvnrepository.com/artifact/junit/junit -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
		</dependency>
  </dependencies>
```
