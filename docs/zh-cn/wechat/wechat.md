
## 2023年10月25日

### 近日见闻

1. 语雀宕机超过7小时，影响用户正常使用，已经发公告解释了原因和赔偿方案，给与用户半年会员。 --语雀

2. GOPS 全球运维大会2023 · 上海站，10月26日-27日上海站即将正式举行 --GOPS社区

3. 青云科技近日发布 KubeSphere 企业版 3.5.0（以下简称 KSE v3.5.0），致力于为企业提供更优质、更高效的容器应用体验。 --Kubesphere

4. 文档网站上线，历史文章各位可查看docs.cillian.website --希里安

## java常用注解

当使用Spring Boot进行应用程序开发时，常常需要使用各种注解来简化配置、处理依赖注入以及定义特定行为。以下是更详细的介绍和示例，以帮助您更好地了解Spring Boot中一些常用的注解：

1. `@SpringBootApplication`:
   - 用途：这个注解是Spring Boot应用程序的主要入口点。它结合了`@Configuration`、`@EnableAutoConfiguration`和`@ComponentScan`，自动配置应用程序并扫描包中的组件。
   - 示例：
     ```java
     @SpringBootApplication
     public class MyApplication {
         public static void main(String[] args) {
             SpringApplication.run(MyApplication.class, args);
         }
     }
     ```

2. `@RestController`:
   - 用途：标识一个类为RESTful控制器，它用于处理HTTP请求并返回数据，通常以JSON格式。
   - 示例：
     ```java
     @RestController
     public class MyController {
         @GetMapping("/hello")
         public String hello() {
             return "Hello, World!";
         }
     }
     ```

3. `@RequestMapping`:
   - 用途：用于映射HTTP请求到处理方法，并可以指定请求路径和HTTP方法。
   - 示例：
     ```java
     @RestController
     @RequestMapping("/api")
     public class MyController {
         @GetMapping("/hello")
         public String hello() {
             return "Hello, World!";
         }
     }
     ```

4. `@Autowired`:
   - 用途：自动装配依赖对象，通常用于注入Spring Bean。它可以用在字段、构造函数、或setter方法上。
   - 示例：
     ```java
     @Service
     public class MyService {
         @Autowired
         private MyRepository repository;
     }
     ```

5. `@Service`, `@Repository`, `@Component`:
   - 用途：这些注解用于将类标识为Spring管理的组件。`@Service`通常用于业务逻辑层，`@Repository`用于数据访问层，而`@Component`是一个通用的组件标识。
   - 示例：
     ```java
     @Service
     public class MyService {
         // ...
     }

     @Repository
     public class MyRepository {
         // ...
     }
     ```

6. `@Configuration`:
   - 用途：标识一个类为Spring配置类，通常用于定义Bean和配置。这对于将第三方组件集成到应用程序中非常有用。
   - 示例：
     ```java
     @Configuration
     public class MyConfig {
         @Bean
         public DataSource dataSource() {
             // 配置数据源并返回
         }
     }
     ```

7. `@Value`:
   - 用途：通过该注解可以将外部属性值注入到Spring Bean中。
   - 示例：
     ```java
     @Component
     public class MyComponent {
         @Value("${my.property}")
         private String myProperty;
     }
     ```

8. `@EnableAutoConfiguration`:
   - 用途：开启Spring Boot的自动配置功能，根据应用程序的依赖自动配置应用程序。
   - 示例：通常由`@SpringBootApplication`自动包含。

9. `@Entity`:
   - 用途：用于JPA实体类的标识。它指示该类将映射到数据库表。
   - 示例：
     ```java
     @Entity
     public class User {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         private String username;
         // ...
     }
     ```

这些注解代表了Spring Boot应用程序中的常见构建块，它们帮助简化配置、依赖注入和处理HTTP请求等任务。根据您的应用程序需求，还可以使用其他Spring Boot注解来实现更多特定功能。这些注解是Spring Boot框架的核心，使开发变得更加高效且易于维护。


## 2023年10月24日

### 近日见闻

1. 1024程序员节快乐！

