---
title: Ресурсы приложения, содержимое и файлы данных
description: Ознакомьтесь с специальной поддержкой по настройке, идентификации и использованию файлов данных приложения в Windows Presentation Foundation (WPF).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], files
- loose resources [WPF]
- content files [WPF]
- Site of Origin files [WPF]
- resource files [WPF]
- remote files [WPF]
- embedded resources [WPF]
- files [WPF]
- referencing application files [WPF]
- application development [WPF], files
- application management [WPF]
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
ms.openlocfilehash: 324b3eb922f0fd1d1d9ad00105a06a7fbdb8effd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622865"
---
# <a name="wpf-application-resource-content-and-data-files"></a>Ресурсы, Содержимое и Файлы данных WPF-приложения
Приложения Microsoft Windows часто зависят от файлов, содержащих неисполняемые данные, такие как [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] , изображения, видео и звук. Windows Presentation Foundation (WPF) предлагает специальную поддержку для настройки, идентификации и использования этих типов файлов данных, которые называются файлами данных приложения. Эта поддержка относится к определенному набору типов файлов данных приложения, включая следующие:  
  
- **Файлы ресурсов**. файлы данных, компилируемые в исполняемый файл или СБОРКУ библиотеки WPF.  
  
- **Файлы содержимого**: автономные файлы данных с явной связью с исполняемой сборкой WPF.  
  
- **Файлы исходного узла**: автономные файлы данных, не имеющие связи с исполняемой сборкой WPF.  
  
 Важным отличием между этими тремя типами файлов является то, что файлы ресурсов и файлы содержимого известны во время построения. Сборка содержит информацию о них. Однако для файлов исходного узла сборка может вообще не иметь сведений о них или неявного набора знаний через универсальный код ресурса (URI) типа pack. в последнем случае нет никакой гарантии, что файл исходного узла, на который указывает ссылка, фактически существует.  
  
 Для ссылки на файлы данных приложения Windows Presentation Foundation (WPF) использует схему универсального идентификатора ресурса (URI) типа Pack, которая подробно описана в разделе URI типа " [Pack" в WPF](pack-uris-in-wpf.md).  
  
 В этом разделе описывается настройка и использование файлов данных приложения.  

<a name="Resource_Files"></a>
## <a name="resource-files"></a>Файлы ресурсов  
 Если файл данных приложения всегда должен быть доступен для приложения, то единственный способ гарантировать доступность — скомпилировать его в главную исполняемую сборку приложения или в одну из его указанных ссылками сборок. Этот тип файла данных приложения называется *файлом ресурсов*.  
  
 Нужно использовать файлы ресурсов, если:  
  
- Не нужно обновлять содержимое файла ресурсов после его компиляции в сборку.  
  
- Необходимо упростить распространение приложения за счет уменьшения количества зависимостей между файлами.  
  
- Файл данных приложения должен быть локализуемой (см. [Общие сведения о глобализации и локализации WPF](../advanced/wpf-globalization-and-localization-overview.md)).  
  
> [!NOTE]
> Файлы ресурсов, описанные в этом разделе, отличаются от файлов ресурсов, описанных в [ресурсах XAML](../../../desktop-wpf/fundamentals/xaml-resources-define.md) , и отличаются от внедренных или связанных ресурсов, описанных в статье [Управление ресурсами приложения (.NET)](/visualstudio/ide/managing-application-resources-dotnet).  
  
### <a name="configuring-resource-files"></a>Настройка файлов ресурсов  
 В WPF файл ресурсов — это файл, включенный в проект Microsoft Build Engine (MSBuild) в качестве `Resource` элемента.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> В Visual Studio создайте файл ресурсов, добавив файл в проект и задав для него значение `Build Action` `Resource` .  
  
 При построении проекта MSBuild компилирует ресурс в сборку.  
  
