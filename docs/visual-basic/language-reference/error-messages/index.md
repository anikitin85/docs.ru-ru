---
title: сообщения об ошибках
ms.date: 07/20/2015
helpviewer_keywords:
- errors [Visual Basic]
- error messages
- trappable errors
- errors [Visual Basic], trappable
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
ms.openlocfilehash: c2d9974f41efdd321af800e6270586d9b18ba6f7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402853"
---
# <a name="error-messages-visual-basic"></a>Сообщения об ошибке (Visual Basic)
При записи, компиляции или выполнении приложения Visual Basic возможны ошибки следующих типов.  
  
1. Ошибки во время разработки, то есть при написании приложения в Visual Studio.  
  
2. Ошибки компиляции, возникающие при компиляции приложения в Visual Studio или из командной строки.  
  
3. Ошибки времени выполнения, возникающие при выполнении приложения в Visual Studio или в виде отдельного исполняемого файла.  
  
 Сведения о способах устранения некоторых ошибок можно найти в статье [Additional Resources for Visual Basic Programmers](../../getting-started/additional-resources.md) (Дополнительные ресурсы для программирования на Visual Basic).  
  
## <a name="run-time-errors"></a>Ошибки времени выполнения  
 Если Visual Basic приложение пытается выполнить действие, которое система не может выполнить, возникает ошибка времени выполнения, а Visual Basic создает `Exception` объект. Visual Basic могут формировать пользовательские ошибки любого типа данных, включая `Exception` объекты, с помощью `Throw` инструкции. Приложение может идентифицировать ошибки, отображая номер ошибки и сообщение перехваченного исключения. Если ошибка не будет перехвачена, приложение завершается.  
  
 Код может перехватывать и проверять ошибки времени выполнения. Если вы заключите код, создающий ошибку, в блок `Try`, вы сможете перехватить любую созданную ошибку в соответствующем блоке `Catch`. Сведения о том, как в коде отлавливать ошибки во время выполнения и реагировать на них, можно найти в статье [Try...Catch...Finally Statement](../statements/try-catch-finally-statement.md) (Оператор Try...Catch...Finally).  
  
## <a name="compile-time-errors"></a>Ошибки времени компиляции  
 Если компилятор Visual Basic обнаруживает проблему в коде, возникает ошибка времени компиляции. В редакторе кода можно легко определить, какая строка кода вызвала ошибку. Строка с ошибкой подчеркивается волнистой линий. Если навести курсор на подчеркнутый фрагмент, появляется сообщение об ошибке. Также его можно увидеть вместе с другими сообщениями в **списке ошибок**.  
  
 Если идентификатор подчеркивается волнистой линией, а под крайним правым символом есть короткое подчеркивание, это означает возможность создать заглушку для класса, конструктора, метода, свойства, поля или перечисления. Дополнительные сведения см. в статье [Generate From Usage](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage) (Создание из использования).
  
 Если вы будете правильно учитывать предупреждения компилятора Visual Basic, ваш код будет работать быстрее и с меньшим количеством ошибок. Эти предупреждения сообщают о том, что в коде могут возникнуть ошибки при запуске приложения. Например, компилятор предупреждает о вызове члена неопределенной объектной переменной, о возврате из функции без задания возвращаемого значения, а также о выполнении блока `Try` с ошибками в логике перехвата исключений. Дополнительные сведения о предупреждениях, в том числе о возможности включать и отключать их, см. в статье [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic) (Настройка предупреждений в Visual Basic).
