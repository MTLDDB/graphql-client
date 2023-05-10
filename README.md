# English

## Graphql Client
The project is graphql client for java,support custom query and mutation.

The current version only supports post requests

You need java1.7 and maven.

Just changed some dependencies to accommodate java7.
Please copy the source code to your computer and use java7 to compile and package it.
Due to the use of local packages, Maven's dependency delivery was interrupted, and some dependencies needed for the project need to be added.Or upload the package to Maven's private server

## Update 1.2 Note

Requested parameters support custom complex types and Enum types.


## Use You Project

maven dependency.

	<dependency>
		<groupId>org.mountcloud</groupId>
		<artifactId>graphql-client</artifactId>
		<version>1.2-java7</version>
		<scope>system</scope>
		<systemPath>${project.basedir}/lib/graphql-client-1.2-java7.jar</systemPath>
	</dependency
	<!--some dependencies needed for the project need to be added-->
	 <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jdk7</artifactId>
            <version>2.6.7</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.5.3</version>
        </dependency>

        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.5.3</version>
        </dependency>

## Insall Project

	mvn install


## Demo 

do query

```Java
//crate client
GraphqlClient client = GraphqlClient.buildGraphqlClient("http://localhost:8081/graphql");
//create http headers
Map<String,String> headers = new HashMap<String,String>();
headers.put("token","123");
client.setHttpHeaders(headers);
//create query
GraphqlQuery query = new DefaultGraphqlQuery("findUsers");
//add query or mutation param
query.addParameter("sex","man").addParameter("age",11);
//add query response basics attribute
query.addResultAttributes("id","name","age","sex");
//add query complex attributes
ResultAttributtes classAttributte = new ResultAttributtes("class");
classAttributte.addResultAttributes("name","code");
//attributes can be more complex
ResultAttributtes schoolAttributte = new ResultAttributtes("school");
schoolAttributte.addResultAttributes("name");
//class add school attribute
classAttributte.addResultAttributes(schoolAttributte);
//do query
try {
    GraphqlResponse response = client.doQuery(query);

    //this map is graphql result
    Map data = response.getData();

} catch (IOException e) {
    e.printStackTrace();
}
```

query is

```Java
query{
  findUsers(sex:"man",age:11){
    id
    name
    age
    sex
    class{
    	name
	code
	school{
	  name
	}
    }
  }
}
```


do mutation

```Java
//crate client
GraphqlClient client = GraphqlClient.buildGraphqlClient("http://localhost:8081/graphql");
//create http headers
Map<String,String> headers = new HashMap<String,String>();
headers.put("token","123");
client.setHttpHeaders(headers);
//create mutaion
GraphqlMutation mutation = new DefaultGraphqlMutation("updateUser");
//create param
mutation.addParameter("id",1).addParameter("name","123").addParameter("age",18);
//add more complex attribute to see do query demo

//result
mutation.addResultAttributes("code");
try {
    GraphqlResponse response = client.doMutation(mutation);
    //this map is graphql result
    Map data = response.getData();
} catch (IOException e) {
    e.printStackTrace();
}
```

mutation is

```Java
mutation{
  updateUser(id:1,name:"123",age:18){
    code
  }
}
```

## Complex structure request demo

Mutation demo,The query is consistent with the mutation.


```Java
    @Test
    public void testObjectParameter() throws IOException {


        
        String serverUrl = "http://localhost:8080/graphql";
        
        GraphqlClient graphqlClient = GraphqlClient.buildGraphqlClient(serverUrl);

        
        Map<String,String> httpHeaders = new HashMap<>();
        httpHeaders.put("token","graphqltesttoken");
        
        graphqlClient.setHttpHeaders(httpHeaders);

        GraphqlMutation mutation = new DefaultGraphqlMutation("addUser");

        List<User> users = new ArrayList<>();
        users.add(new User("tim",SexEnum.M));
        users.add(new User("sdf",SexEnum.F));
        mutation.getRequestParameter().addParameter("classId","123").addObjectParameter("users",users);

        mutation.addResultAttributes("code");

        System.out.println(mutation.toString());

    }

    /**
     * test user
     */
    class User{
        public User(String name, SexEnum sexEnum) {
            this.name = name;
            this.sexEnum = sexEnum;
        }

        private String name;
        private SexEnum sexEnum;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public SexEnum getSexEnum() {
            return sexEnum;
        }

        public void setSexEnum(SexEnum sexEnum) {
            this.sexEnum = sexEnum;
        }
    }

    /**
     * test user sex
     */
    enum SexEnum{
        M,
        F
    }
```

mutation is

```Java
mutation{
  addUser(classId:"123",users:[{name:"tim",sexEnum:M},{name:"sdf",sexEnum:F}]){
    code
  }
}
```

