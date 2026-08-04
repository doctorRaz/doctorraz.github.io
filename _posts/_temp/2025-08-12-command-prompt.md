---
title: Ком строка
description: Examples of text, typography, math equations, diagrams, flowcharts, pictures, videos, and more.
author: cotes
date: 2025-08-15 11:33:00 +0300
categories: [nanoCAD, hook]
tags: [nanoCAD]
pin: true
math: true
mermaid: true
image:
  path: /commons/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

для памяти походу у наны бага
флаги видимости и включения обрабатываются некоректно
```csharp
            promptOptions.Keywords.Add("acDisplay", "Экран", "Экран", true, true);
            promptOptions.Keywords.Add("acExtents", "Границы", "Границы", false, true);
            promptOptions.Keywords.Add("Acp", "Лист", "Лист", false, false);
            promptOptions.Keywords.Add("acLimits", "лИмиты", "лИмиты", true, false);
```
результат

![Image](https://github.com/user-attachments/assets/9bb15f5a-0025-4d31-b8ab-bbe453c8d267)

корректно скрылись только `Границы`
`Лист` должен быть скрыт, но нет
`лИмиты` `Enabled=false` не должны реагировать??? но реагируют и на мышку и на прямой ввод



[Как запустить nanoCAD](#funky)

[Релатив]({{ root_url | prepend: site.baseurl}}/posts/img/#funky)

