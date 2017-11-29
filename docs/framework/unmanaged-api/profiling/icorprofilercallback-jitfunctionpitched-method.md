---
title: "Método ICorProfilerCallback::JITFunctionPitched"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerCallback.JITFunctionPitched
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerCallback::JITFunctionPitched
helpviewer_keywords:
- JITFunctionPitched method [.NET Framework profiling]
- ICorProfilerCallback::JITFunctionPitched method [.NET Framework profiling]
ms.assetid: 116085df-7a77-404a-afac-d0557a12b986
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: a5b14bc5735c83897e818ca2038455e0c6510e27
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilercallbackjitfunctionpitched-method"></a><span data-ttu-id="d0afa-102">Método ICorProfilerCallback::JITFunctionPitched</span><span class="sxs-lookup"><span data-stu-id="d0afa-102">ICorProfilerCallback::JITFunctionPitched Method</span></span>
<span data-ttu-id="d0afa-103">Notifica o criador de perfil que uma função que tenha sido just-in-time (JIT)-compilado foi removido da memória.</span><span class="sxs-lookup"><span data-stu-id="d0afa-103">Notifies the profiler that a function that has been just-in-time (JIT)-compiled has been removed from memory.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="d0afa-104">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="d0afa-104">Syntax</span></span>  
  
```  
HRESULT JITFunctionPitched(  
    [in] FunctionID functionId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="d0afa-105">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d0afa-105">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="d0afa-106">[in] A ID da função que foi removida.</span><span class="sxs-lookup"><span data-stu-id="d0afa-106">[in] The ID of the function that was removed.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="d0afa-107">Comentários</span><span class="sxs-lookup"><span data-stu-id="d0afa-107">Remarks</span></span>  
 <span data-ttu-id="d0afa-108">Se a função removida é chamada, o criador de perfil receberá novos eventos de compilação JIT quando a função é recompilada.</span><span class="sxs-lookup"><span data-stu-id="d0afa-108">If the removed function is called, the profiler will receive new JIT-compilation events when the function is recompiled.</span></span> <span data-ttu-id="d0afa-109">Atualmente, o compilador JIT common language runtime (CLR) não remove funções de memória, para que esse retorno de chamada não está sendo usado e não será recebido pelo criador de perfil.</span><span class="sxs-lookup"><span data-stu-id="d0afa-109">Currently, the common language runtime (CLR) JIT compiler does not remove functions from memory, so this callback is currently not used and will not be received by the profiler.</span></span>  
  
 <span data-ttu-id="d0afa-110">O valor de `functionId` não é válido até que a função é recompilada.</span><span class="sxs-lookup"><span data-stu-id="d0afa-110">The value of `functionId` is not valid until the function is recompiled.</span></span> <span data-ttu-id="d0afa-111">Quando a função é recompilada, o mesmo `functionId` valor será usado.</span><span class="sxs-lookup"><span data-stu-id="d0afa-111">When the function is recompiled, the same `functionId` value will be used.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="d0afa-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="d0afa-112">Requirements</span></span>  
 <span data-ttu-id="d0afa-113">**Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="d0afa-113">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="d0afa-114">**Cabeçalho:** Corprof. idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="d0afa-114">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="d0afa-115">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="d0afa-115">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="d0afa-116">**Versões do .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="d0afa-116">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d0afa-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="d0afa-117">See Also</span></span>  
 [<span data-ttu-id="d0afa-118">Interface ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="d0afa-118">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)