2. NGINX 推出 Plus Release 30 (R30) 版本。NGINX Plus 基于 NGINX 开源版构建而成，是唯一一款将软件 Web 服务器、负载均衡器、反向代理、内容缓存和 API 网关集于一身的多合一产品。 --Nginx社区

3. OpenTiny Vue 3.11.0 发布：增加富文本、ColorPicker等4个新组件，迎来了贡献者大爆发！ --前端开源星球

4. 有读者朋友建议我分享运维工作经验或者日常问题解决经验，我尽快总结分享，欢迎关注文档网站：docs.cillian.website



### Java21创建一个Springboot应用


**步骤 1：设置开发环境**

首先，安装Java Development Kit（JDK），可以从Oracle或OpenJDK下载并安装。Java版本要兼容Spring Boot。比如springboot3最低要求java17。我们直接下载安装openjdk21，并设置好环境变量。

**步骤 2：创建Spring Boot项目**

使用Spring Initializer（https://start.spring.io/）或在IDE中创建新的Spring Boot项目。

1. 打开浏览器，访问Spring Initializer网站。
2. 在该网站上，选择项目的基本设置，包括项目名称、描述、包名、Java版本等，选择spring web依赖。
3. 点击"Generate"按钮生成项目。
4. 下载生成的项目文件，通常是一个zip压缩包。
5. 解压缩项目文件，并导入到您的IDE中。

**步骤 3：编写Spring Boot应用程序**

在项目中，可以开始编写Spring Boot应用程序代码。比如创建一个RESTful Web服务：

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class MySpringBootApplication {

    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApplication.class, args);
    }
}

@RestController
class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}
```

这个示例创建了一个Spring Boot应用程序，其中包含一个HelloController，用于处理HTTP GET请求并返回"Hello, Spring Boot!"。

**步骤 4：运行应用程序**

在IDE中运行应用程序，或者使用以下命令行命令来运行：

```
./mvnw spring-boot:run
```

**步骤 5：测试应用程序**

也可以使用浏览器或工具如curl或Postman来测试应用程序。在浏览器中输入`http://localhost:8080/hello`，应该能够看到"Hello, Spring Boot!"的响应。

**步骤 6：打包应用程序**

使用以下命令将应用程序打包成可执行的JAR文件：

```
./mvnw clean package
```

打包后的JAR文件通常会位于`target`目录下。

**步骤 7：部署应用程序**

将打包好的JAR文件部署到目标服务器或云平台上。通常，可以使用`java -jar your-app.jar`来运行应用程序。

**步骤 8：配置应用程序**

Spring Boot允许您在`application.properties`或`application.yml`文件中配置应用程序属性，例如端口号、数据库连接等。以下是一个`application.properties`文件的示例：

```properties
# 应用程序端口号
server.port=8080

# 数据库连接配置
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=username
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

这只是一个简单的示例，Spring Boot支持更多功能和配置选项，具体取决于项目需求。可以根据需求进一步扩展和定制应用程序。






## 2023年10月20日

### 近日见闻

1. 微软最近宣布，Azure Database 将放弃对 MariaDB 的支持。在接下来的几个月里，用户将不能通过控制台或 CLI 创建新的 MariaDB 数据库，现有的实例计划在 2025 年到期。--https://www.infoq.com/news/2023/09/azure-database-mariadb/

2. 2023年10月16日，vivo在官方微博宣布，将于11月1日举办开发者大会，并将发布vivo自研AI大模型，引领手机智慧体验变革。--vivo社区

3. 国考报名四天人数超63万！单日将近20万！ --新闻

### 日常sidecar运用


在Kubernetes（通常简称为K8s）中，"Sidecar" 是指一种容器模式，其中一个容器（主容器）与一个或多个辅助容器（Sidecar容器）一起运行在同一个Pod中。这种模式允许在一个Pod中同时运行多个容器，每个容器可以独立执行不同的任务，但它们共享相同的网络和存储命名空间，可以相互通信和协同工作。

以下是一个示例，假设您正在运行一个Web应用程序，需要记录应用程序日志。您可以使用一个主容器来运行您的Web应用程序，同时使用一个Sidecar容器来记录应用程序的日志。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
spec:
  containers:
    - name: web-app
      image: my-web-app:1.0
      ports:
        - containerPort: 80
    - name: log-sidecar
      image: log-processor:1.0
```

