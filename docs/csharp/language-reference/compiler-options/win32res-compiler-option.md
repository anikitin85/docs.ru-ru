---
title: -win32res (параметры компилятора C#)
ms.date: 07/20/2015
f1_keywords:
- /win32res
helpviewer_keywords:
- win32res compiler option
- /win32res compiler option [C#]
- -win32res compiler option [C#]
- win32res compiler option [C#]
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
ms.openlocfilehash: 3bb1614fcf28c62a9000c9b96af2f046f329fb1e
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794381"
---
# <a name="-win32res-c-compiler-options"></a>-win32res (параметры компилятора C#)
Параметр **-win32res** вставляет ресурс Win32 в выходной файл.  
  
## <a name="syntax"></a>Синтаксис  
  
```console  
-win32res:filename  
```  
  
## <a name="arguments"></a>Аргументы  
 `filename`  
 Файл ресурсов, который требуется добавить в выходной файл.  
  
## <a name="remarks"></a>Remarks  
 Файл ресурсов Win32 можно создать с помощью [компилятора ресурсов](resource-compiler-option.md). Компилятор ресурсов вызывается при компиляции программы Visual C++; RES-файл создается из RC-файла.  
  
 Ресурс Win32 может содержать сведения о версии или точечный рисунок (значок) для упрощения идентификации приложения в проводнике. Если параметр **-win32res** не задан, компилятор будет создавать сведения о версии на основе версии сборки.  
  
 Дополнительные сведения о ссылках на файлы ресурсов .NET Framework и их присоединении см. в разделах [-linkresource](./linkresource-compiler-option.md) и [-resource](./resource-compiler-option.md) соответственно.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Установка данного параметра компилятора в среде разработки Visual Studio  
  
1. Откройте страницу **Свойства** проекта.  
  
2. Перейдите на страницу свойств **Приложение**.  
  
3. Чтобы выбрать файл в поле со списком, нажмите кнопку **Файл ресурсов**.  
  
## <a name="example"></a>Пример  
 Скомпилируйте `in.cs` и присоедините файл ресурсов Win32 `rf.res`, чтобы создать `in.exe`:  
  
```console  
csc -win32res:rf.res in.cs  
```  
  
## <a name="see-also"></a>См. также раздел

- [Параметры компилятора C# ](./index.md)
- [Управление свойствами проектов и решений](/visualstudio/ide/managing-project-and-solution-properties)
