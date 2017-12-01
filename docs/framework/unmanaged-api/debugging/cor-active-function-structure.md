---
title: Estrutura COR_ACTIVE_FUNCTION
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_ACTIVE_FUNCTION
api_location: mscordbi.dll
api_type: COM
f1_keywords: COR_ACTIVE_FUNCTION
helpviewer_keywords: COR_ACTIVE_FUNCTION structure [.NET Framework debugging]
ms.assetid: ed86185f-2152-459c-961f-10c06d62e83f
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 85096b607fa2fec9875e497cc1f50167fc482fbd
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="coractivefunction-structure"></a><span data-ttu-id="c4eaf-102">Estrutura COR_ACTIVE_FUNCTION</span><span class="sxs-lookup"><span data-stu-id="c4eaf-102">COR_ACTIVE_FUNCTION Structure</span></span>
<span data-ttu-id="c4eaf-103">Contém informações sobre as funções que estão atualmente ativas nos quadros de um thread.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-103">Contains information about the functions that are currently active in a thread's frames.</span></span> <span data-ttu-id="c4eaf-104">Essa estrutura é usada pelo [Icordebugthread2](../../../../docs/framework/unmanaged-api/debugging/icordebugthread2-getactivefunctions-method.md) método.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-104">This structure is used by the [ICorDebugThread2::GetActiveFunctions](../../../../docs/framework/unmanaged-api/debugging/icordebugthread2-getactivefunctions-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c4eaf-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="c4eaf-105">Syntax</span></span>  
  
```  
typedef struct  _COR_ACTIVE_FUNCTION {  
    ICorDebugAppDomain   *pAppDomain;  
    ICorDebugModule      *pModule;  
    ICorDebugFunction2   *pFunction;  
    ULONG32              ilOffset;  
    ULONG32              flags;  
} COR_ACTIVE_FUNCTION;  
```  
  
## <a name="members"></a><span data-ttu-id="c4eaf-106">Membros</span><span class="sxs-lookup"><span data-stu-id="c4eaf-106">Members</span></span>  
  
|<span data-ttu-id="c4eaf-107">Membro</span><span class="sxs-lookup"><span data-stu-id="c4eaf-107">Member</span></span>|<span data-ttu-id="c4eaf-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="c4eaf-108">Description</span></span>|  
|------------|-----------------|  
|`pAppDomain`|<span data-ttu-id="c4eaf-109">Ponteiro para o proprietário do domínio de aplicativo do `ilOffset` campo.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-109">Pointer to the application domain owner of the `ilOffset` field.</span></span>|  
|`pModule`|<span data-ttu-id="c4eaf-110">Ponteiro para o proprietário do módulo do `ilOffset` campo.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-110">Pointer to the module owner of the `ilOffset` field.</span></span>|  
|`pFunction`|<span data-ttu-id="c4eaf-111">Ponteiro para o proprietário da função do `ilOffset` campo.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-111">Pointer to the function owner of the `ilOffset` field.</span></span>|  
|`ilOffset`|<span data-ttu-id="c4eaf-112">O deslocamento de linguagem intermediária (MSIL) da Microsoft do quadro.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-112">The Microsoft intermediate language (MSIL) offset of the frame.</span></span>|  
|`flags`|<span data-ttu-id="c4eaf-113">Reservado para extensibilidade futura.</span><span class="sxs-lookup"><span data-stu-id="c4eaf-113">Reserved for future extensibility.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c4eaf-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="c4eaf-114">Requirements</span></span>  
 <span data-ttu-id="c4eaf-115">**Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c4eaf-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c4eaf-116">**Cabeçalho:** CorDebug.idl</span><span class="sxs-lookup"><span data-stu-id="c4eaf-116">**Header:** CorDebug.idl</span></span>  
  
 <span data-ttu-id="c4eaf-117">**Biblioteca:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c4eaf-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c4eaf-118">**Versões do .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c4eaf-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c4eaf-119">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c4eaf-119">See Also</span></span>  
 [<span data-ttu-id="c4eaf-120">Estruturas de depuração</span><span class="sxs-lookup"><span data-stu-id="c4eaf-120">Debugging Structures</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)  
 [<span data-ttu-id="c4eaf-121">Depuração</span><span class="sxs-lookup"><span data-stu-id="c4eaf-121">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)