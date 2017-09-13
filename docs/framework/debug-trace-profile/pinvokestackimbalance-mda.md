---
title: MDA pInvokeStackImbalance
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- signatures, platform invoke
- stack depth
- platform invoke stack imbalance
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- PInvokeStackImbalance MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: 34ddc6bd-1675-4f35-86aa-de1645d5c631
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c7dcab401da29798365f4cbb5477dd0fb154c830
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="pinvokestackimbalance-mda"></a><span data-ttu-id="f0204-102">MDA pInvokeStackImbalance</span><span class="sxs-lookup"><span data-stu-id="f0204-102">pInvokeStackImbalance MDA</span></span>
<span data-ttu-id="f0204-103">O MDA (Assistente de Depuração Gerenciado) de `pInvokeStackImbalance` é ativado quando o CLR detecta que a profundidade da pilha após uma chamada de invocação de plataforma não corresponde à profundidade da pilha esperada, dada a convenção de chamada especificada no atributo <xref:System.Runtime.InteropServices.DllImportAttribute>, bem como a declaração dos parâmetros na assinatura gerenciada.</span><span class="sxs-lookup"><span data-stu-id="f0204-103">The `pInvokeStackImbalance` managed debugging assistant (MDA) is activated when the CLR detects that the stack depth after a platform invoke call does not match the expected stack depth, given the calling convention specified in the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute as well as the declaration of the parameters in the managed signature.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f0204-104">O MDA `pInvokeStackImbalance` é implementado somente para plataformas x86 de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="f0204-104">The `pInvokeStackImbalance` MDA is implemented only for 32-bit x86 platforms.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f0204-105">No .NET Framework versão 3.5, o MDA `pInvokeStackImbalance` é desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="f0204-105">In the .NET Framework version 3.5, the `pInvokeStackImbalance` MDA is disabled by default.</span></span> <span data-ttu-id="f0204-106">Quando você usar a versão 3.5 do .NET Framework com Visual Studio 2005, o MDA de `pInvokeStackImbalance` aparecerá na lista **Assistentes de Depuração Gerenciados** na caixa de diálogo **Exceções** (que é exibida quando você clica em **Exceções** no menu **Depurar**).</span><span class="sxs-lookup"><span data-stu-id="f0204-106">When you use the .NET Framework version 3.5 with Visual Studio 2005, the `pInvokeStackImbalance` MDA will appear in the **Managed Debugging Assistants** list in the **Exceptions** dialog box (which is displayed when you click **Exceptions** on the **Debug** menu).</span></span> <span data-ttu-id="f0204-107">No entanto, marcar ou desmarcar a caixa de seleção **Geradas** para `pInvokeStackImbalance` não habilita nem desabilita o MDA, apenas controla se o Visual Studio gera ou não uma exceção quando o MDA é ativado.</span><span class="sxs-lookup"><span data-stu-id="f0204-107">However, selecting or clearing the **Thrown** check box for `pInvokeStackImbalance` does not enable or disable the MDA; it only controls whether Visual Studio throws an exception when the MDA is activated.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="f0204-108">Sintomas</span><span class="sxs-lookup"><span data-stu-id="f0204-108">Symptoms</span></span>  
 <span data-ttu-id="f0204-109">Um aplicativo encontra uma violação de acesso ou uma corrupção de memória ao fazer uma chamada de invocação de plataforma ou em seguida a ela.</span><span class="sxs-lookup"><span data-stu-id="f0204-109">An application encounters an access violation or memory corruption when making or following a platform invoke call.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="f0204-110">Causa</span><span class="sxs-lookup"><span data-stu-id="f0204-110">Cause</span></span>  
 <span data-ttu-id="f0204-111">A assinatura gerenciada da chamada de invocação de plataforma pode não corresponder à assinatura não gerenciada do método que está sendo chamado.</span><span class="sxs-lookup"><span data-stu-id="f0204-111">The managed signature of the platform invoke call might not match the unmanaged signature of the method being called.</span></span>  <span data-ttu-id="f0204-112">Essa incompatibilidade pode ser causada devido à assinatura gerenciada não declarar o número correto de parâmetros ou não especificar o tamanho apropriado para eles.</span><span class="sxs-lookup"><span data-stu-id="f0204-112">This mismatch can be caused by the managed signature not declaring the correct number of parameters or not specifying the appropriate size for the parameters.</span></span>  <span data-ttu-id="f0204-113">O MDA também pode ser ativado porque a convenção de chamada, possivelmente especificada pelo atributo <xref:System.Runtime.InteropServices.DllImportAttribute>, não corresponde à convenção de chamada não gerenciada.</span><span class="sxs-lookup"><span data-stu-id="f0204-113">The MDA can also activate because the calling convention, possibly specified by the <xref:System.Runtime.InteropServices.DllImportAttribute> attribute, does not match the unmanaged calling convention.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="f0204-114">Resolução</span><span class="sxs-lookup"><span data-stu-id="f0204-114">Resolution</span></span>  
 <span data-ttu-id="f0204-115">Examine a assinatura de invocação e convenção de chamada da plataforma gerenciada para confirmar que ela corresponde à assinatura e convenção de chamada do destino nativo.</span><span class="sxs-lookup"><span data-stu-id="f0204-115">Review the managed platform invoke signature and calling convention to confirm it matches the signature and calling convention of the native target.</span></span>  <span data-ttu-id="f0204-116">Tente especificar explicitamente a convenção de chamada tanto no lado gerenciado quanto no não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="f0204-116">Try explicitly specifying the calling convention on both the managed and unmanaged sides.</span></span> <span data-ttu-id="f0204-117">Também é possível, embora mais improvável, que a função não gerenciada tenha desequilibrado a pilha por algum outro motivo, assim como um bug no compilador não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="f0204-117">It is also possible, although not as likely, that the unmanaged function unbalanced the stack for some other reason, such as a bug in the unmanaged compiler.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="f0204-118">Efeito sobre o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="f0204-118">Effect on the Runtime</span></span>  
 <span data-ttu-id="f0204-119">Força todas as chamadas de invocação de plataforma a usar o caminho não otimizado no CLR.</span><span class="sxs-lookup"><span data-stu-id="f0204-119">Forces all platform invoke calls to take the nonoptimized path in the CLR.</span></span>  
  
