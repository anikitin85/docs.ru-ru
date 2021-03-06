---
title: Пространства имен и DTD в DOM
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 1e9b55c4-76ad-4f54-8d96-7ce4b4cf1e05
ms.openlocfilehash: 748be66c255aa018fb3e1ed541c6e5a92775408c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288788"
---
# <a name="namespaces-and-dtds-in-the-dom"></a>Пространства имен и DTD в DOM
Определения типа документа (DTD) усложняют поддержку пространства имен. Например, приведенный ниже XML-файл содержит атрибуты по умолчанию с двоеточиями в имени.  
  
```xml  
<!ATTLIST item x:id CDATA #IMPLIED>  
```  
  
 Ниже приведены возможные разрешения, если эта конструкция допустима:  
  
- `x:` рассматривается как префикс пространства имен, но этот префикс должен быть разрешаемым с использованием декларации пространства имен `xmlns:x`, которое также должно быть в DTD. Сопоставлять этот префикс с чем-то иным в экземпляре документа - ошибка.  
  
- `x:` рассматривается как префикс пространства имен, но этот префикс всегда разрешается в контексте элементов экземпляра. Это значит, что префикс может быть сопоставлен с другими URI пространства имен в зависимости от диапазона пространства имен, в котором находится элемент `item`. Это поведение более предсказуемо, чем разрешение, данное в предшествующем пункте, но имеет другие сложные последствия, поскольку требует материализованных атрибутов по умолчанию.  
  
- Двоеточие не обрабатывается, так как оно находится в DTD, имя атрибута - `x:y`, нет префикса и нет URI-кода пространства имен.  
  
- Двоеточие в атрибуте по умолчанию вызывает исключение, указывающее, что двоеточия в имена внутри DTD не поддерживаются. Это дает прогнозируемость поведения, но лишает возможности загружать многие из DTD, опубликованные консорциумом W3C.  
  
- Когда пользователь запрашивает проверку DTD, поддержка пространства имен для всего документа отключается. Это позволяет загружать DTD консорциума W3C и обеспечивает прогнозируемость работы.  
  
 Язык XML в платформе Microsoft .NET Framework реализует второй вариант, обеспечивая максимальную совместимость со стандартом W3C.  
  
## <a name="see-also"></a>См. также

- [Модель объектов документов XML (DOM)](xml-document-object-model-dom.md)