### <a name="using-resource-files"></a>Использование файлов ресурсов  
 Чтобы загрузить файл ресурсов, можно вызвать <xref:System.Windows.Application.GetResourceStream%2A> метод <xref:System.Windows.Application> класса, передав URI типа Pack, который идентифицирует нужный файл ресурсов. <xref:System.Windows.Application.GetResourceStream%2A>Возвращает <xref:System.Windows.Resources.StreamResourceInfo> объект, который предоставляет файл ресурсов как <xref:System.IO.Stream> и описывает его тип содержимого.  
  
 Например, в следующем коде показано, как использовать <xref:System.Windows.Application.GetResourceStream%2A> для загрузки <xref:System.Windows.Controls.Page> файла ресурсов и его установки в качестве содержимого объекта <xref:System.Windows.Controls.Frame> ( `pageFrame` ):  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 Хотя при вызове <xref:System.Windows.Application.GetResourceStream%2A> предоставляется доступ к <xref:System.IO.Stream> , необходимо выполнить дополнительную работу по преобразованию в тип свойства, для которого будет задано значение. Вместо этого можно позволить WPF относиться к открытию и преобразованию, <xref:System.IO.Stream> загружая файл ресурсов непосредственно в свойство типа с помощью кода.  
  
 В следующем примере показано, как загрузить объект <xref:System.Windows.Controls.Page> непосредственно в <xref:System.Windows.Controls.Frame> ( `pageFrame` ) с помощью кода.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 В следующем примере показан эквивалент разметки предыдущего примера.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### <a name="application-code-files-as-resource-files"></a>Файлы кода приложения как файлы ресурсов  
 На Специальный набор файлов кода приложения WPF можно ссылаться с помощью URI типа "Pack", включая окна, страницы, документы нефиксированного формата и словари ресурсов. Например, можно задать <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType> свойство с URI типа Pack, который ссылается на окно или страницу, которые необходимо загрузить при запуске приложения.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 Это можно сделать, когда XAML-файл включается в проект MSBuild как `Page` элемент.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> В Visual Studio вы добавите в проект новый,,, <xref:System.Windows.Window> <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Controls.Page> <xref:System.Windows.Documents.FlowDocument> или <xref:System.Windows.ResourceDictionary> , `Build Action` для файла разметки по умолчанию будет выбрано значение `Page` .  
  
 При компиляции проекта с `Page` элементами [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] элементы преобразуются в двоичный формат и компилируются в связанную сборку. Следовательно, эти файлы можно использовать таким же образом, как и обычные файлы ресурсов.  
  
> [!NOTE]
> Если [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] файл настроен в качестве `Resource` элемента и не имеет файла кода программной части, то необработанный код [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] компилируется в сборку, а не в двоичную версию RAW [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] .  
  
<a name="Content_Files"></a>
## <a name="content-files"></a>Файлы с содержимым  
 *Файл содержимого* распространяется в виде свободного файла вместе с исполняемой сборкой. Несмотря на то, что они не компилируются в сборку, сборки компилируются с метаданными, которые устанавливают связь с каждым файлом содержимого.  
  
 Файлы содержимого необходимо использовать, если приложению требуется определенный набор файлов данных приложения, которые нужно обновлять без повторной компиляции использующей их сборки.  
  
### <a name="configuring-content-files"></a>Настройка файлов содержимого  
 Чтобы добавить файл содержимого в проект, в качестве элемента необходимо включить файл данных приложения `Content` . Более того, поскольку файл содержимого не компилируется непосредственно в сборку, необходимо задать `CopyToOutputDirectory` элемент метаданных MSBuild, чтобы указать, что файл содержимого копируется в расположение, относящееся к построенной сборке. Если требуется, чтобы ресурс копировался в выходную папку сборки при каждом построении проекта, необходимо задать для `CopyToOutputDirectory` элемента метаданных `Always` значение. В противном случае можно гарантировать, что только последняя версия ресурса копируется в выходную папку сборки с использованием `PreserveNewest` значения.  
  
 Ниже показан файл, настроенный как файл содержимого, который копируется в папку выходных данных построения только при добавлении новой версии ресурса в проект.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
> В Visual Studio вы создаете файл содержимого, добавляя файл в проект и присвоив ему значение `Build Action` , а также установите для него значение `Content` `Copy to Output Directory` `Copy always` (то же, что `Always` `Copy if newer` `PreserveNewest` и).  
  
 При построении проекта <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> атрибут компилируется в метаданные сборки для каждого файла содержимого.  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 Значение параметра <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> указывает путь к файлу содержимого относительно его положения в проекте. Например, если файл содержимого находился во вложенной папке проекта, то в это значение будет включен дополнительный путь к данным <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> .  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>Значение является также значением пути к файлу содержимого в выходной папке построения.  
  
### <a name="using-content-files"></a>Использование файлов содержимого  
 Чтобы загрузить файл содержимого, можно вызвать <xref:System.Windows.Application.GetContentStream%2A> метод <xref:System.Windows.Application> класса, передав URI типа Pack, который идентифицирует нужный файл содержимого. <xref:System.Windows.Application.GetContentStream%2A>Возвращает <xref:System.Windows.Resources.StreamResourceInfo> объект, который предоставляет файл содержимого в виде <xref:System.IO.Stream> и описывает его тип содержимого.  
  
 Например, в следующем коде показано, как использовать <xref:System.Windows.Application.GetContentStream%2A> для загрузки <xref:System.Windows.Controls.Page> файла содержимого и его установки в качестве содержимого объекта <xref:System.Windows.Controls.Frame> ( `pageFrame` ).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 Хотя при вызове <xref:System.Windows.Application.GetContentStream%2A> предоставляется доступ к <xref:System.IO.Stream> , необходимо выполнить дополнительную работу по преобразованию в тип свойства, для которого будет задано значение. Вместо этого можно позволить WPF относиться к открытию и преобразованию, <xref:System.IO.Stream> загружая файл ресурсов непосредственно в свойство типа с помощью кода.  
  
 В следующем примере показано, как загрузить объект <xref:System.Windows.Controls.Page> непосредственно в <xref:System.Windows.Controls.Frame> ( `pageFrame` ) с помощью кода.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 В следующем примере показан эквивалент разметки предыдущего примера.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>
