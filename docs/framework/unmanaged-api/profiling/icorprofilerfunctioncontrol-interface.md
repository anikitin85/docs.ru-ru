---
title: Интерфейс ICorProfilerFunctionControl
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl
helpviewer_keywords:
- ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 4e3d3141-4662-4166-8f05-bc857c1b4216
topic_type:
- apiref
ms.openlocfilehash: 177127c8c53e4fee31f7007d04c49cc337cca458
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498730"
---
# <a name="icorprofilerfunctioncontrol-interface"></a>Интерфейс ICorProfilerFunctionControl
Предоставляет методы, позволяющие профилировщику кода взаимодействовать со средой выполнения CLR и контролировать порядок генерирования кода JIT-компилятором при повторной компиляции указанного метода.  
  
## <a name="methods"></a>Методы  
  
|Метод|Описание|  
|------------|-----------------|  
|[Метод SetCodegenFlags](icorprofilerfunctioncontrol-setcodegenflags-method.md)|Задает один или несколько флагов из перечисления [COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md) для управления созданием кода для перекомпилированной функции JIT.|  
|[Метод SetILFunctionBody](icorprofilerfunctioncontrol-setilfunctionbody-method.md)|Заменяет тело метода на языке CIL.|  
|[Метод SetILInstrumentedCodeMap](icorprofilerfunctioncontrol-setilinstrumentedcodemap-method.md)|Устанавливает карту кода для указанной функции с помощью указанных записей карты языка CIL.|  
  
## <a name="remarks"></a>Примечания  
 Интерфейс `ICorProfilerFunctionControl` предоставляет методы для генерации управляющего кода для одной перекомпилированной функции. Профилировщик получает экземпляр этого интерфейса через обратный вызов [ICorProfilerCallback4:: жетрежитпараметерс](icorprofilercallback4-getrejitparameters-method.md) . Каждый экземпляр `ICorProfilerFunctionControl` управляет всеми экземплярами одной функции.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerInfo4](icorprofilerinfo4-interface.md)
- [Профилирующие интерфейсы](profiling-interfaces.md)
- [Метод EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md)
