---
title: Исключения размещения
ms.date: 03/30/2017
ms.assetid: ad9e14f8-fa17-4d59-b365-fe0e7ec17c98
ms.openlocfilehash: f2bc7d0ca09faa2598990437295d1abf0cff3c45
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61934736"
---
# <a name="hosting-exceptions"></a>Исключения размещения
В этом разделе перечислены все исключения, создаваемые Hosting.  
  
## <a name="exception-list"></a>Список исключений  
  
|Код ресурса|Строка ресурса|  
|-------------------|---------------------|  
|Hosting_AddressIsAbsoluteUri|Полный универсальный код ресурса (URI) не допускается. Интерфейс API ServiceHostingEnvironment.EnsureServiceAvailable не допускает использования полных URI. Используйте виртуальный путь для соответствующей службы.|  
|Hosting_BuildProviderCouldNotCreateType|Не удалось загрузить указанный тип CLR во время компиляции службы. Убедитесь, что этот тип определяется либо в исходный файл, расположенный в приложения \\каталоге \App_Code, содержащихся в скомпилированной сборке, расположенной в приложения \\\bin каталог, или присутствует в сборке, установленной в Глобальный кэш сборок. Имя типа вводится с учетом регистра. Каталоги, такие как \\\App_Code и \\\bin должен быть расположен в корневом каталоге приложения. \\\App_Code и \\\bin каталоги не могут быть вложенными в подкаталогах.|
