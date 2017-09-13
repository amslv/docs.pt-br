---
title: MDA invalidCERCall
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
- invalid CER calls
- InvalidCERCall MDA
- MDAs (managed debugging assistants), CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: c4577410-602e-44e5-9dab-fea7c55bcdfe
caps.latest.revision: 14
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8fda91296ffb27a7661f8e9c5ea4bc664e570ce8
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="invalidcercall-mda"></a><span data-ttu-id="082a4-102">MDA invalidCERCall</span><span class="sxs-lookup"><span data-stu-id="082a4-102">invalidCERCall MDA</span></span>
<span data-ttu-id="082a4-103">O MDA (Assistente de Depuração Gerenciado) de `invalidCERCall` é ativado quando há uma chamada de dentro do gráfico de CER (região de execução restrita) a um método que não tem nenhum contrato de confiabilidade um tem um contrato excessivamente fraco.</span><span class="sxs-lookup"><span data-stu-id="082a4-103">The `invalidCERCall` managed debugging assistant (MDA) is activated when there is a call within the constrained execution region (CER) graph to a method that has no reliability contract or an excessively weak contract.</span></span> <span data-ttu-id="082a4-104">Um contrato fraco é um contrato que declara que o pior caso de corrupção de estado tem escopo maior do que a instância passou para a chamada, ou seja, o <xref:System.AppDomain> ou o estado do processo pode se corromper ou o resultado dele não é sempre computável de forma determinística quando chamado dentro de uma CER.</span><span class="sxs-lookup"><span data-stu-id="082a4-104">A weak contract is a contract that declares that the worst case state corruption is of greater scope than the instance passed to the call, that is, the <xref:System.AppDomain> or process state may become corrupted or that its result is not always deterministically computable when called within a CER.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="082a4-105">Sintomas</span><span class="sxs-lookup"><span data-stu-id="082a4-105">Symptoms</span></span>  
 <span data-ttu-id="082a4-106">Resultados inesperados ao executar código em uma CER.</span><span class="sxs-lookup"><span data-stu-id="082a4-106">Unexpected results when executing code in a CER.</span></span> <span data-ttu-id="082a4-107">Os sintomas não são específicos.</span><span class="sxs-lookup"><span data-stu-id="082a4-107">The symptoms are not specific.</span></span> <span data-ttu-id="082a4-108">Eles poderiam ser uma <xref:System.OutOfMemoryException> inesperada, uma <xref:System.Threading.ThreadAbortException> ou outras exceções na chamada para o método não confiável, porque o tempo de execução não o preparou com antecedência nem o protegeu de exceções <xref:System.Threading.ThreadAbortException> em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="082a4-108">They could be an unexpected <xref:System.OutOfMemoryException>, a <xref:System.Threading.ThreadAbortException>, or other exceptions at the call into the unreliable method because the runtime did not prepare it ahead of time or protect it from <xref:System.Threading.ThreadAbortException> exceptions at run time.</span></span> <span data-ttu-id="082a4-109">Uma ameaça maior é que qualquer exceção resultante do método em tempo de execução pode deixar o <xref:System.AppDomain> ou o processo em um estado instável, o que contraria o objetivo de uma CER.</span><span class="sxs-lookup"><span data-stu-id="082a4-109">A greater threat is that any exception resulting from the method at run time could leave the <xref:System.AppDomain> or process in an unstable state, which is contrary to the objective of a CER.</span></span> <span data-ttu-id="082a4-110">O motivo pelo qual uma CER é criada é para evitar corrupções de estado como essa.</span><span class="sxs-lookup"><span data-stu-id="082a4-110">The reason a CER is created is to avoid state corruptions such as this.</span></span> <span data-ttu-id="082a4-111">Os sintomas de estado corrompido são específicos do aplicativo porque a definição de estado consistente é diferente entre aplicativos.</span><span class="sxs-lookup"><span data-stu-id="082a4-111">The symptoms of corrupt state are application specific because the definition of consistent state is different between applications.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="082a4-112">Causa</span><span class="sxs-lookup"><span data-stu-id="082a4-112">Cause</span></span>  
 <span data-ttu-id="082a4-113">O código dentro de uma CER está chamando uma função sem nenhum <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> ou com um <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> fraco que não é compatível com a execução em uma CER.</span><span class="sxs-lookup"><span data-stu-id="082a4-113">Code within a CER is calling a function with no <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> or with a weak <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> that is not compatible with running in a CER.</span></span>  
  
 <span data-ttu-id="082a4-114">Em termos de sintaxe de contrato de confiabilidade, um contrato fraco é um contrato que não especifica um valor de enumeração <xref:System.Runtime.ConstrainedExecution.Consistency> ou especifica um valor de <xref:System.Runtime.ConstrainedExecution.Consistency> de <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>, <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain> ou <xref:System.Runtime.ConstrainedExecution.Cer.None>.</span><span class="sxs-lookup"><span data-stu-id="082a4-114">In terms of reliability contract syntax, a weak contract is a contract that does not specify a <xref:System.Runtime.ConstrainedExecution.Consistency> enumeration value or specifies a <xref:System.Runtime.ConstrainedExecution.Consistency> value of <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>, <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain>, or <xref:System.Runtime.ConstrainedExecution.Cer.None>.</span></span> <span data-ttu-id="082a4-115">Qualquer uma das condições a seguir indica que o código de chamada pode impedir os esforços de outro código na CER para manter o estado consistente.</span><span class="sxs-lookup"><span data-stu-id="082a4-115">Any of these conditions indicates that the code called may impede the efforts of the other code in the CER to maintain consistent state.</span></span>  <span data-ttu-id="082a4-116">CERs permitem que o código trate erros de maneira muito determinística, mantendo invariáveis internas que são importantes para o aplicativo e permitindo que ele continue em execução ao enfrentar erros transitórios, como exceções de memória insuficiente.</span><span class="sxs-lookup"><span data-stu-id="082a4-116">CERs allow code to treat errors in a very deterministic manner, maintaining internal invariants that are important to the application and allowing it to continue running in the face of transient errors such as out-of-memory exceptions.</span></span>  
  
 <span data-ttu-id="082a4-117">A ativação desse MDA indica uma possibilidade de que o método ser chamado na CER pode falhar de forma que o chamador não esperava ou que deixa o <xref:System.AppDomain> ou o estado do processo irrecuperável ou corrompido.</span><span class="sxs-lookup"><span data-stu-id="082a4-117">The activation of this MDA indicates a possibility the method being called in the CER can fail in a way that the caller did not expect or that leaves the <xref:System.AppDomain> or process state corrupted or unrecoverable.</span></span> <span data-ttu-id="082a4-118">Naturalmente, o código chamado pode ser executado corretamente e o problema é simplesmente um contrato ausente.</span><span class="sxs-lookup"><span data-stu-id="082a4-118">Of course, the called code might execute correctly and the problem is simply a missing contract.</span></span> <span data-ttu-id="082a4-119">No entanto, os problemas envolvidos ao escrever código confiável são sutis e a ausência de um contrato é um bom indicador de que o código pode não ser executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="082a4-119">However, the issues involved in writing reliable code are subtle and the absence of a contract is a good indicator the code might not execute correctly.</span></span> <span data-ttu-id="082a4-120">Os contratos são indicadores de que o programador codificou de modo confiável e também são promessas de que essas garantias não serão alteradas em revisões futuras do código.</span><span class="sxs-lookup"><span data-stu-id="082a4-120">The contracts are indicators that the programmer has coded reliably and also promises that these guarantees will not change in future revisions of the code.</span></span>  <span data-ttu-id="082a4-121">Ou seja, os contratos são declarações de intenção e não apenas detalhes de implementação.</span><span class="sxs-lookup"><span data-stu-id="082a4-121">That is, the contracts are declarations of intent and not just implementation details.</span></span>  
  
 <span data-ttu-id="082a4-122">Já que qualquer método com um contrato fraco ou inexistente pode vir a falhar de muitas maneiras imprevisíveis, o tempo de execução não tenta remover do método nenhuma das suas próprias falhas imprevisíveis que são introduzidas por compilação JIT lenta, população do dicionário genérico ou anulações de thread, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="082a4-122">Because any method with a weak or nonexistent contract can potentially fail in many unpredictable ways, the runtime does not attempt to remove any of its own unpredictable failures from the method  that are introduced by lazy JIT-compiling, generics dictionary population, or thread aborts, for example.</span></span> <span data-ttu-id="082a4-123">Ou seja, quando esse MDA é ativado, ele indica que o tempo de execução não incluiu o método chamado na CER sendo definida; o grafo de chamadas foi encerrado neste nó porque continuar a preparar essa subárvore ajudaria a mascarar o erro em potencial.</span><span class="sxs-lookup"><span data-stu-id="082a4-123">That is, when this MDA is activated, it indicates that the runtime did not include the called method in the CER being defined; the call graph was terminated at this node because continuing to prepare this subtree would help mask the potential error.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="082a4-124">Resolução</span><span class="sxs-lookup"><span data-stu-id="082a4-124">Resolution</span></span>  
 <span data-ttu-id="082a4-125">Adicionar um contrato de confiabilidade válido para a função ou evitar o uso dessa chamada de função.</span><span class="sxs-lookup"><span data-stu-id="082a4-125">Add a valid reliability contract to the function or avoid using that function call.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="082a4-126">Efeito sobre o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="082a4-126">Effect on the Runtime</span></span>  
 <span data-ttu-id="082a4-127">O efeito de chamar um contrato fraco de uma CER pode ser a falha da CER em concluir suas operações.</span><span class="sxs-lookup"><span data-stu-id="082a4-127">The effect of calling a weak contract from a CER could be the CER failure to complete its operations.</span></span> <span data-ttu-id="082a4-128">Isso pode levar à corrupção do estado do processo <xref:System.AppDomain>.</span><span class="sxs-lookup"><span data-stu-id="082a4-128">This could lead to corruption of the <xref:System.AppDomain> process state.</span></span>  
  
