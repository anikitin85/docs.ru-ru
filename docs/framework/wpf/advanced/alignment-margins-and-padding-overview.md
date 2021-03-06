---
title: Общие сведения о свойствах Alignment, Margin, Padding
description: Сведения о HorizontalAlignment, Margin, Padding и VerticalAlignment, которые управляют положением дочернего элемента в Windows Presentation Foundation приложениях.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- margins [WPF]
- padding [WPF]
- aligning [WPF]
ms.assetid: 9c6a2009-9b86-4e40-8605-0a2664dc3973
ms.openlocfilehash: 832325086c85a7b044876e825d93e0b680a0b99c
ms.sourcegitcommit: 87cfeb69226fef01acb17c56c86f978f4f4a13db
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/24/2020
ms.locfileid: "87165893"
---
# <a name="alignment-margins-and-padding-overview"></a>Общие сведения о свойствах Alignment, Margin, Padding
<xref:System.Windows.FrameworkElement>Класс предоставляет несколько свойств, которые используются для точного позиционирования дочерних элементов. В этом разделе обсуждаются четыре наиболее важных свойства: <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> , <xref:System.Windows.FrameworkElement.Margin%2A> , <xref:System.Windows.Controls.Border.Padding%2A> и <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> . Очень важно иметь представление о результатах применения этих свойств, поскольку они обеспечивают основу для управления положением элементов в приложениях [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].  

