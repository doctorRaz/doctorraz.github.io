---
title: Утечка using
description: Реализации "протекают" в библиотеки.
author: doctorraz
date: 2026-08-04T11:00:00
categories:
  - C#
  - NET
  - VS
tags:
  - NET
  - csproj
  - VisualStudio
pin: true
hidden: false
media_subpath: /assets/img/posts/2026-08-04-VS-Utechka-using
---

# Утечка using 

Не забыть добавить картинок

Иногда несмотря на то, что зависимая библиотека подключена только к абстракциям, в нее могут "протекать"  реализации из сборок которые напрямую не подключены (транзит)\
В принципе если работать только через интерфейсы большой проблемы нет, но иногда надо запретить такое поведение
## DisableTransitiveProjectReferences

Это свойство **отключает все транзитивные `ProjectReference`** для зависимого проекта, \
т.е. сборки подключенные только к интерфейсам, ничего кроме этих интерфейсов видеть не будут.\
 
```xml
<Project>
	<!-- .... -->
	<PropertyGroup> 
		<DisableTransitiveProjectReferences>true</DisableTransitiveProjectReferences>
	</PropertyGroup>
	<!-- .... -->
</Project>
```
## PrivateAssets
отключает в верхней сборке передачу реализаций "вниз"\
гарантированно сборки напрямую не подключенные к **Infrastructure.csproj** реализации внутри нее не увидят.
```xml
<Project>
	<!-- .... -->
	<ProjectReference Include="..\Infrastructure\Infrastructure.csproj">
	    <PrivateAssets>all</PrivateAssets>
	</ProjectReference>
	<!-- .... -->
</Project>
```