## <a name="output"></a><span data-ttu-id="082a4-129">Saída</span><span class="sxs-lookup"><span data-stu-id="082a4-129">Output</span></span>  
 <span data-ttu-id="082a4-130">A seguir, a saída de exemplo deste MDA.</span><span class="sxs-lookup"><span data-stu-id="082a4-130">The following is sample output from this MDA.</span></span>  
  
 `Method 'MethodWithCer', while executing within a constrained execution region, makes a call at IL offset 0x000C to 'MethodWithWeakContract', which does not have a sufficiently strong reliability contract and might cause non-deterministic results.`  
  
## <a name="configuration"></a><span data-ttu-id="082a4-131">Configuração</span><span class="sxs-lookup"><span data-stu-id="082a4-131">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a><span data-ttu-id="082a4-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="082a4-132">See Also</span></span>  
 <span data-ttu-id="082a4-133"><xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A></span><span class="sxs-lookup"><span data-stu-id="082a4-133"><xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A></span></span>   
 <span data-ttu-id="082a4-134"><xref:System.Runtime.ConstrainedExecution></span><span class="sxs-lookup"><span data-stu-id="082a4-134"><xref:System.Runtime.ConstrainedExecution></span></span>   
 [<span data-ttu-id="082a4-135">Diagnosticando erros com Assistentes de Depuração Gerenciados</span><span class="sxs-lookup"><span data-stu-id="082a4-135">Diagnosing Errors with Managed Debugging Assistants</span></span>](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
