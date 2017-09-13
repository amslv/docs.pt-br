---
title: MDA dangerousThreadingAPI
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
- suspending threads
- DangerousThreadingAPI MDA
- managed debugging assistants (MDAs), dangerous threading operations
- threading [.NET Framework], suspending
- MDAs (managed debugging assistants), dangerous threading operations
- Suspend method
- threading [.NET Framework], managed debugging assistants
ms.assetid: 3e5efbc5-92e4-4229-b31f-ce368a1adb96
caps.latest.revision: 10
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: fd0d8b8a4a96e1e92aa8cf58ee49adf7b51857ab
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="dangerousthreadingapi-mda"></a><span data-ttu-id="88980-102">MDA dangerousThreadingAPI</span><span class="sxs-lookup"><span data-stu-id="88980-102">dangerousThreadingAPI MDA</span></span>
<span data-ttu-id="88980-103">O MDA (assistente para depuração gerenciada) `dangerousThreadingAPI` é ativado quando o método <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> é chamado em um thread que não seja o thread atual.</span><span class="sxs-lookup"><span data-stu-id="88980-103">The `dangerousThreadingAPI` managed debugging assistant (MDA) is activated when the <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> method is called on a thread other than the current thread.</span></span>  
  
## <a name="symptoms"></a><span data-ttu-id="88980-104">Sintomas</span><span class="sxs-lookup"><span data-stu-id="88980-104">Symptoms</span></span>  
 <span data-ttu-id="88980-105">Um aplicativo não está respondendo ou para de responder por tempo indefinido.</span><span class="sxs-lookup"><span data-stu-id="88980-105">An application is unresponsive or hangs indefinitely.</span></span> <span data-ttu-id="88980-106">Os dados do sistema ou do aplicativo podem ser deixados em um estado imprevisível temporariamente ou mesmo depois que um aplicativo foi desligado.</span><span class="sxs-lookup"><span data-stu-id="88980-106">System or application data might be left in an unpredictable state temporarily or even after an application has been shut down.</span></span> <span data-ttu-id="88980-107">Algumas operações não são concluídas como esperado.</span><span class="sxs-lookup"><span data-stu-id="88980-107">Some operations are not completing as expected.</span></span>  
  
 <span data-ttu-id="88980-108">Os sintomas podem variar muito devido à aleatoriedade inerente ao problema.</span><span class="sxs-lookup"><span data-stu-id="88980-108">Symptoms can vary widely due to the randomness inherent to the problem.</span></span>  
  
## <a name="cause"></a><span data-ttu-id="88980-109">Causa</span><span class="sxs-lookup"><span data-stu-id="88980-109">Cause</span></span>  
 <span data-ttu-id="88980-110">Um thread é suspenso de forma assíncrona por outro thread usando o método <xref:System.Threading.Thread.Suspend%2A>.</span><span class="sxs-lookup"><span data-stu-id="88980-110">A thread is asynchronously suspended by another thread using the <xref:System.Threading.Thread.Suspend%2A> method.</span></span> <span data-ttu-id="88980-111">Não há nenhuma maneira de determinar quando é seguro suspender outro thread que pode estar no meio de uma operação.</span><span class="sxs-lookup"><span data-stu-id="88980-111">There is no way to determine when it is safe to suspend another thread which might be in the middle of an operation.</span></span> <span data-ttu-id="88980-112">A suspensão do thread pode resultar na corrupção de dados ou na interrupção de invariáveis.</span><span class="sxs-lookup"><span data-stu-id="88980-112">Suspending the thread can result in the corruption of data or the breaking of invariants.</span></span> <span data-ttu-id="88980-113">Caso um thread precise ser colocado em um estado suspenso e nunca ser retomado usando o método <xref:System.Threading.Thread.Resume%2A>, o aplicativo poderá parar de responder por tempo indefinido e, possivelmente, danificar os dados do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88980-113">Should a thread be placed into a suspended state and never resumed using the <xref:System.Threading.Thread.Resume%2A> method, the application can hang indefinitely and possibly damage application data.</span></span> <span data-ttu-id="88980-114">Esses métodos foram marcados como obsoletos.</span><span class="sxs-lookup"><span data-stu-id="88980-114">These methods have been marked as obsolete.</span></span>  
  
 <span data-ttu-id="88980-115">Se os primitivos de sincronização forem mantidos pelo thread de destino, eles permanecerão mantidos durante a suspensão.</span><span class="sxs-lookup"><span data-stu-id="88980-115">If synchronization primitives are held by the target thread, they remain held during suspension.</span></span> <span data-ttu-id="88980-116">Isso pode levar a deadlocks, caso outro thread, por exemplo, o thread que executa o <xref:System.Threading.Thread.Suspend%2A>, tente adquirir um bloqueio no primitivo.</span><span class="sxs-lookup"><span data-stu-id="88980-116">This can lead to deadlocks should another thread, for example the thread performing the <xref:System.Threading.Thread.Suspend%2A>, attempt to acquire a lock on the primitive.</span></span> <span data-ttu-id="88980-117">Nessa situação, o problema se manifesta como um deadlock.</span><span class="sxs-lookup"><span data-stu-id="88980-117">In this situation, the problem manifests itself as a deadlock.</span></span>  
  
