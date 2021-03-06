---
title: Руководство по программированию на C#. Индексаторы в интерфейсах
description: В C# можно объявлять индексаторы для интерфейса. Узнайте, чем методы доступа индексаторов интерфейса отличаются от методов доступа индексаторов класса.
ms.date: 02/08/2020
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: ec77843bdf3181a543bd6c02cfb034b21ded1ae7
ms.sourcegitcommit: 6f58a5f75ceeb936f8ee5b786e9adb81a9a3bee9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/28/2020
ms.locfileid: "87303105"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>Индексаторы в интерфейсах (Руководство по программированию в C#)

Индексаторы можно объявлять для [интерфейса](../../language-reference/keywords/interface.md). Методы доступа индексаторов интерфейса отличаются от методов доступа индексаторов [класса](../../language-reference/keywords/class.md) следующим образом:

- Методы доступа интерфейса не используют модификаторы.
- Метод доступа интерфейса обычно не имеет тела.

Методы доступа нужны, чтобы указать, доступен ли индексатор для чтения и записи, только для чтения или только для записи. Вы можете предоставить реализацию для индексатора, определенного в интерфейсе, но это случается редко. Индексаторы обычно определяют API для доступа к полям данных, а поля данных не могут быть определены в интерфейсе.

Ниже показан пример метода доступа индексатора для интерфейса:

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#DefineIndexer)]

Сигнатура индексатора должна отличаться от сигнатур любых других индексаторов, объявленных в том же интерфейсе.

## <a name="example"></a>Пример

Следующий пример демонстрирует реализацию индексаторов интерфейса.

[!code-csharp[Implement](~/samples/snippets/csharp/interfaces/indexers.cs#ImplementInterface)]

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#ExampleCode)]

В приведенном выше примере можно использовать явную реализацию члена интерфейса с помощью полного имени члена интерфейса. Пример

```csharp
string IIndexInterface.this[int index]
{
}
```

Тем не менее полное имя требуется только в целях устранения неоднозначности, если класс реализует более одного интерфейса с одинаковой сигнатурой индексатора. Например, если класс `Employee` реализует два интерфейса (`ICitizen` и `IEmployee`), оба из которых имеют одинаковую сигнатуру индексатора, требуется явная реализация члена интерфейса. Это значит, что потребуется следующее объявление индексатора:

```csharp
string IEmployee.this[int index]
{
}
```

реализует индексатор в интерфейсе `IEmployee`, тогда как следующее объявление:

```csharp
string ICitizen.this[int index]
{
}
```

реализует индексатор в интерфейсе `ICitizen`.

## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../index.md)
- [Индексаторы](./index.md)
- [Свойства](../classes-and-structs/properties.md)
- [Интерфейсы](../interfaces/index.md)
