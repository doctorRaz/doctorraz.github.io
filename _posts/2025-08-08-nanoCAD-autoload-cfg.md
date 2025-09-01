---
title: Как загрузить свое меню и ленту в nanoCAD
description: Несколько способов загрузки
author: doctorraz
date: 2025-08-08 11:10:00 +0300
categories: [CAD, nanoCAD]
tags: [nanocad, settings, levelup]
pin: false
hidden: false
media_subpath: '/assets/img/posts/2025-08-08-autoload-cfg'
---

 
### Способы загрузки
 
#### 1. Через настройки пользовательского интерфейса. 

Самый очевидный и простой способ загрузки меню в nanoCAD 

![НПИ](npi.png)
_Настройки пользовательского интерфейса_

> ![частичный](partial.png)
>
> В nanoCAD есть древняя бага,  при подключении частичного файла меню \
> nanoCAD скопирует файл \*.cfg в каталог `%AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ.х\config\` \
> а файл \*.cuix ленты нет, соответственно лента не будет подгружена. 
{: .prompt-danger }


#### 2. Ручная правка nanoCAD.cfg

Дописать в файл настроек _%AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ\config\nanoCAD.cfg_ путь к файлу конфигурации: 

```
#include "d:\@Developers\Programmers\!NET\!bundle\BlockFix.bundle\Resources\BlockFix.cfg"
```

####  3. Автозагрузка из \*.cfg  nanoCAD

![загрузка/выгрузка](load-unload.png)

![автозагрузка](autoload.png)

> nanoCAD не умеет напрямую из автозагрузки грузить файлы \*.cfg, поэтому нужен промежуточный файл .package (в кодировке UTF8). \
> в секции прописываем пути:
> - `ConfigEntry` к файлам меню (\*.cfg )
> - `ComponentEntry` к загружаемым приложениям:
> 
> ```xml
> <?xml version="1.0" encoding="utf-8" ?>
> <ApplicationPackage xmlns="hostApplicationPackage/v01"
>                     Name="drzTools">
> 	<Components>
> 		<ComponentEntry AppName="BlockFix"
> 		                ModuleName="/BlockFix.bundle/BlockFix.NCad.dll"
> 		                ModuleType="MGD"/>
> 
> 		<ConfigEntry FileName="/BlockFix.bundle/Resources/BlockFix.cfg"
> 		             FileType="CFG"/>
> 	</Components>
> </ApplicationPackage>
> ```
{: .prompt-info }

> Для загрузки способами 1-3 достаточно прав обычного пользователя, повышение прав не требуется.
{: .prompt-tip }

####  4. Через _nApp.cfg_ или _userdata.cfg_

Создать файл _nApp.cfg_ или _userdata.cfg_  (в кодировке UTF8 BOM) и прописать в него пути к файлам конфигураций: 

```
#include "d:\@Developers\Programmers\!NET\!bundle\BlockFix.bundle\Resources\BlockFix.cfg"
```

_nApp.cfg_ или _userdata.cfg_ можно скопировать в любой из каталогов:
- %ProgramFiles%\Nanosoft\nanoCAD x64 ХХ.х\
- %AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ.х\Config\
- %ProgramData%\Nanosoft\nanoCAD x64 ХХ.х\Config\

> Для записи и изменения в каталоге:
> - `%AppData%` повышение прав не требуется
> - `%ProgramData%\Nanosoft\nanoCAD x64 ХХ.х` у пользователя есть права только на запись, на изменение нет, это значит, что скопировать файл в этот каталог  пользователь сможет, но ни удалить не изменить без повышения прав нет. (хз отчего так сделано)
> - `%ProgramFiles%\Nanosoft\nanoCAD x64 ХХ.х` нужно повышение прав.
{: .prompt-info }

#### 5. Автозагрузка из реестра

 ![regedit](regedit.png)

В разделе _HKEY_LOCAL_MACHINE\SOFTWARE\Nanosoft\nanoCAD x64\ХХ.х_  :
- добавляем подраздел `Applications` 
- в этом подразделе еще один подраздел с названием нашего приложения `BlockFixNC` 
- в этом подразделе создаем строковый параметр имя `Package`, значение полный путь до нашего пакета `d:\@Developers\Programmers\!NET\!bundle\BlockFixNC.package`

в автозагрузке это будет выглядеть так:

![autolaod-regedit](autolaod-regedit.png)

> для записи в секцию _HKEY_LOCAL_MACHINE_ требуется повышение прав
{: .prompt-warning }

### Очередность загрузки

1. %ProgramFiles%\Nanosoft\nanoCAD x64 ХХ\nApp.cfg
2. %AppData%\Roaming\Nanosoft\nanoCAD x64 23.1\Config\nApp.cfg
3. %ProgramData%\Nanosoft\nanoCAD x64 ХХ\Config\nApp.cfg
4. %ProgramFiles%\Nanosoft\nanoCAD x64 ХХ\userdata.cfg
5. %AppData%\Roaming\Nanosoft\nanoCAD x64 23.1\Config\userdata.cfg
6. %ProgramData%\Nanosoft\nanoCAD x64 ХХ\Config\userdata.cfg 
7. %AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ\config\nanoCAD.cfg 
8. %AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ\config\cfg.cfg (штатная автозагрузка) 
9. HKEY_LOCAL_MACHINE\SOFTWARE\Nanosoft\nanoCAD x64\ХХ.х\Applications\ (из реестра)
 
> - nApp.cfg всегда загружаются перед userdata.cfg
> - Если файлы `nApp` или `userdata` скопированы в несколько каталогов, то загрузится только первый одноименный найденный файл, в порядке приведенном выше, остальные файлы грузиться не будут!
> - `nApp` и `userdata` загружаются независимо друг от друга
{: .prompt-info }

> все выше написанное про порядок загрузки \*.cfg относится и к файлам \*.ini \
> подробнее про загрузку приложений можно почитать у Алексея Кулика [Автозагрузка приложений nanoCAD и ее последовательность](https://autolisp.ru/2023/12/13/nanocad-addon-loading/)
{: .prompt-info }

### Особенности загрузки меню

При загрузке меню через:

#### 1. Файлы конфигурации

`nApp, userdata` или `nanoCAD.cfg` меню будет загружено во все профили (платформа, СПДС, Механика) и возможности отключить загрузку в профиле нет, но nanoCAD умеет загружать меню по условию, т.е. если в конфиге загрузки прописать:

```ini
#include condition="ComponentEnabled_nMechComp" "d:\@Developers\В работе\!Текущее\Programmers\!NET\!bundle\PlotSPDS.bundle\Resources\Mech_menu.cfg"
#include condition="ComponentEnabled_nSPDSComp" "d:\@Developers\В работе\!Текущее\Programmers\!NET\!bundle\PlotSPDS.bundle\Resources\SPDS_menu.cfg"
```

то первое меню будет загружаться только в профиль Механика, второе в профиль СПДС.\
допустимы ключевые слова, `or` `not` возможно какие то еще...:

```ini
#include condition="ComponentEnabled_MODELER3D or ComponentEnabled_MODELER3D_C3D" "nmenu3D.cfg"
#include condition="not ComponentEnabled_RasterTools"                             "RasterTools.cfg"
```

#### 2. Реестр

`HKEY_LOCAL_MACHINE\SOFTWARE\Nanosoft\nanoCAD x64\ХХ.х\Applications\`

Меню будет загружаться во все профили, но в автозагрузке (из под профиля) меню можно отключить

![autolaod-regedit](autolaod-regedit.png)

#### 3. Штатная автозагрузка 

(%AppData%\Roaming\Nanosoft\nanoCAD x64 ХХ\config\cfg.cfg) загрузит меню только в свой профиль

> Пути к файлам меню (\*.cfg) могут быть как абсолютными, так и относительными. Относительный путь отсчитывается от файла в котором прописан путь к конфигурации.
> Регистр символов не важен.
{: .prompt-tip }
 
