---
title: Метод ICorDebugExceptionObjectCallStackEnum::Next
ms.date: 03/30/2017
api_name:
- ICorDebugExceptionObjectCallStackEnum::Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next
helpviewer_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugExceptionObjectCallStackEnum interface [.NET Framework debugging]
ms.assetid: 3328a2c0-1e48-4a54-802a-9b474cf82c21
topic_type:
- apiref
ms.openlocfilehash: 6fce9f61e222d0fc1763495de162a94a7fc22689
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2020
ms.locfileid: "82975983"
---
# <a name="icordebugexceptionobjectcallstackenumnext-method"></a>Метод ICorDebugExceptionObjectCallStackEnum::Next
Возвращает указанное число экземпляров [кордебужексцептионобжектстаккфраме](cordebugexceptionobjectstackframe-structure.md) , содержащих сведения из стека вызовов объекта исключения.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT Next(  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)] CorDebugExceptionObjectStackFrame values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `celt`  
 окне Число извлекаемых экземпляров [кордебужексцептионобжектстаккфраме](cordebugexceptionobjectstackframe-structure.md) .  
  
 `values`  
 заполняет Массив указателей, каждый из которых указывает на объект [кордебужексцептионобжектстаккфраме](cordebugexceptionobjectstackframe-structure.md) .  
  
 `pceltFetched`  
 заполняет Указатель на число фактически возвращенных экземпляров [кордебужексцептионобжектстаккфраме](cordebugexceptionobjectstackframe-structure.md) .  
  
## <a name="remarks"></a>Remarks  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также раздел

- [Интерфейс ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md)
- [Интерфейсы отладки](debugging-interfaces.md)