在上面的示例中，我们定义了一个Pod，其中包含两个容器：`web-app` 和 `log-sidecar`。`web-app` 容器运行您的Web应用程序，而 `log-sidecar` 容器运行一个用于处理和记录日志的服务。这两个容器在同一个Pod中运行，它们可以共享相同的网络和存储，以便 `web-app` 可以将日志发送给 `log-sidecar` 进行处理，然后 `log-sidecar` 负责将日志保存到适当的位置。

这种模式的好处包括了解耦、易于管理和维护。您可以根据需要添加或删除Sidecar容器，而无需对主应用程序进行修改。


### 怎么维护sidecar

在Kubernetes中，维护Sidecar容器的数量可能会涉及到一些管理和运维任务，特别是在多个Sidecar容器之间需要协同工作，以确保应用程序的稳定性和性能。以下是关于维护Sidecar容器的一些建议：

1. **监控和日志记录**：确保在整个Pod中监控主容器和所有Sidecar容器的性能和日志记录。使用适当的监控和日志记录工具，以便及时检测问题并采取必要的纠正措施。

2. **版本管理**：Sidecar容器的镜像版本应该与主应用程序的镜像版本保持一致，以防止不兼容或冲突的问题。在部署新版本时，确保所有容器都更新为最新版本。

3. **资源管理**：管理Pod的资源请求和限制，以确保Pod中的所有容器都有足够的资源来运行。不同容器可能需要不同的资源配置，因此需要根据各容器的需求来调整。

4. **容器间通信**：确保Sidecar容器能够与主容器进行正确的通信，以便执行协同工作。这可能需要适当的网络策略和服务发现机制。

5. **容器健康检查**：配置适当的健康检查以确保主容器和Sidecar容器都正常运行。这有助于自动故障恢复和替代。

6. **自动扩展**：如果需要，使用Kubernetes的自动扩展功能来动态调整Pod的副本数量，以满足应用程序的需求。这可以确保Sidecar容器能够处理负载的增加。

7. **升级策略**：定义升级策略，以确保在进行主容器或Sidecar容器的更新时不会导致应用程序中断。可以使用滚动升级或蓝绿部署等策略来管理更新。

8. **文档和标准**：为团队创建清晰的文档和标准，以规范化Sidecar容器的使用和维护。这有助于确保一致性和可维护性。

9. **灾难恢复计划**：制定灾难恢复计划，以应对主容器或Sidecar容器中的故障。这可以包括备份和恢复策略。

10. **安全性**：确保所有容器都受到适当的安全措施的保护，以防止潜在的威胁。

维护多个Sidecar容器需要仔细的计划和管理，以确保整个应用程序在长期运行中保持稳定和高效。这涉及到监控、调整资源、升级管理、文档化和灾难恢复计划等多个方面。在实践中，根据具体应用的需求来制定和实施维护策略。



## 2023年10月20日

1. 安全内参10月18日消息，今年5月至9月期间，有官方背景的俄罗斯黑客组织“沙虫”（Sandworm）已经成功侵入11家乌克兰电信公司。 --安全内参

2. Tekton 是一个用于创建持续集成和持续交付（CI/CD）系统的 Kubernetes 原生开源框架。通过对底层实施细节的抽象，它还可以帮助你在多个云供应商或企业内部系统中进行端到端（构建、测试、部署）应用开发。 --Linux社区

3. 「RTE 2023 第九届实时互联网大会」定档 10.24-10.25 --RTE

### TS与JS

当比较TypeScript（TS）和JavaScript（JS）时，以下是详细的区别：

1. **类型系统**：
   - **JavaScript**：JavaScript是一种动态类型语言，这意味着变量的类型在运行时确定，你可以随时改变一个变量的类型。
   - **TypeScript**：TypeScript是一种静态类型语言，你需要在编码阶段为变量、函数参数和返回值等显式定义类型注解。类型注解可以帮助编译器检测潜在的类型错误，提高代码的可靠性和可维护性。

