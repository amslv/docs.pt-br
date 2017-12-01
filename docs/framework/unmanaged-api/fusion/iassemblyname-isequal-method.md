---
title: "Método IAssemblyName::IsEqual"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IAssemblyName.IsEqual
api_location: fusion.dll
api_type: COM
f1_keywords: IAssemblyName::IsEqual
helpviewer_keywords:
- IsEqual method [.NET Framework fusion]
- IAssemblyName::IsEqual method [.NET Framework fusion]
ms.assetid: 6dfc220f-d0d4-45b3-bfce-5829f817766f
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 51a4fbe005a8e270b9fe6767ae5173bd027a191b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="iassemblynameisequal-method"></a><span data-ttu-id="6fa53-102">Método IAssemblyName::IsEqual</span><span class="sxs-lookup"><span data-stu-id="6fa53-102">IAssemblyName::IsEqual Method</span></span>
<span data-ttu-id="6fa53-103">Determina se um especificado [IAssemblyName](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md) objeto é igual a este `IAssemblyName`, com base nos sinalizadores de comparação especificado.</span><span class="sxs-lookup"><span data-stu-id="6fa53-103">Determines whether a specified [IAssemblyName](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md) object is equal to this `IAssemblyName`, based on the specified comparison flags.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6fa53-104">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="6fa53-104">Syntax</span></span>  
  
```  
HRESULT IsEqual (  
    [in] IAssemblyName  *pName,  
    [in] DWORD          dwCmpFlags  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="6fa53-105">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6fa53-105">Parameters</span></span>  
 `pName`  
 <span data-ttu-id="6fa53-106">[in] O `IAssemblyName` objeto ao qual comparar isso `IAssemblyName`.</span><span class="sxs-lookup"><span data-stu-id="6fa53-106">[in] The `IAssemblyName` object to which to compare this `IAssemblyName`.</span></span>  
  
 `dwCmpFlags`  
 <span data-ttu-id="6fa53-107">[in] Uma combinação bit a bit de [ASM_CMP_FLAGS](../../../../docs/framework/unmanaged-api/fusion/asm-cmp-flags-enumeration.md) valores que influenciam a comparação.</span><span class="sxs-lookup"><span data-stu-id="6fa53-107">[in] A bitwise combination of [ASM_CMP_FLAGS](../../../../docs/framework/unmanaged-api/fusion/asm-cmp-flags-enumeration.md) values that influence the comparison.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6fa53-108">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6fa53-108">Requirements</span></span>  
 <span data-ttu-id="6fa53-109">**Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6fa53-109">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6fa53-110">**Cabeçalho:** Fusion.h</span><span class="sxs-lookup"><span data-stu-id="6fa53-110">**Header:** Fusion.h</span></span>  
  
 <span data-ttu-id="6fa53-111">**As versões do .NET Framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6fa53-111">**NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6fa53-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6fa53-112">See Also</span></span>  
 [<span data-ttu-id="6fa53-113">Interface IAssemblyName</span><span class="sxs-lookup"><span data-stu-id="6fa53-113">IAssemblyName Interface</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-interface.md)  
 [<span data-ttu-id="6fa53-114">Enumerações de fusão</span><span class="sxs-lookup"><span data-stu-id="6fa53-114">Fusion Enumerations</span></span>](../../../../docs/framework/unmanaged-api/fusion/fusion-enumerations.md)