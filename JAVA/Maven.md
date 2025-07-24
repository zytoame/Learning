1. 常用命令cmd
	1. mvn clean：删除target文件夹
	2. mvn compile    # 编译代码
	3. mvn test       # 运行测试
	4. mvn package    # 打包为 JAR/WAR
	5. mvn install    # 安装到本地仓库
2. 生命周期内，执行后边的命令，前边的所有命令会自动执行
	1. clean
	2. default：核心工作：编译，测试，打包。安装
	3. site
3. 坐标
	1. groupId：定义当前maven项目隶属组织名称
	2. artifactId：定义当前maven项目名称
	3. version：当前版本号
4. 依赖管理
	1. 使用坐标导入jar包：在pom.xml中快捷键alt+fn+insert，进行搜索
		1. 在pom.xml中编写< dependencies>标签
		2. 在标签中使用 < dependency>引入坐标
		3. 定义坐标的 groupId , artifactId, version
		4. 点击刷新坐标，使坐标生效
	2. 依赖范围< scope>
		1. compxxx
		2. test
		3. provided


Maven Web项目
![Pasted image 20250706154748](https://kmk1132-obs-1370539359.cos.ap-guangzhou.myqcloud.com/Pasted%20image%2020250706154748.png)