## <a name="site-of-origin-files"></a>Файлы исходного узла  
 Файлы ресурсов имеют явную связь со сборками, которые они распределяют вместе, как определено в <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> . Но иногда необходимо установить неявную либо несуществующую связь между сборкой и файлом данных приложения, например, в следующих случаях:  
  
- Файл не существует во время компиляции.  
  
- Неизвестно, какие файлы потребуются для сборки до времени выполнения.  
  
- Нужна возможность обновлять файлы без повторной компиляции сборки, связанной с ними.  
  
- Приложение использует большие файлы данных, такие как аудио и видео, и необходимо, чтобы пользователи могли их загружать только при необходимости.  
  
 Эти типы файлов можно загрузить с помощью традиционных схем URI, таких как `file:///` `http://` схемы и.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 Однако `file:///` `http://` для схем и требуется, чтобы приложение имело полное доверие. Если приложение является приложением браузера XAML (XBAP), которое было запущено из Интернета или интрасети, и запрашивает только набор разрешений, разрешенных для приложений, запускаемых из этих расположений, свободные файлы могут загружаться только из исходного узла приложения (расположение запуска). Такие файлы называются файлами *исходного узла* .  
  
 Файлы исходного узла являются единственным вариантом для приложений с частичным доверием, хотя и не ограничиваются такими приложениями. Приложениям с полным доверием, возможно, все равно придется загружать файлы данных приложений, о которых они не знают во время построения. Хотя приложения с полным доверием могут использовать схему file:///, вероятнее всего, файлы данных приложения будут установлены в одну папку или вложенную папку со сборкой приложения. В этом случае использовать ссылки на исходный узел проще, чем использовать file:///, так как последнее требует разработки полного пути к файлу.  
  
> [!NOTE]
> Файлы исходного узла не кэшируются с помощью приложения браузера XAML (XBAP) на клиентском компьютере, а файлы содержимого —. Следовательно, они загружаются только по специальному запросу. Если приложение браузера XAML (XBAP) имеет большие файлы мультимедиа, их настройка в качестве файлов исходного узла означает, что начальный запуск приложения выполняется гораздо быстрее, а файлы загружаются по требованию.  
  
### <a name="configuring-site-of-origin-files"></a>Настройка файлов исходного узла  
 Если файлы исходного сайта не существуют или неизвестны во время компиляции, необходимо использовать традиционные механизмы развертывания для обеспечения доступности необходимых файлов во время выполнения, в том числе с помощью `XCopy` программы командной строки или Microsoft установщик Windows.  
  
 Если во время компиляции вы узнаете, какие файлы необходимо найти на исходном узле, но все равно хотите избежать явной зависимости, можно добавить эти файлы в проект MSBuild как `None` элемент. Как и в случае с файлами содержимого, необходимо задать `CopyToOutputDirectory` атрибут MSBuild, чтобы указать, что файл исходного узла копируется в расположение относительно сборки, указав либо значение, либо `Always` `PreserveNewest` значение.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
> В Visual Studio создайте файл исходного узла, добавив файл в проект и задав для него значение `Build Action` `None` .  
  
 При построении проекта MSBuild копирует указанные файлы в выходную папку сборки.  
  
### <a name="using-site-of-origin-files"></a>Использование файлов исходного узла  
 Чтобы загрузить файл исходного узла, можно вызвать <xref:System.Windows.Application.GetRemoteStream%2A> метод <xref:System.Windows.Application> класса, передав URI типа Pack, который идентифицирует нужный файл исходного узла. <xref:System.Windows.Application.GetRemoteStream%2A>Возвращает <xref:System.Windows.Resources.StreamResourceInfo> объект, который предоставляет файл исходного узла как <xref:System.IO.Stream> и описывает его тип содержимого.  
  
 В следующем примере кода показано, как использовать <xref:System.Windows.Application.GetRemoteStream%2A> для загрузки <xref:System.Windows.Controls.Page> файла исходного узла и задать его в качестве содержимого объекта <xref:System.Windows.Controls.Frame> ( `pageFrame` ).  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 Хотя при вызове <xref:System.Windows.Application.GetRemoteStream%2A> предоставляется доступ к <xref:System.IO.Stream> , необходимо выполнить дополнительную работу по преобразованию в тип свойства, для которого будет задано значение. Вместо этого можно позволить WPF относиться к открытию и преобразованию, <xref:System.IO.Stream> загружая файл ресурсов непосредственно в свойство типа с помощью кода.  
  
 В следующем примере показано, как загрузить объект <xref:System.Windows.Controls.Page> непосредственно в <xref:System.Windows.Controls.Frame> ( `pageFrame` ) с помощью кода.  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 В следующем примере показан эквивалент разметки предыдущего примера.  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>
## <a name="rebuilding-after-changing-build-type"></a>Повторное построение после изменения типа построения  
 После изменения типа построения файла данных приложения необходимо перестроить все приложение, чтобы обеспечить применение этих изменений. Если просто выполнить построение приложения, изменения не применяются.  
  
## <a name="see-also"></a>См. также

- [URI типа "pack" в WPF](pack-uris-in-wpf.md)
