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