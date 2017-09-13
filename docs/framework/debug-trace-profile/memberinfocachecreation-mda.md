---
title: MDA memberInfoCacheCreation
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
- member info cache creation
- MemberInfoCacheCreation MDA
- reflection, run-time errors
- MDAs (managed debugging assistants), cache
- cache [.NET Framework], reflection
- managed debugging assistants (MDAs), cache
- MemberInfo cache
ms.assetid: 5abdad23-1335-4744-8acb-934002c0b6fe
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 991055f537bfcbb2a533384ffc787c070a0122d4
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="memberinfocachecreation-mda"></a><span data-ttu-id="b3ecc-102">MDA memberInfoCacheCreation</span><span class="sxs-lookup"><span data-stu-id="b3ecc-102">memberInfoCacheCreation MDA</span></span>
<span data-ttu-id="b3ecc-103">O MDA (Assistente de Depuração Gerenciado) de `memberInfoCacheCreation` é ativado quando um cache de <xref:System.Reflection.MemberInfo> é criado.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-103">The `memberInfoCacheCreation` managed debugging assistant (MDA) is activated when a <xref:System.Reflection.MemberInfo> cache is created.</span></span> <span data-ttu-id="b3ecc-104">Isso é uma indicação forte de um programa que está fazendo uso de recursos de reflexão com consumo elevado de recursos computacionais.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-104">This is a strong indication of a program that is making use of resource-expensive reflection features.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="b3ecc-105">Sintomas</span><span class="sxs-lookup"><span data-stu-id="b3ecc-105">Symptoms</span></span>  
 <span data-ttu-id="b3ecc-106">O conjunto de trabalho de um programa aumenta porque o programa está usando reflexão com consumo elevado de recursos.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-106">A program's working set increases because the program is using resource-expensive reflection.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="b3ecc-107">Causa</span><span class="sxs-lookup"><span data-stu-id="b3ecc-107">Cause</span></span>  
 <span data-ttu-id="b3ecc-108">Operações de reflexão que envolvem objetos <xref:System.Reflection.MemberInfo> são consideradas grandes consumidoras de recursos porque elas devem ler os metadados que são armazenados em páginas frias e, em geral, eles indicam que o programa está usando algum tipo de cenário de associação tardia.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-108">Reflection operations that involve <xref:System.Reflection.MemberInfo> objects are considered resource expensive because they must read metadata that is stored in cold pages and in general they indicate the program is using some type of late-bound scenario.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="b3ecc-109">Resolução</span><span class="sxs-lookup"><span data-stu-id="b3ecc-109">Resolution</span></span>  
 <span data-ttu-id="b3ecc-110">Você pode determinar o local em que a reflexão está sendo usada em seu programa habilitando esse MDA e, em seguida, executando o código em um depurador ou anexando com um depurador quando o MDA é ativado.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-110">You can determine where reflection is being used in your program by enabling this MDA and then running your code in a debugger or attaching with a debugger when the MDA is activated.</span></span> <span data-ttu-id="b3ecc-111">Em um depurador, você obterá um rastreamento de pilha mostrando o local em que o cache <xref:System.Reflection.MemberInfo> foi criado e, desse ponto em diante, você poderá determinar o local em que o programa está usando reflexão.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-111">Under a debugger you will get a stack trace showing where the <xref:System.Reflection.MemberInfo> cache was created and from there you can determine where your program is using reflection.</span></span>  
  
 <span data-ttu-id="b3ecc-112">A resolução depende dos objetivos do código.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-112">The resolution is dependent on the objectives of the code.</span></span> <span data-ttu-id="b3ecc-113">Esse MDA alerta você de que o programa tem um cenário de associação tardia.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-113">This MDA alerts you that your program has a late-bound scenario.</span></span> <span data-ttu-id="b3ecc-114">Você talvez queira determinar se você pode substituir um cenário de associação precoce ou considerar o desempenho do cenário de associação tardia.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-114">You might want to determine if you can substitute an early-bound scenario or consider the performance of the late bound scenario.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="b3ecc-115">Efeito sobre o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="b3ecc-115">Effect on the Runtime</span></span>  
 <span data-ttu-id="b3ecc-116">Esse MDA é ativado para cada cache <xref:System.Reflection.MemberInfo> criado.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-116">This MDA is activated for every <xref:System.Reflection.MemberInfo> cache that is created.</span></span> <span data-ttu-id="b3ecc-117">O impacto de desempenho é negligenciável.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-117">The performance impact is negligible.</span></span>  
  
## <a name="output"></a><span data-ttu-id="b3ecc-118">Saída</span><span class="sxs-lookup"><span data-stu-id="b3ecc-118">Output</span></span>  
 <span data-ttu-id="b3ecc-119">O MDA gera uma mensagem indicando que o cache <xref:System.Reflection.MemberInfo> foi criado.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-119">The MDA outputs a message indicating the <xref:System.Reflection.MemberInfo> cache was created.</span></span> <span data-ttu-id="b3ecc-120">Use um depurador para obter um rastreamento de pilha mostrando o local em que o programa está usando reflexão.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-120">Use a debugger to get a stack trace showing where your program is using reflection.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="b3ecc-121">Configuração</span><span class="sxs-lookup"><span data-stu-id="b3ecc-121">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <memberInfoCacheCreation/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a><span data-ttu-id="b3ecc-122">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b3ecc-122">Example</span></span>  
 <span data-ttu-id="b3ecc-123">Esse código de exemplo ativará o MDA `memberInfoCacheCreation`.</span><span class="sxs-lookup"><span data-stu-id="b3ecc-123">This sample code will activate the `memberInfoCacheCreation` MDA.</span></span>  
  
```  
using System;  
  
public class Exe  
{  
    public static void Main()  
    {  
        typeof(object).GetMethods();  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="b3ecc-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b3ecc-124">See Also</span></span>  
 <span data-ttu-id="b3ecc-125"><xref:System.Reflection.MemberInfo></span><span class="sxs-lookup"><span data-stu-id="b3ecc-125"><xref:System.Reflection.MemberInfo></span></span>   
 [<span data-ttu-id="b3ecc-126">Diagnosticando erros com Assistentes de Depuração Gerenciados</span><span class="sxs-lookup"><span data-stu-id="b3ecc-126">Diagnosing Errors with Managed Debugging Assistants</span></span>](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
