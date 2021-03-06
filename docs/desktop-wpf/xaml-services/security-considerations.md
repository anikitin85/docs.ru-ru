---
title: Соображения безопасности XAML
ms.date: 03/30/2017
helpviewer_keywords:
- security [XAML Services], .NET XAML services
- XAML security [XAML Services]
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
ms.openlocfilehash: 1864910b339c74e3033fb4d6d8baebffada1a4f8
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432920"
---
# <a name="xaml-security-considerations"></a>Соображения безопасности XAML

В этой статье описаны рекомендации по безопасности в приложениях при использовании API XAML и .NET XAML Services.

## <a name="untrusted-xaml-in-applications"></a>Недоверие XAML в приложениях

В самом общем смысле, ненадежный XAML является любым источником XAML, который ваше приложение специально не включало и не излучало.

XAML, который компилируется `resx`или хранится в качестве ресурса типа -типа в доверенной и подписанной сборке, по своей сути не является ненадежным. Вы можете доверять XAML столько, сколько вы доверяете сборки в целом. В большинстве случаев вас беспокоят только аспекты доверия свободного XAML, который является источником XAML, который вы загружаете из потока или другого ввоза или другого ввоза. Loose XAML не является специфическим компонентом или характеристикой модели приложения с инфраструктурой развертывания и упаковки. Тем не менее, сборка может реализовать поведение, которое включает в себя загрузку свободного XAML.

Для недоверчивого XAML, вы должны относиться к нему в целом так же, как если бы это был ненадежный код. Используйте песочницу или другие метафоры, чтобы предотвратить, возможно, ненадежный XAML от доступа к вашему доверенному коду.

Характер возможностей XAML дает XAML право строить объекты и устанавливать их свойства. Эти возможности также включают доступ к преобразователям типов, картографирование и `x:Code` доступ к сборкам в домене приложения, использование расширений разметки, блоков и так далее.

В дополнение к своим возможностям на языковом уровне, XAML используется для определения uI во многих технологиях. Загрузка ненадежного XAML может означать загрузку вредоносного пуль для спуфинга.

## <a name="sharing-context-between-readers-and-writers"></a>Обмен контекстом между читателями и писателями

Архитектура xAML Services .NET xAML для читателей XAML и авторов XAML часто требует обмена считывателя XAML для автора XAML или общего контекста схемы XAML. При написании логики цикла узлов XAML или предоставлении пользовательского пути сохранения может потребоваться совместное использование объектов или контекстов. Не делитесь экземплярами чтения XAML, нестандартным контекстом схемы XAML или настройками для классов чтения/записок XAML между доверенным и ненадежным кодом.

В большинстве сценариев и операций, связанных с записью объектов XAML для поддержки типа CLR, можно просто использовать контекст схемы XAML по умолчанию. Контекст схемы XAML по умолчанию явно не включает параметры, которые могут поставить под угрозу полное доверие. Таким образом, безопасно делиться контекстом между надежными и ненадежными компонентами XAML reader/writer. Однако, если вы сделаете это, это все еще лучшая <xref:System.AppDomain> практика, чтобы держать таких читателей и писателей в отдельных областях, с одним из них специально предназначены / sandboxed для частичного доверия.

## <a name="xaml-namespaces-and-assembly-trust"></a>XAML Namespaces и доверие сборки

Основной неквалифицированный синтаксис и определение того, как XAML интерпретирует пользовательское отображение пространства имен XAML в сборке, не проводит различия между доверенной и ненадежной сборкой, загруженной в домен приложения. Таким образом, технически возможно, чтобы ненадежная сборка подделать предназначенное отображение пространства имен XAML и захватить заявленную информацию об объекте и имуществе источника XAML. Если у вас есть требования к безопасности, чтобы избежать этой ситуации, предполагаемое отображение пространства имен XAML должно быть сделано с использованием одного из следующих методов:

- Используйте полностью квалифицированное название сборки с сильным именем в любом отображении пространства имен XAML, сделанном XAML вашего приложения.

- Ограничьте отображение сборки фиксированным набором референс-агрегатов, создав специфичную <xref:System.Xaml.XamlSchemaContext> для ваших читателей XAML и авторов объектов XAML. См. раздел <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>.

## <a name="xaml-type-mapping-and-type-system-access"></a>Картирование типа XAML и доступ к системе типа

XAML поддерживает свою собственную систему типов, которая во многом является одноранговой, как CLR реализует основную систему типа CLR. Однако для некоторых аспектов осведомленности о типе, когда вы принимаете доверительные решения о типе, основанном на его типе информации, следует отложить информацию типа в типах поддержки CLR. Это объясняется тем, что некоторые из конкретных возможностей отчетности системы типа XAML остаются открытыми как виртуальные методы и поэтому не полностью контролируются первоначальными реализациями .NET XAML Services. Эти точки расширяемости существуют потому, что система типа XAML является расширительной, чтобы соответствовать расширяемости самого XAML и его возможных альтернативных стратегий отображения типов по сравнению с реализацией, поддерживаемой CLR по умолчанию, и контекстом схемы XAML по умолчанию. Для получения дополнительной информации, см конкретные заметки о нескольких свойствах <xref:System.Xaml.XamlType> и <xref:System.Xaml.XamlMember>.

## <a name="see-also"></a>См. также

- <xref:System.Xaml.Permissions.XamlAccessLevel>
