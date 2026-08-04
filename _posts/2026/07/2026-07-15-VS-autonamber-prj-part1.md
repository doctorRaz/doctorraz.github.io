---
title: Visual Studio авто нумерация сборок. Часть 1.
description: Себе для памяти, возможно дополню и поправлю
author: doctorraz
date: 2026-07-15 10:00:00 +0300
categories:
  - NET
  - C#
  - VS
tags:
  - NET
  - VisualStudio
  - csproj
pin: false
hidden: false
---

[начало тут](https://autolisp.ru/2026/07/13/net-avtoversioning-loaded-assemblies/)

> Для "сопутствующих" сборок
>> *например собрал ты в конце года сборку
пересобрал после нового года, не поменял мажор минор.... лисп посчитает, что она старая???*

предлагаю так....

как ты всегда учил надо минимизировать дублирование кода (относится и 
к свойствам проектов), для этого в нашем случае отлично подходит 
*Directory.Build.props*

кидаем его в корень каталога решения и прописываем в нем общие параметры для всех сборок

```xml
<Project>
	<!-- <Import Project="d:\@Developers\Programmers\!NET\Shared\Directory.Build\Directory.Build.props"/> -->
	<PropertyGroup>
		<!-- ***************** общие свойства всех решений ***************** -->
		<!-- root решения относительно этого файла -->
		<!--<RepoRoot>$(MSBuildThisFileDirectory)</RepoRoot>-->
		<!-- root решения относительно каталога решения, более верно -->
		<!--************* только при сборке из решения ******************-->
		<RepoRoot>$(SolutionDir)</RepoRoot>
		
		<!-- позволяет проекты размещать в одном каталоге -->
		<!-- выходной каталог obj в каталоге решения -->
		<BaseIntermediateOutputPath>$(RepoRoot)obj\$(MSBuildProjectName)\</BaseIntermediateOutputPath>
		<LangVersion>latest</LangVersion>
		
		<!--<DateTime -->
		<StartYear>2014</StartYear>
		<CurrentYear>$([System.DateTime]::Now.Year)</CurrentYear>
		
		<!--<Version />-->
		<!-- <GenerateAssemblyInformationalVersionAttribute>false</GenerateAssemblyInformationalVersionAttribute> -->
		<!--<Version />-->
		
		<!-- путь к сборке -->
		<AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
		<BaseOutputPath>..\bin\</BaseOutputPath>
		<OutputPath>$(SolutionDir)bin\$(Configuration)</OutputPath>
		
		<!-- *******************Description *************-->
		<!-- ***************** Постоянные свойства ***************** -->
		
		<!-- CompanyName -->
		<Company>doctorRaz@gmail.com</Company>
		
		<!-- LegalCopyright -->
		<Copyright>Разыграев Андрей</Copyright>
		
		<!-- LegalTrademarks -->
		<Trademark>©doctorRaz $(StartYear)-$(CurrentYear)</Trademark>
		<!-- ***************** Переопределяются в проекте ***************** -->
		<!-- ProductName -->
		<Product>$(SolutionName)</Product>
		<!-- FileDescription он жэж Title-->
		<!-- если все закоментить то в титул пойдет имя сборки -->
		<!-- <AssemblyTitle>PlotSPDS</AssemblyTitle> -->
		<!-- Comments -->
		<!-- ProductVersion он жэж AssemblyInformationalVersion-->
		<InformationalVersion>$(SolutionName) for nanoCAD</InformationalVersion>
		<IncludeSourceRevisionInInformationalVersion>false</IncludeSourceRevisionInInformationalVersion>
		<NeutralLanguage>ru-RU</NeutralLanguage>
		<!-- ***************** ХЗ где используется ***************** -->
		<!-- <PackageProjectUrl>http://doctorraz.blogspot.com/2022/10/PlotSPDS.NET.html</PackageProjectUrl> -->
		<!-- <ProductVersion>ProductVersion</ProductVersion> -->
		<!-- <AssemblyProductVersion>AssemblyProductVersion</AssemblyProductVersion> -->
		<!-- <AssemblyInformationalVersionAttribute>AssemblyInformationalVersionAttribute</AssemblyInformationalVersionAttribute> -->
		<!-- ***************** индивидуальные свойства решения *****************-->
		<!-- с WPF аккуратно, теряет ресурсы если root другой, -->
		<RootNamespace>drz.SpecSPDS</RootNamespace>
		<Deterministic>false</Deterministic>
		<GenerateAssemblyInfo>true</GenerateAssemblyInfo>
		<AssemblyVersion>0.1.*</AssemblyVersion>		<GenerateAssemblyFileVersionAttribute>false</GenerateAssemblyFileVersionAttribute>
		<Description>Спецификация из универсального маркера, CAD + Multicad</Description>
		<RepositoryUrl>https://github.com/doctorRaz/SpecSPDS</RepositoryUrl>
		<MinVersion>23</MinVersion>
	</PropertyGroup>
</Project>
```

эти строчки отвечают за номер сборки

```xml
		<Deterministic>false</Deterministic>
		<GenerateAssemblyInfo>true</GenerateAssemblyInfo>
		<AssemblyVersion>0.1.*</AssemblyVersion>
		<GenerateAssemblyFileVersionAttribute>false</GenerateAssemblyFileVersionAttribute>
```
будет вида 0.1.9692.15284, для всех сборок проекта

если для какой то группы сборок нужен другой мажор минор, в каталоге этих сборок создаем *Directory.Build.props* и пишем там нужные цифры
если нужны индивидуальные свойства, то прописываем их в проекте сборки, они переопределят заданные в корневом Directory.Build.props

---

по поводу сборок *NET Framework*
я перевел их почти все на стиль SDK, типа так

```xml
<Project Sdk="Microsoft.NET.Sdk">
	<Import Project="$(SolutionDir)Directory.Build.props" Condition="Exists('$(SolutionDir)Directory.Build.props')" />
	<PropertyGroup>
		<TargetFramework>net462</TargetFramework>
		<RootNamespace>drz.Abstractions</RootNamespace>
		<AssemblyName>$(SolutionName).$(MSBuildProjectName)</AssemblyName>
		<InformationalVersion>$(MSBuildProjectName) for All</InformationalVersion>
		<ImplicitUsings>disable</ImplicitUsings>
		<Description>абстракции, интерфейсы</Description>
	</PropertyGroup>
	<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
		<GenerateDocumentationFile>True</GenerateDocumentationFile>
	</PropertyGroup>
</Project>
```

учитывая, что у тебя есть *Directory.Build.props* если хочешь другой номер версии, то просто добавь

```xml
<AssemblyVersion>10.21.*</AssemblyVersion>
```

---

по поводу текстового файла с номером версии для обновлятора

в корень решения кидаем Directory.Build.targets

там прописываем такие строчки

```xml
	<Target Name="WriteUpdateInfoINI" AfterTargets="Build">

		<GetAssemblyIdentity AssemblyFiles="$(TargetPath)">
			<Output TaskParameter="Assemblies" ItemName="AssemblyInfo"/>
		</GetAssemblyIdentity>

		<WriteLinesToFile
			File="$(TargetDir)update.ini"
			Overwrite="false"
			Lines="
[$(MSBuildProjectName)]
Name=$(AssemblyName)
Version=%(AssemblyInfo.Version)
"/>
		<!--json-->
	</Target>
	<Target Name="WriteUpdateInfoJson" AfterTargets="Build">

		<GetAssemblyIdentity AssemblyFiles="$(TargetPath)">
			<Output TaskParameter="Assemblies" ItemName="AssemblyInfo"/>
		</GetAssemblyIdentity>
		<PropertyGroup>
			<Major>$([System.Version]::Parse('%(AssemblyInfo.Version)').Major)</Major>
			<Minor>$([System.Version]::Parse('%(AssemblyInfo.Version)').Minor)</Minor>
			<Build>$([System.Version]::Parse('%(AssemblyInfo.Version)').Build)</Build>
			<Revision>$([System.Version]::Parse('%(AssemblyInfo.Version)').Revision)</Revision>
		</PropertyGroup>
		<WriteLinesToFile
			File="$(TargetDir)update.json"
			Overwrite="false"
			Lines='{"Project":"$(AssemblyName)","Major":$(Major),"Minor":$(Minor),"Build":$(Build),"Revision":$(Revision)}' />
	</Target>
```

формат любой, данные любые, тут только фантазией креатив ограничен

у меня все сборки идут в один каталог, поэтому по каждой идет дозапись в файл **update.\***.

единственное но... перед сборкой файл надо удалять руками или батником, как автоматизировать удаление перед общей сборкой мы с ботом пока не придумали