<a name="wcpsdk_layout_amp_introduction"></a>
## <a name="introduction-to-element-positioning"></a>Введение в позиционирование элементов  
 Существуют разные способы позиционирования элементов с помощью [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Однако достижение идеального макета выходит за рамки простого выбора правильного <xref:System.Windows.Controls.Panel> элемента. Точное управление размещением требует понимания <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> <xref:System.Windows.FrameworkElement.Margin%2A> свойств,, <xref:System.Windows.Controls.Border.Padding%2A> и <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> .  
  
 На следующем рисунке показан сценарий макета, использующий несколько свойств размещения.  
  
 ![Пример использования свойств позиционирования WPF](./media/layout-margins-padding-alignment-graphic1.PNG "layout_margins_padding_alignment_graphic1")  
  
 На первый взгляд, <xref:System.Windows.Controls.Button> элементы на этом рисунке могут показаться случайными. На самом деле их положение точно контролируется с помощью сочетания полей, выравнивания и заполнения.  
  
 В следующем примере демонстрируется создание макета, показанного на предыдущем рисунке. <xref:System.Windows.Controls.Border>Элемент инкапсулирует родителя <xref:System.Windows.Controls.StackPanel> , <xref:System.Windows.Controls.Border.Padding%2A> значение которого равно 15 аппаратно-независимых пикселей. Эти учетные записи для узких <xref:System.Windows.Media.Brushes.LightBlue%2A> полос, охватывающих дочерний элемент <xref:System.Windows.Controls.StackPanel> . Дочерние элементы элемента <xref:System.Windows.Controls.StackPanel> используются для иллюстрации каждого из различных свойств позиционирования, подробно описанных в этом разделе. <xref:System.Windows.Controls.Button>Для демонстрации свойств и используются три элемента <xref:System.Windows.FrameworkElement.Margin%2A> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> .  
  
 [!code-csharp[MPALayoutSampleIntro#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutSampleIntro/CSharp/MPA_Layout_Sample_Intro.cs#1)]
 [!code-vb[MPALayoutSampleIntro#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutSampleIntro/VisualBasic/MPALayoutIntro.vb#1)]  
  
 Следующая схема обеспечивает подробное представление различных свойств размещения, примененных в предыдущем примере. В последующих разделах этой статьи более подробно описывается использование каждого свойства размещения.  
  
 ![Размещение свойств с помощью&#45;вызова экрана](./media/layout-margins-padding-alignment-graphic2.PNG "layout_margins_padding_alignment_graphic2")  
  
<a name="wcpsdk_layout_amp_alignment_properties"></a>
## <a name="understanding-alignment-properties"></a>Общие сведения о свойствах Alignment  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>Свойства и <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> описывают, как дочерний элемент должен располагаться в выделенном пространстве макета родительского элемента. При совместном использовании этих свойств можно точно расположить дочерние элементы. Например, дочерние элементы <xref:System.Windows.Controls.DockPanel> могут задавать четыре различных выравнивания по горизонтали: <xref:System.Windows.HorizontalAlignment.Left> , <xref:System.Windows.HorizontalAlignment.Right> , или <xref:System.Windows.HorizontalAlignment.Center> , чтобы <xref:System.Windows.HorizontalAlignment.Stretch> заполнить доступное пространство. Аналогичные значения доступны для вертикального размещения.  
  
> [!NOTE]
> Явно заданный параметр <xref:System.Windows.FrameworkElement.Height%2A> и <xref:System.Windows.FrameworkElement.Width%2A> свойства элемента имеют приоритет над <xref:System.Windows.HorizontalAlignment.Stretch> значением свойства. Попытка установить <xref:System.Windows.FrameworkElement.Height%2A> , <xref:System.Windows.FrameworkElement.Width%2A> и значение, если <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> `Stretch` `Stretch` запрос пропускается.  
  
<a name="wcpsdk_layout_amp_horizontalalignment_properties"></a>
### <a name="horizontalalignment-property"></a>Свойство HorizontalAlignment  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>Свойство объявляет характеристики выравнивания по горизонтали, которые применяются к дочерним элементам. В следующей таблице показаны все возможные значения <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> Свойства.  
  
|Член|Описание|  
|------------|-----------------|  
|<xref:System.Windows.HorizontalAlignment.Left>|Дочерние элементы выравниваются по левому краю выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.HorizontalAlignment.Center>|Дочерние элементы выравниваются по центру выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.HorizontalAlignment.Right>|Дочерние элементы выравниваются по правому краю выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.HorizontalAlignment.Stretch> (по умолчанию)|Дочерние элементы растягиваются для заполнения выделенного пространства макета родительского элемента. Явные <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement.Height%2A> значения и имеют приоритет.|  
  
 В следующем примере показано, как применить <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> свойство к <xref:System.Windows.Controls.Button> элементам. Показаны все значения атрибутов, чтобы проиллюстрировать различные режимы отрисовки.  
  
 [!code-csharp[MPALayoutHorizontalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/CSharp/MPA_Layout_HorizontalAlignment.cs#2)]
 [!code-vb[MPALayoutHorizontalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutHorizontalAlignment/VisualBasic/MPA_Layout_HorizontalAlignment.vb#2)]  
  
 Приведенный выше код создает макет, похожий на следующий рисунок. На <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> рисунке видны эффекты позиционирования каждого значения.  
  
 ![Пример HorizontalAlignment](./media/layout-horizontal-alignment-graphic.PNG "layout_horizontal_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_verticalalignment_properties"></a>
### <a name="verticalalignment-property"></a>Свойство VerticalAlignment  
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>Свойство описывает характеристики вертикального выравнивания, применяемые к дочерним элементам. В следующей таблице показаны все возможные значения <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> Свойства.  
  
|Член|Описание|  
|------------|-----------------|  
|<xref:System.Windows.VerticalAlignment.Top>|Дочерние элементы выравниваются по верхнему краю выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.VerticalAlignment.Center>|Дочерние элементы выравниваются по центру выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.VerticalAlignment.Bottom>|Дочерние элементы выравниваются по нижнему краю выделенного пространства макета родительского элемента.|  
|<xref:System.Windows.VerticalAlignment.Stretch> (по умолчанию)|Дочерние элементы растягиваются для заполнения выделенного пространства макета родительского элемента. Явные <xref:System.Windows.FrameworkElement.Width%2A> <xref:System.Windows.FrameworkElement.Height%2A> значения и имеют приоритет.|  
  
 В следующем примере показано, как применить <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> свойство к <xref:System.Windows.Controls.Button> элементам. Показаны все значения атрибутов, чтобы проиллюстрировать различные режимы отрисовки. Для целей этого примера <xref:System.Windows.Controls.Grid> элемент с видимыми линиями сетки используется в качестве родителя, чтобы лучше проиллюстрировать поведение макета для каждого значения свойства.  
  
 [!code-csharp[MPALayoutVerticalAlignment#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MPALayoutVerticalAlignment/CSharp/MPA_Layout_VerticalAlignment.cs#2)]
 [!code-vb[MPALayoutVerticalAlignment#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MPALayoutVerticalAlignment/VisualBasic/MPA_Layout_VerticalAlignment.vb#2)]
 [!code-xaml[MPALayoutVerticalAlignment#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MPALayoutVerticalAlignment/XAML/default.xaml#2)]  
  
 Приведенный выше код создает макет, похожий на следующий рисунок. На <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> рисунке видны эффекты позиционирования каждого значения.  
  
 ![Пример свойства VerticalAlignment](./media/layout-vertical-alignment-graphic.PNG "layout_vertical_alignment_graphic")  
  
<a name="wcpsdk_layout_amp_margin_properties"></a>
## <a name="understanding-margin-properties"></a>Основные сведения о свойствах Margin  
 <xref:System.Windows.FrameworkElement.Margin%2A>Свойство описывает расстояние между элементом и его дочерними или одноранговыми узлами. <xref:System.Windows.FrameworkElement.Margin%2A>значения могут быть однородными с помощью синтаксиса, такого как `Margin="20"` . Благодаря этому синтаксису <xref:System.Windows.FrameworkElement.Margin%2A> элементу будет применено универсальное из 20 аппаратно независимых пикселей. <xref:System.Windows.FrameworkElement.Margin%2A>значения могут также иметь форму из четырех различных значений, каждое из которых описывает отдельное поле для применения к левым, верхним, правым и нижним (в этом порядке), например `Margin="0,10,5,25"` . Правильное использование <xref:System.Windows.FrameworkElement.Margin%2A> свойства обеспечивает очень точное управление позицией отрисовки элемента и позицией отрисовки его соседних элементов и потомков.  
  
> [!NOTE]
> Ненулевое поле применяет пространство за пределами элемента <xref:System.Windows.FrameworkElement.ActualWidth%2A> и <xref:System.Windows.FrameworkElement.ActualHeight%2A> .  
  
 В следующем примере показано, как применять однородные поля вокруг группы <xref:System.Windows.Controls.Button> элементов. <xref:System.Windows.Controls.Button>Элементы размещаются равномерно с использованием буфера полей размером в десять пикселей в каждом направлении.  
  
 [!code-cpp[MarginPaddingAlignmentSample#1](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#1)]
 [!code-csharp[MarginPaddingAlignmentSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#1)]
 [!code-vb[MarginPaddingAlignmentSample#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#1)]
 [!code-xaml[MarginPaddingAlignmentSample#1](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#1)]  
  
 Во многих случаях универсальные поля не подходят. В этих случаях можно применять неоднородные интервалы. В следующем примере показано применение неоднородных полей к дочерним элементам. Поля описываются в следующем порядке: слева, сверху, справа, снизу.  
  
 [!code-cpp[MarginPaddingAlignmentSample#2](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#2)]
 [!code-csharp[MarginPaddingAlignmentSample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#2)]
 [!code-vb[MarginPaddingAlignmentSample#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#2)]
 [!code-xaml[MarginPaddingAlignmentSample#2](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#2)]  
  
<a name="wcpsdk_layout_amp_padding_properties"></a>
## <a name="understanding-the-padding-property"></a>Основные сведения о свойстве Padding  
 Заполнение аналогично <xref:System.Windows.FrameworkElement.Margin%2A> в большинстве случаев. Свойство Padding предоставляется только в нескольких классах, в основном как удобство: <xref:System.Windows.Documents.Block> ,, <xref:System.Windows.Controls.Border> <xref:System.Windows.Controls.Control> и <xref:System.Windows.Controls.TextBlock> — примеры классов, предоставляющих свойство заполнения. <xref:System.Windows.Controls.Border.Padding%2A>Свойство увеличивает эффективный размер дочернего элемента на указанное <xref:System.Windows.Thickness> значение.  
  
 В следующем примере показано, как применить <xref:System.Windows.Controls.Border.Padding%2A> к родительскому <xref:System.Windows.Controls.Border> элементу.  
  
 [!code-cpp[MarginPaddingAlignmentSample#3](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#3)]
 [!code-csharp[MarginPaddingAlignmentSample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#3)]
 [!code-vb[MarginPaddingAlignmentSample#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#3)]
 [!code-xaml[MarginPaddingAlignmentSample#3](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#3)]  
  
<a name="wcpsdk_layout_amp_summary"></a>
## <a name="using-alignment-margins-and-padding-in-an-application"></a>Использование свойств Alignment, Margin и Padding в приложении  
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>, <xref:System.Windows.FrameworkElement.Margin%2A> , <xref:System.Windows.Controls.Border.Padding%2A> и <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> предоставляют элемент управления положением, необходимый для создания сложного элемента [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] . Эффекты каждого свойства позволяют изменить размещение дочерних элементов, обеспечивая гибкость создания динамических приложений и интерфейсов пользователя.  
  
 В следующем примере демонстрируются понятия, описанные в этом разделе. Основываясь на инфраструктуре в первом примере этого раздела, в этом примере элемент добавляется <xref:System.Windows.Controls.Grid> в качестве дочернего элемента <xref:System.Windows.Controls.Border> в первом примере. <xref:System.Windows.Controls.Border.Padding%2A>применяется к родительскому <xref:System.Windows.Controls.Border> элементу. <xref:System.Windows.Controls.Grid>Используется для разделения пространства между тремя дочерними <xref:System.Windows.Controls.StackPanel> элементами. <xref:System.Windows.Controls.Button>элементы снова используются для отображения различных эффектов <xref:System.Windows.FrameworkElement.Margin%2A> и <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> . <xref:System.Windows.Controls.TextBlock>к каждому элементу добавляются элементы <xref:System.Windows.Controls.ColumnDefinition> для лучшего определения различных свойств, применяемых к <xref:System.Windows.Controls.Button> элементам в каждом столбце.  
  
 [!code-cpp[MarginPaddingAlignmentSample#4](~/samples/snippets/cpp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CPP/Margin_Padding_Alignment_Sample.cpp#4)]
 [!code-csharp[MarginPaddingAlignmentSample#4](~/samples/snippets/csharp/VS_Snippets_Wpf/MarginPaddingAlignmentSample/CSharp/Margin_Padding_Alignment_Sample.cs#4)]
 [!code-vb[MarginPaddingAlignmentSample#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarginPaddingAlignmentSample/VisualBasic/MarginPaddingAlignment.vb#4)]
 [!code-xaml[MarginPaddingAlignmentSample#4](~/samples/snippets/xaml/VS_Snippets_Wpf/MarginPaddingAlignmentSample/XAML/default.xaml#4)]  
  
 При компиляции приведенное выше приложение создает [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)], который показан на рисунке ниже. Влияние различных значений свойств очевидно в интервале между элементами, а значимые значения свойств для элементов в каждом столбце отображаются в <xref:System.Windows.Controls.TextBlock> элементах.  
  
 ![Несколько свойств размещения в одном приложении](./media/layout-margins-padding-aligment-graphic3.PNG "layout_margins_padding_aligment_graphic3")  
  
<a name="wcpsdk_layout_amp_alignment_whatsnext"></a>
## <a name="whats-next"></a>Дальнейшие действия  
 Свойства позиционирования, определенные <xref:System.Windows.FrameworkElement> классом, обеспечивают точное управление размещением элементов в [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] приложениях. Вы получаете в свое распоряжение несколько способов, позволяющих более эффективно размещать элементы с помощью [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].  
  
 Доступны дополнительные ресурсы, в которых макет [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] рассматривается более подробно. Раздел [Обзор панелей](../controls/panels-overview.md) содержит более подробные сведения о различных <xref:System.Windows.Controls.Panel> элементах. В разделе [Пошаговое руководство. мое первое классическое приложение WPF](../getting-started/walkthrough-my-first-wpf-desktop-application.md) содержит дополнительные методы, которые используют элементы макета для позиционирования компонентов и привязки их действий к источникам данных.  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.Windows.FrameworkElement>
- <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>
- <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>
- <xref:System.Windows.FrameworkElement.Margin%2A>
- [Общие сведения о панелях](../controls/panels-overview.md)
- [Макет](layout.md)
- [Пример коллекции макетов WPF](https://go.microsoft.com/fwlink/?LinkID=160054)
