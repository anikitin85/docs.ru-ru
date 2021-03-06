---
title: Коллекции и типы коллекций для XAML
ms.date: 03/30/2017
ms.assetid: 58f8e7c6-9a41-4f25-8551-c042f1315baa
ms.openlocfilehash: 2ec58026c605df31489c8aab4c4cc714dab11474
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2020
ms.locfileid: "81432584"
---
# <a name="collections-and-collection-types-for-xaml"></a>Коллекции и типы коллекций для XAML

В этой статье описывается, как определить свойства типов, предназначенных для поддержки коллекции, и поддержать синтаксис XAML для мгновенного сбора элементов как элемента элемента элемента родительского объекта или элемента свойства.

## <a name="xaml-collection-concepts"></a>Концепции коллекции XAML

Концептуально любая связь в XAML, где есть несколько элементов ребенка в рамках элемента объекта XAML или элемента свойства XAML, должна быть реализована в виде коллекции. Эта коллекция должна быть связана с определенным свойством XAML типа XAML, которое является родителем в этих отношениях. Свойство должно быть коллекцией, поскольку процессор XAML предполагает назначить каждый элемент в наценке, чтобы быть недавно добавленным элементом свойства резервной коллекции.

На языковом уровне XAML точные требования поддержки коллекции не определены в полной мере. Понятие, что коллекция может быть либо списком, либо словарем (но не обоими) определяется на уровне языка XAML, но какие типы поддержки представляют списки или словари, не определяемые языком XAML.

В .NET XAML Services концепция поддержки коллекции XAML более четко определена с точки зрения типов поддержки .NET. В частности, поддержка Коллекций XAML основана на нескольких концепциях .NET и AI, которые используются для списков и словарей в целом .

1. Интерфейс <xref:System.Collections.IList> указывает на сбор списков.

2. Интерфейс <xref:System.Collections.IDictionary> указывает на набор словарей.

3. <xref:System.Array>представляет массив, и массив <xref:System.Collections.IList> поддерживает методы.

В каждой из этих концепций коллекции процессор .NET XAML `Add` Services XAML предполагает вызвать метод на определенный экземпляр типа свойства коллекции. Или, в сценарии сериализации, процессор XAML производит дискретные экземпляры типа XAML для каждого элемента, найденного в списке, словаре или массиве, основываясь на конкретной концепции каждой коллекции "Items". Эти элементы: ; <xref:System.Collections.IList.Item%2A?displayProperty=nameWithType> <xref:System.Collections.IDictionary.Item%2A?displayProperty=nameWithType>; явное <xref:System.Array.System%23Collections%23IList%23Item%2A?displayProperty=nameWithType> <xref:System.Array>для .

## <a name="generic-collections"></a>Общие коллекции

Общие коллекции могут быть полезны для общего программирования .NET, а также могут быть использованы для свойств коллекции XAML. Тем не менее, <xref:System.Collections.Generic.IList%601> <xref:System.Collections.Generic.IDictionary%602> общие интерфейсы и не определены процессорами .NET XAML Services <xref:System.Collections.IList> <xref:System.Collections.IDictionary>XAML как эквивалентные негенерическим или . Вместо того, чтобы реализовывать интерфейсы, рекомендуемый подход для <xref:System.Collections.Generic.List%601> <xref:System.Collections.Generic.Dictionary%602>общих типов свойств сбора должен вытекать из классов или . Эти классы реализуют необщие интерфейсы и, таким образом, включают ожидаемую поддержку коллекций XAML в базовую реализацию.

## <a name="read-only-collections-and-initialization-logic"></a>Только для чтения коллекции и логика инициализации

В программировании .NET существует общий шаблон проектирования, который делает любое свойство, которое имеет ценность коллекции в виде коллекции только для чтения. Эта модель позволяет экземпляру, владеющему свойством коллекции, лучше контролировать, что происходит с коллекцией. В частности, шаблон предотвращает случайную замену всей уже существующей коллекции путем установки свойства. В этом шаблоне любой доступ к коллекции абонентов должен быть сделан путем вызова методов или свойств, <xref:System.Collections.IList>поддерживаемых типом коллекции и/или соответствующими интерфейсами коллекции, такими как .

Использование этого шаблона подразумевает, что любой класс, который предоставляет свойство собрания только для чтения, должен сначала инициализировать это свойство для хранения пустой коллекции. Обычно инициализация выполняется как часть поведения конструкции для класса. Чтобы быть полезным для XAML, важно, чтобы такая логика всегда ссылалась на беспараметрыный конструктор, потому что XAML обычно вызывает беспараметрыный конструктор перед обработкой свойств (свойства сбора или иным образом).

## <a name="xaml-type-system-support-and-collections"></a>Поддержка и коллекции систем типа XAML

Помимо базовой механики разбора XAML и заполнения или сериализации свойств сбора, система типа XAML, реализованная в .NET XAML Services, включает в себя несколько конструктивных особенностей, относящихся к коллекциям xAML.

1. <xref:System.Xaml.XamlType.IsCollection%2A>возвращается верно, если тип XAML поддерживается типом, который обеспечивает поддержку коллекции XAML.

2. <xref:System.Xaml.XamlType.IsDictionary%2A>и <xref:System.Xaml.XamlType.IsArray%2A> может дополнительно определить, какой режим сбора поддерживает тип XAML. Для пользовательских процессоров XAML, основанных на службах .NET XAML services <xref:System.Xaml.XamlWriter> и системе типа XAML, но не основанных на существующих реализациях, возможно, потребуется знать, какой метод следует использовать для обработки сбора.

3. Каждое из предыдущих значений свойств потенциально <xref:System.Xaml.XamlType.LookupCollectionKind%2A> зависит от переопределения на типе XAML.
