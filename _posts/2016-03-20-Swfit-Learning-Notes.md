---
layout: post
title:  Swift 学习笔记
comments: true
---

看了下别人的源码，发现有一个这样的写法我不大熟悉，原来是Swift中的[Access Control](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AccessControl.html)。

`
public final class Map {
  	public let mappingType: MappingType
  	
 -	var JSONDictionary: [String : AnyObject] = [:]
 +	public internal(set) var JSONDictionary: [String : AnyObject] = [:]
  	public var currentValue: AnyObject?
  	var currentKey: String?
  	var keyIsNested = false
 
@@ -157,4 +157,4 @@ private func valueFor(keyPathComponents: ArraySlice<String>, dictionary: [AnyObj
  	}
  	
  	return nil
 -}  
 +}
 `
 
 其中:
 `
 public internal(set) var JSONDictionary: [String : AnyObject] = [:]
 `
 
 书上是这样定义的：
> + **Public** access enables entities to be used within any source file from their defining module, and also in a source file from another module that imports the defining module. You typically use public access when specifying the public interface to a framework.

> + **Internal** access enables entities to be used within any source file from their defining module, but not in any source file outside of that module. You typically use internal access when defining an app’s or a framework’s internal structure.

> + **Private** access restricts the use of an entity to its own defining source file. Use private access to hide the implementation details of a specific piece of functionality.


*Getters and Setters*

>Getters and setters for constants, variables, properties, and subscripts automatically receive the same access level as the constant, variable, property, or subscript they belong to.

>You can give a setter a lower access level than its corresponding getter, to restrict the read-write scope of that variable, property, or subscript. You assign a lower access level by writing `private(set)` or `internal(set)` before the `var` or `subscript` introducer.


大概的意思就是如果要公开Getter方法给别人,可以这样定义API 
`
public internal(set) var someproperty
`
通过`internal(set)`把Setter的访问权限设置成`internal`级别，就可以保护Setter 不被公开出去。
