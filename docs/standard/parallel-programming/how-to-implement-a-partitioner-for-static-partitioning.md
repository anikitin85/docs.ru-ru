---
title: Практическое руководство. Реализация разделителя для статического секционирования
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- tasks, how to create a static partitioner
ms.assetid: f4410508-cac6-4ba7-bef1-c5e68b2794f3
ms.openlocfilehash: 22d2cf788d4726488512703356a75f84efd04250
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/02/2020
ms.locfileid: "84278510"
---
# <a name="how-to-implement-a-partitioner-for-static-partitioning"></a>Практическое руководство. Реализация разделителя для статического секционирования
Следующий пример демонстрирует реализацию простого пользовательского разделителя для PLINQ, который выполняет статическое секционирование. Поскольку этот разделитель не поддерживает динамические секции, его нельзя использовать в <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType>. Эта конкретная реализация разделителя может работать быстрее, чем стандартный разделитель по диапазонам для таких источников данных, в которых требуется большое время на обработку каждого элемента.  
  
## <a name="example"></a>Пример  
 [!code-csharp[TPL_Partitioners#05](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_partitioners/cs/partitioners.cs#05)]  
  
 Секции в этом примере создаются, исходя из предположения о линейном увеличении времени обработки для каждого элемента. В реальных ситуациях обычно нельзя так просто спрогнозировать время обработки. Если вы используете статический разделитель для конкретного источника данных, попробуйте оптимизировать формулу разделения для этого источника, добавить логику балансировки нагрузки или использовать блочное секционирование. Примеры таких подходов представлены в статье [Практическое руководство. Реализация динамических секций](how-to-implement-dynamic-partitions.md).  
  
## <a name="see-also"></a>См. также раздел

- [Пользовательские разделители для PLINQ и TPL](custom-partitioners-for-plinq-and-tpl.md)
