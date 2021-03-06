[Core Data Programming Guide]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/cdProgrammingGuide.html#//apple_ref/doc/uid/TP30001200-SW1)

Core Data 的特性
==================

>
- change tracking and undo support
- relationship maintenance: change propagation
- futures: lazy loading
- automatic property value validation
- schema migration
- integration with application's controller to support UI sync
- support key-value coding and observing
- grouping, filtering and organizing data in memory and UI
- support for storing data in external data repositories
- sophisticated query compilation
- merge policies

为什么要用Core Data?
=============================
>
- reduce the amount of code you write to support model layer of your app
- widely used, highly optimized, offers best memory scalability
- integrates well with OS X tool chain: graphic design tool, debug tool


- 大大减少代码量
- 被广泛应用；高度优化
- 有开发调试工具支持




Core Data 基础
====

> 如果不使用Core Data你需要维护一个数据文件，从数据文件中加载的数据集等等，需要做很多繁琐的工作。

![Figure 1: Document Management using the standard Cocoa document architecture]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/document_management_2x.png)

使用Core Data你可以通过一个叫做`managed object context`或简称`context`来管理数据集：

> 在数据文件(`Persistent Object Store` 持久对象存储)和应用程序之间建立了一个间接层：`NSManagedObjectContext 托管对象上下文` + `Persistent Store Coordinator 持久存储协调器`

![Figure 2: Document management using Core Data]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/coredata_doc_management_2x.png)


托管对象和上下文 Managed Objects and Contexts
====

管理器将数据从持久存储中加载到内存任你操作，直有你明确要求保存才回写到持久存储中。
一个持久存储对象可以对应多个托管对象上下文。这有可能在保存时出现数据不一致的问题。Core Data提供了多种解决方案。

数据抓取请求 Fetch Requests
====
要想从托管对象上下文中获取数据，你需要创建`数据抓取请求`。

数据抓取请求三要素：

- 实体名称 Entity Name
- 查询条件 Predicate
- 多个结果排序方式 Sort Orderings

![Figure 3: An example fetch request]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/fetch_request_2x.png)

你向托管对象上下文发出一个数据抓取请求，它会返回多个或零个符合条件的对象。

持久存储协调器 Persistent Store Coordinator
====

前面提到过，Core Data提供的这组对象组成了一个持久栈，栈顶是`托管对象上下文`，栈低是`持久存储`。他们之间就是`持久存储协调器`。
`持久存储协调器`作为`托管对象上下文`的门面(façade)。将多个`持久存储`虚拟为单个存储。之后，`托管对象上下文`通过它创建一个`对象图`(objects graph)。

![Figure 4:Advanced persistence stack]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/advanced_persistence_stack_2x.png)

持久存储 Persistent Stores
====

Your application code should not make any assumptions about the persistent store in which data may reside

持久化文档 Persistent Documents
====

NSPersistentDocument继承自NSDocument。它建立一个自己的持久栈，包括一个托管对象和一个一对一的(one-to-one)持久对象存储。

托管对象和托管对象模型
====

为了可以管理`对象图`并提供对象持久化，Core Data要求使用托管对象模型来描述它要操作的对象。

![Figure 5: Managed object model with two entities]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/managed_object_model_2x.png)

对象的属性和对象之间的关系用响应的描述符描述

![Figure 6: Entity description with two attributes and a relationship]
(https://developer.apple.com/library/ios/documentation/cocoa/conceptual/CoreData/Art/entity_description_2x.png)