# 中文

## Graphql Client
该项目是java的graphql客户端，支持自定义query和mutation.

当前版本仅支持post请求

您需要java1.7和maven。

更改了一些依赖项以适应java7。

请将源代码复制到您的计算机上，并使用java7对其进行编译和打包。

由于使用本地包，Maven的依赖项传递中断，需要添加项目所需的一些依赖项。或者将包上传到Maven的私有服务器


## 更新 1.2 日志

请求的参数支持自定义复杂类型和Enum类型。


## 使用方式

maven:

	<dependency>
		<groupId>org.mountcloud</groupId>
		<artifactId>graphql-client</artifactId>
		<version>1.2-java7</version>
		<scope>system</scope>
		<systemPath>${project.basedir}/lib/graphql-client-1.2-java7.jar</systemPath>
	</dependency
	<!--some dependencies needed for the project need to be added-->
	 <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jdk7</artifactId>
            <version>2.6.7</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-core</artifactId>
            <version>2.5.3</version>
        </dependency>

        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.5.3</version>
        </dependency>

## Insall Project

	mvn install


## Demo 

do query

```Java
//crate client
GraphqlClient client = GraphqlClient.buildGraphqlClient("http://localhost:8081/graphql");
//create http headers
Map<String,String> headers = new HashMap<String,String>();
headers.put("token","123");
client.setHttpHeaders(headers);
//create query
GraphqlQuery query = new DefaultGraphqlQuery("findUsers");
//add query or mutation param
query.addParameter("sex","man").addParameter("age",11);
//add query response basics attribute
query.addResultAttributes("id","name","age","sex");
//add query complex attributes
ResultAttributtes classAttributte = new ResultAttributtes("class");
classAttributte.addResultAttributes("name","code");
//attributes can be more complex
ResultAttributtes schoolAttributte = new ResultAttributtes("school");
schoolAttributte.addResultAttributes("name");
//class add school attribute
classAttributte.addResultAttributes(schoolAttributte);
//do query
try {
    GraphqlResponse response = client.doQuery(query);

    //this map is graphql result
    Map data = response.getData();

} catch (IOException e) {
    e.printStackTrace();
}
```

query is

```Java
query{
  findUsers(sex:"man",age:11){
    id
    name
    age
    sex
    class{
    	name
	code
	school{
	  name
	}
    }
  }
}
```


do mutation

```Java
//crate client
GraphqlClient client = GraphqlClient.buildGraphqlClient("http://localhost:8081/graphql");
//create http headers
Map<String,String> headers = new HashMap<String,String>();
headers.put("token","123");
client.setHttpHeaders(headers);
//create mutaion
GraphqlMutation mutation = new DefaultGraphqlMutation("updateUser");
//create param
mutation.addParameter("id",1).addParameter("name","123").addParameter("age",18);
//add more complex attribute to see do query demo

//result
mutation.addResultAttributes("code");
try {
    GraphqlResponse response = client.doMutation(mutation);
    //this map is graphql result
    Map data = response.getData();
} catch (IOException e) {
    e.printStackTrace();
}
```

mutation is

```Java
mutation{
  updateUser(id:1,name:"123",age:18){
    code
  }
}
```

## 如何实现一个复杂请求

用Mutation做演示,query与mutation原理一样.


```Java
    @Test
    public void testObjectParameter() throws IOException {


        
        String serverUrl = "http://localhost:8080/graphql";
        
        GraphqlClient graphqlClient = GraphqlClient.buildGraphqlClient(serverUrl);

        
        Map<String,String> httpHeaders = new HashMap<>();
        httpHeaders.put("token","graphqltesttoken");
        
        graphqlClient.setHttpHeaders(httpHeaders);

        GraphqlMutation mutation = new DefaultGraphqlMutation("addUser");

        List<User> users = new ArrayList<>();
        users.add(new User("tim",SexEnum.M));
        users.add(new User("sdf",SexEnum.F));
        mutation.getRequestParameter().addParameter("classId","123").addObjectParameter("users",users);

        mutation.addResultAttributes("code");

        System.out.println(mutation.toString());

    }

    /**
     * test user
     */
    class User{
        public User(String name, SexEnum sexEnum) {
            this.name = name;
            this.sexEnum = sexEnum;
        }

        private String name;
        private SexEnum sexEnum;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public SexEnum getSexEnum() {
            return sexEnum;
        }

        public void setSexEnum(SexEnum sexEnum) {
            this.sexEnum = sexEnum;
        }
    }

    /**
     * test user sex
     */
    enum SexEnum{
        M,
        F
    }
```

mutation is

```Java
mutation{
  addUser(classId:"123",users:[{name:"tim",sexEnum:M},{name:"sdf",sexEnum:F}]){
    code
  }
}
```