## <a name="output"></a><span data-ttu-id="f0204-120">Saída</span><span class="sxs-lookup"><span data-stu-id="f0204-120">Output</span></span>  
 <span data-ttu-id="f0204-121">A mensagem MDA fornece o nome da chamada de método de invocação de plataforma que está causando o desequilíbrio na pilha.</span><span class="sxs-lookup"><span data-stu-id="f0204-121">The MDA message gives the name of the platform invoke method call that is causing the stack imbalance.</span></span>  <span data-ttu-id="f0204-122">Uma mensagem de exemplo de uma chamada de invocação de plataforma no método `SampleMethod` é:</span><span class="sxs-lookup"><span data-stu-id="f0204-122">A sample message of a platform invoke call on method `SampleMethod` is:</span></span>  
  
```  
A call to PInvoke function 'SampleMethod' has unbalanced the stack.   
This is likely because the managed PInvoke signature does not match   
the unmanaged target signature. Check that the calling convention and   
parameters of the PInvoke signature match the target unmanaged signature.  
```  
  
## <a name="configuration"></a><span data-ttu-id="f0204-123">Configuração</span><span class="sxs-lookup"><span data-stu-id="f0204-123">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <pInvokeStackImbalance />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="f0204-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f0204-124">See Also</span></span>  
 <span data-ttu-id="f0204-125"><xref:System.Runtime.InteropServices.MarshalAsAttribute></span><span class="sxs-lookup"><span data-stu-id="f0204-125"><xref:System.Runtime.InteropServices.MarshalAsAttribute></span></span>   
 <span data-ttu-id="f0204-126">[Diagnosticando erros com Assistentes de Depuração Gerenciados](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md) </span><span class="sxs-lookup"><span data-stu-id="f0204-126">[Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md) </span></span>  
 [<span data-ttu-id="f0204-127">Marshaling de interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="f0204-127">Interop Marshaling</span></span>](../../../docs/framework/interop/interop-marshaling.md)