2. **编译**：
   - **JavaScript**：JavaScript代码可以直接在浏览器或Node.js中运行，无需编译过程。
   - **TypeScript**：TypeScript代码需要经过编译，编译器将TypeScript代码转换为JavaScript代码。这个过程会去除类型注解，并将TypeScript特有的语法转换为标准的JavaScript，以便在浏览器或Node.js中执行。

3. **语法**：
   - **JavaScript**：JavaScript的语法相对灵活，可以在不严格遵循规范的情况下编写代码。
   - **TypeScript**：TypeScript引入了一些新的语法，如类型注解、接口、枚举、泛型等，以增强代码的可读性和可维护性。这些语法在编译时进行类型检查，并提供更多的开发工具支持。

4. **工具支持**：
   - **JavaScript**：JavaScript的开发工具有很多，但它们主要专注于语法高亮和基本的错误检查。
   - **TypeScript**：TypeScript拥有更强大的开发工具支持，如自动完成、智能重构、类型检查、导航等，这些功能可以提高开发效率和代码质量。

5. **生态系统**：
   - **JavaScript**：JavaScript拥有巨大而成熟的生态系统，有大量的第三方库和框架可供选择，用于前端和后端开发，以及各种其他应用。
   - **TypeScript**：TypeScript可以无缝与JavaScript生态系统集成，同时还有一个类型声明文件（.d.ts文件）生态系统，用于描述第三方JavaScript库的类型信息。这使得使用TypeScript开发时能够享受类型安全，同时仍然能够利用广泛的JavaScript库。

TypeScript是JavaScript的一个超集，它添加了类型系统和其他功能，旨在提高代码的可维护性和可读性。选择使用哪种语言取决于项目需求、开发团队的偏好以及个人偏好。较大、复杂的项目通常更容易受益于TypeScript的类型检查和工具支持，而小型项目可能更适合使用JavaScript的灵活性。

---
## 2023年10月19日

1. 10 月 17 日，Node.js 21 正式发布，其取代了 Node.js 20 成为当前版本，而 Node.js 20 则被推广为长期支持版本（LTS）。 --NodeJS

2. 10月17日，拜登政府决定停止向中国输送高性能的人工智能芯片，其中包括GPU A100、H100、A800、H800、L40、L40S 以及 RTX4090。 --新闻

3. 11月4日，云原生+ AI Meetup成都站即将开启！--CNCF

4. 大厂离职就打低绩效，已成常规操作？--招聘社区


### 静态、动态路由的使用

当你构建一个Vue.js应用时，你需要考虑如何管理和配置路由，以便导航到不同的页面或视图。路由可以分为两种主要类型：静态路由和动态路由，下面我将进一步详细解释它们。

#### 静态路由（Static Routes）

1. **定义方式**：静态路由是在应用的路由配置中提前定义的路由规则。这些规则在应用启动时就被确定，通常在路由配置文件中硬编码。

2. **用途**：静态路由通常用于表示应用中的一些常规页面，如主页、关于页面、联系页面等。这些页面的路由规则在开发时就已经确定，不会发生变化。

3. **示例**：以下是一些静态路由的示例，它们都是在路由配置文件中提前定义的：

```javascript
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  { path: '/contact', component: Contact }
];
```

#### 动态路由（Dynamic Routes）

1. **定义方式**：动态路由是在应用运行时根据数据或其他条件来动态生成的路由规则。这种路由通常用于处理具有可变参数的页面。

2. **用途**：动态路由通常用于处理需要根据不同参数显示不同内容的页面，例如博客文章详情页面，每篇文章都有不同的标识，或用户个人资料页面，每个用户都有不同的标识。

3. **示例**：以下是一些动态路由的示例，它们包含了动态参数，参数的值是根据实际路由匹配而变化的：

```javascript
const routes = [
  { path: '/blog/:id', component: BlogPost },
  { path: '/profile/:username', component: UserProfile }
];
```

在动态路由中，`:id`和`:username`都是动态参数，它们的值会根据实际路由匹配而变化。你可以在组件中使用这些参数来获取相应的数据并呈现在页面上。

静态路由是在开发时定义的固定路由规则，而动态路由是在运行时根据数据或用户输入动态生成的路由规则。你可以根据应用的需求和路由配置来选择使用静态路由、动态路由或两者结合，以构建你的Vue.js应用。