## <a name="resolution"></a><span data-ttu-id="88980-118">Resolução</span><span class="sxs-lookup"><span data-stu-id="88980-118">Resolution</span></span>  
 <span data-ttu-id="88980-119">Evite designs que exigem o uso de <xref:System.Threading.Thread.Suspend%2A> e <xref:System.Threading.Thread.Resume%2A>.</span><span class="sxs-lookup"><span data-stu-id="88980-119">Avoid designs that require the use of <xref:System.Threading.Thread.Suspend%2A> and <xref:System.Threading.Thread.Resume%2A>.</span></span> <span data-ttu-id="88980-120">Para cooperação entre threads, use primitivos de sincronização como <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex> ou a instrução `lock` do C#.</span><span class="sxs-lookup"><span data-stu-id="88980-120">For cooperation between threads, use synchronization primitives such as <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex>, or the C# `lock` statement.</span></span> <span data-ttu-id="88980-121">Se você precisar usar esses métodos, reduza a janela de tempo e minimize a quantidade de código que é executada enquanto o thread está em um estado suspenso.</span><span class="sxs-lookup"><span data-stu-id="88980-121">If you must use these methods, reduce the window of time and minimize the amount of code that executes while the thread is in a suspended state.</span></span>  
  
## <a name="effect-on-the-runtime"></a><span data-ttu-id="88980-122">Efeito sobre o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="88980-122">Effect on the Runtime</span></span>  
 <span data-ttu-id="88980-123">Esse MDA não tem efeito sobre o CLR.</span><span class="sxs-lookup"><span data-stu-id="88980-123">This MDA has no effect on the CLR.</span></span> <span data-ttu-id="88980-124">Ele relata apenas os dados sobre operações de threading perigosas.</span><span class="sxs-lookup"><span data-stu-id="88980-124">It only reports data about dangerous threading operations.</span></span>  
  
## <a name="output"></a><span data-ttu-id="88980-125">Saída</span><span class="sxs-lookup"><span data-stu-id="88980-125">Output</span></span>  
 <span data-ttu-id="88980-126">O MDA identifica o método de threading perigoso que fez com que ele fosse ativado.</span><span class="sxs-lookup"><span data-stu-id="88980-126">The MDA identifies the dangerous threading method that caused it to be activated.</span></span>  
  
## <a name="configuration"></a><span data-ttu-id="88980-127">Configuração</span><span class="sxs-lookup"><span data-stu-id="88980-127">Configuration</span></span>  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dangerousThreadingAPI />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a><span data-ttu-id="88980-128">Exemplo</span><span class="sxs-lookup"><span data-stu-id="88980-128">Example</span></span>  
 <span data-ttu-id="88980-129">O exemplo de código a seguir demonstra uma chamada ao método <xref:System.Threading.Thread.Suspend%2A> que causa a ativação da `dangerousThreadingAPI`.</span><span class="sxs-lookup"><span data-stu-id="88980-129">The following code example demonstrates a call to the <xref:System.Threading.Thread.Suspend%2A> method that causes the activation of the `dangerousThreadingAPI`.</span></span>  
  
```  
using System.Threading;  
void FireMda()  
{  
Thread t = new Thread(delegate() { Thread.Sleep(1000); });  
    t.Start();  
    // The following line activates the MDA.  
    t.Suspend();   
    t.Resume();  
    t.Join();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="88980-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="88980-130">See Also</span></span>  
 <span data-ttu-id="88980-131"><xref:System.Threading.Thread></span><span class="sxs-lookup"><span data-stu-id="88980-131"><xref:System.Threading.Thread></span></span>   
 <span data-ttu-id="88980-132">[Diagnosticando erros com Assistentes de Depuração Gerenciados](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md) </span><span class="sxs-lookup"><span data-stu-id="88980-132">[Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md) </span></span>  
 [<span data-ttu-id="88980-133">Instrução lock</span><span class="sxs-lookup"><span data-stu-id="88980-133">lock Statement</span></span>](~/docs/csharp/language-reference/keywords/lock-statement.md)
