---
title: "Otimização de uso único de fase de confirmação e notificação de fase única passível de promoção"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 57beaf1a-fb4d-441a-ab1d-bc0c14ce7899
caps.latest.revision: "3"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: 66f60ba31983a6cfbfda0238d80a6e8ad81d30ab
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="optimization-using-single-phase-commit-and-promotable-single-phase-notification"></a><span data-ttu-id="e56ef-102">Otimização de uso único de fase de confirmação e notificação de fase única passível de promoção</span><span class="sxs-lookup"><span data-stu-id="e56ef-102">Optimization using Single Phase Commit and Promotable Single Phase Notification</span></span>
<span data-ttu-id="e56ef-103">Este tópico descreve os mecanismos fornecidos pelo <xref:System.Transactions> infra-estrutura para otimizar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e56ef-103">This topic describes the mechanisms provided by the <xref:System.Transactions> infrastructure to optimize performance.</span></span>  
  
## <a name="promotable-single-phase-enlistment"></a><span data-ttu-id="e56ef-104">Inscrição de fase única passíveis de promoção</span><span class="sxs-lookup"><span data-stu-id="e56ef-104">Promotable Single Phase Enlistment</span></span>  
 <span data-ttu-id="e56ef-105">O <xref:System.Transactions> infra-estrutura administrates uma transação dentro de um único domínio de aplicativo que envolve a no máximo um único recurso durável ou vários recursos voláteis.</span><span class="sxs-lookup"><span data-stu-id="e56ef-105">The <xref:System.Transactions> infrastructure administrates a transaction inside a single application domain that involves at most a single durable resource or multiple volatile resources.</span></span> <span data-ttu-id="e56ef-106">Como o <xref:System.Transactions> infra-estrutura usa chamadas de domínio apenas intra-aplicativo, ele produz a melhor taxa de transferência e o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e56ef-106">Since the <xref:System.Transactions> infrastructure uses only intra-application domain calls, it yields the best throughput and performance.</span></span>  
  
 <span data-ttu-id="e56ef-107">No entanto, se a transação é fornecida a outro objeto em outro domínio de aplicativo (incluindo entre limites de processo e da máquinas) no mesmo computador, ou se você se inscrever outro gerenciador de recursos duráveis, o <xref:System.Transactions> infra-estrutura aumenta automaticamente a transação a ser gerenciado pelo MSDTC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-107">However, if the transaction is provided to another object in another application domain (including across process and machine boundaries) on the same computer, or if you were to enlist another durable resource manager, the <xref:System.Transactions> infrastructure automatically escalates the transaction to be managed by the MSDTC.</span></span> <span data-ttu-id="e56ef-108">Uma transação gerenciada por MSDTC não é tão em termos de desempenho como um gerenciado pelo <xref:System.Transactions> infra-estrutura.</span><span class="sxs-lookup"><span data-stu-id="e56ef-108">A transaction managed by MSDTC is not as performance-wise as one managed by the <xref:System.Transactions> infrastructure.</span></span>  
  
 <span data-ttu-id="e56ef-109">Para otimizar o desempenho, o <xref:System.Transactions> infra-estrutura fornece o podem ser promovidas única fase de inscrição (PSPE) que permite que um único durável recurso remoto, localizado em um domínio de aplicativo diferente, o processo ou a máquina, participe de um <xref:System.Transactions> transação sem fazer com que ele ser escalonado para uma transação MSDTC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-109">To optimize performance, the <xref:System.Transactions> infrastructure provides the Promotable Single Phase Enlistment (PSPE) that allows a single remote durable resource, located in a different application domain, process or machine, to participate in a <xref:System.Transactions> transaction without causing it to be escalated to an MSDTC transaction.</span></span>  <span data-ttu-id="e56ef-110">Esse Gerenciador de recursos (RM) pode hospedar e "proprietário" de uma transação que posteriormente pode ser escalonada para uma transação distribuída (ou transação MSDTC) se necessário.</span><span class="sxs-lookup"><span data-stu-id="e56ef-110">This resource manager (RM) can host and "own" a transaction that can later be escalated to a distributed transaction (or MSDTC transaction) if necessary.</span></span> <span data-ttu-id="e56ef-111">Isso reduz a possibilidade de usar o MSDTC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-111">This reduces the chance of using the MSDTC.</span></span>  
  
 <span data-ttu-id="e56ef-112">O Gerenciador de recursos específico normalmente tem suas próprias transações distribuídas não internas e precisa oferecer suporte a converter essas transações em transações distribuídas em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e56ef-112">This specific resource manager usually has its own internal non distributed transactions and it needs to support converting those transactions to distributed transactions at runtime.</span></span> <span data-ttu-id="e56ef-113">Por exemplo, o SQL Server 2005 é tal um Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e56ef-113">For example, SQL Server 2005 is such a resource manager.</span></span> <span data-ttu-id="e56ef-114">Nesse caso, o <xref:System.Transactions> infra-estrutura usa uma função de gerenciamento de passivo monitorando apenas a transação para uma necessidade de escalonamento.</span><span class="sxs-lookup"><span data-stu-id="e56ef-114">In such case, the <xref:System.Transactions> infrastructure takes a passive management role by just monitoring the transaction for a need for escalation.</span></span> <span data-ttu-id="e56ef-115">Para oferecer suporte a interação entre o <xref:System.Transactions> infra-estrutura e Gerenciador de recursos, o último precisa implementar a interface <xref:System.Transactions.IPromotableSinglePhaseNotification>.</span><span class="sxs-lookup"><span data-stu-id="e56ef-115">To support the interaction between the <xref:System.Transactions> infrastructure and resource manager, the latter needs to implement the interface <xref:System.Transactions.IPromotableSinglePhaseNotification>.</span></span>  
  
 <span data-ttu-id="e56ef-116">O <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> método é usado para inscrever um único recurso durável que pode ser escalonado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="e56ef-116">The <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> method is used to enlist a single durable resource that can be escalated later.</span></span> <span data-ttu-id="e56ef-117">Esse método garante que a inscrição pode ser escalonada conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="e56ef-117">This method ensures that the enlistment can be escalated as needed.</span></span> <span data-ttu-id="e56ef-118">Se a inscrição for bem-sucedida, o Gerenciador de recursos cria sua transação interna e o associa a <xref:System.Transactions> transação.</span><span class="sxs-lookup"><span data-stu-id="e56ef-118">If the enlistment succeeds, the RM creates its internal transaction and associates it with the <xref:System.Transactions> transaction.</span></span> <span data-ttu-id="e56ef-119">Se a inscrição PSPE falhar, o Gerenciador de recursos em vez disso, deve inscrever usando o <xref:System.Transactions.Transaction.EnlistDurable%2A> método.</span><span class="sxs-lookup"><span data-stu-id="e56ef-119">If the PSPE enlistment fails, the RM should instead enlist using the <xref:System.Transactions.Transaction.EnlistDurable%2A> method.</span></span> <span data-ttu-id="e56ef-120">Falhas para se inscrever no PSPE podem acontecer quando a transação já for uma transação distribuída ou outro RM já executou uma inscrição de PSPE</span><span class="sxs-lookup"><span data-stu-id="e56ef-120">Failures to enlist in PSPE might happen when the transaction is already a distributed transaction, or when another RM has already performed a PSPE enlistment</span></span>  
  
 <span data-ttu-id="e56ef-121">Depois de inscrito, chamadas por clientes para confirmar ou anular a <xref:System.Transactions> transação são convertidos em chamadas no Gerenciador de recursos, invocando o <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> método, ou o <xref:System.Transactions.IPromotableSinglePhaseNotification.Rollback%2A> respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e56ef-121">Once enlisted, calls by clients to commit or abort the <xref:System.Transactions> transaction are converted to calls on the Resource Manager by invoking the <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> method, or the <xref:System.Transactions.IPromotableSinglePhaseNotification.Rollback%2A> respectively.</span></span>  
  
 <span data-ttu-id="e56ef-122">Se o <xref:System.Transactions> transação nunca requer escalonamento, quando a transação é confirmada, o RM recebe um <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> notificação.</span><span class="sxs-lookup"><span data-stu-id="e56ef-122">If the <xref:System.Transactions> transaction never requires escalation, when the transaction is committed, the RM receives a <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> notification.</span></span> <span data-ttu-id="e56ef-123">Em seguida, ele poderá confirmar a transação interna que foi inicialmente criada.</span><span class="sxs-lookup"><span data-stu-id="e56ef-123">It can then commit the internal transaction that was initially created.</span></span>  
  
 <span data-ttu-id="e56ef-124">Se o <xref:System.Transactions> transação deverá ser escalonado (por exemplo, para oferecer suporte a vários RMs), <xref:System.Transactions> informa ao Gerenciador de recursos, chamando o <xref:System.Transactions.ITransactionPromoter.Promote%2A> método no <xref:System.Transactions.ITransactionPromoter> interface, da qual o <xref:System.Transactions.IPromotableSinglePhaseNotification> interface deriva.</span><span class="sxs-lookup"><span data-stu-id="e56ef-124">If the <xref:System.Transactions> transaction needs to be escalated (e.g., to support multiple RMs), <xref:System.Transactions> informs the resource manager by calling the <xref:System.Transactions.ITransactionPromoter.Promote%2A> method on the <xref:System.Transactions.ITransactionPromoter> interface, from which the <xref:System.Transactions.IPromotableSinglePhaseNotification> interface derives.</span></span> <span data-ttu-id="e56ef-125">O Gerenciador de recursos converte a transação interna de uma transação local (que não exigem registro em log) para um objeto de transação que é capaz de participar de uma transação do DTC e associa o trabalho já realizado.</span><span class="sxs-lookup"><span data-stu-id="e56ef-125">The resource manager then converts the transaction internally from a local transaction (which does not require logging) to a transaction object that is capable of participating in a DTC transaction, and associates it with the work already done.</span></span> <span data-ttu-id="e56ef-126">Quando a transação é solicitada a confirmar, o Gerenciador de transações ainda envia o <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> notificação para o Gerenciador de recursos, que confirma a transação distribuída que criou durante a expansão.</span><span class="sxs-lookup"><span data-stu-id="e56ef-126">When the transaction is asked to commit, the transaction manager still sends the <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> notification to the resource manager, which commits the distributed transaction that it created during escalation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e56ef-127">O **TransactionCommitted** rastreamentos (que são gerados quando uma confirmação é invocada na transação escalada) contém a ID de atividade de transação do DTC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-127">The **TransactionCommitted** traces (that are generated when a Commit is invoked on the escalated transaction) contain the activity ID of the DTC transaction.</span></span>  
  
 <span data-ttu-id="e56ef-128">Para obter mais informações sobre o escalonamento de bloqueios de gerenciamento, consulte [escalonamento de bloqueios de gerenciamento de transação](../../../../docs/framework/data/transactions/transaction-management-escalation.md).</span><span class="sxs-lookup"><span data-stu-id="e56ef-128">For more information on management escalation, see [Transaction Management Escalation](../../../../docs/framework/data/transactions/transaction-management-escalation.md).</span></span>  
  
## <a name="transaction-management-escalation-scenario"></a><span data-ttu-id="e56ef-129">Cenário de escalonamento de gerenciamento de transações</span><span class="sxs-lookup"><span data-stu-id="e56ef-129">Transaction Management Escalation Scenario</span></span>  
 <span data-ttu-id="e56ef-130">O cenário a seguir demonstra um escalonamento para uma transação distribuída usando o <xref:System.Data> namespace como o 'proxy' para o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="e56ef-130">The following scenario demonstrates an escalation to a distributed transaction using the <xref:System.Data> namespace as the ‘proxy’ for the resource manager.</span></span> <span data-ttu-id="e56ef-131">Este cenário pressupõe que já existe um <xref:System.Data> conexão com o banco de dados, CN1, envolvidos na transação e o aplicativo deseja envolver outro <xref:System.Data> conexão, CN2.</span><span class="sxs-lookup"><span data-stu-id="e56ef-131">This scenario assumes that there is already one <xref:System.Data> connection to the database, CN1, involved in the transaction, and the application wants to involve another <xref:System.Data> connection, CN2.</span></span> <span data-ttu-id="e56ef-132">A transação deve ser escalada para o DTC, como uma transação de confirmação de duas fases distribuída completa.</span><span class="sxs-lookup"><span data-stu-id="e56ef-132">The transaction must be escalated to DTC, as a full distributed two-phase commit transaction.</span></span>  
  
 <span data-ttu-id="e56ef-133">Nesse cenário,</span><span class="sxs-lookup"><span data-stu-id="e56ef-133">In this scenario,</span></span>  
  
1.  <span data-ttu-id="e56ef-134">Chamadas de CN1 a <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> método para se inscrever na transação.</span><span class="sxs-lookup"><span data-stu-id="e56ef-134">CN1 calls the <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> method to enlist in the transaction.</span></span> <span data-ttu-id="e56ef-135">Em seguida, a transação é ainda local e não há nenhum inscrições podem ser promovidas na transação, para que o <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> chamada for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e56ef-135">Then, the transaction is still local and there are no other promotable enlistments on the transaction, so the <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> call succeeds.</span></span>  
  
2.  <span data-ttu-id="e56ef-136">Quando a segunda conexão, CN2 chama <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>, a chamada falhará porque não há outra inscrição podem ser promovida envolvidas.</span><span class="sxs-lookup"><span data-stu-id="e56ef-136">When the second connection, CN2 calls <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>, the call fails because there is another promotable enlistment involved.</span></span> <span data-ttu-id="e56ef-137">Por isso, CN2 deve obter uma transação do DTC para passá-lo para SQL.</span><span class="sxs-lookup"><span data-stu-id="e56ef-137">Because of this, CN2 must get a DTC transaction in order to pass it to SQL.</span></span> <span data-ttu-id="e56ef-138">Para fazer isso, ele usa um dos métodos fornecidos pelo <xref:System.Transactions.TransactionInterop> classe para produzir um formato da transação que pode ser determinado para SQL.</span><span class="sxs-lookup"><span data-stu-id="e56ef-138">To do this, it uses one of the methods provided by the <xref:System.Transactions.TransactionInterop> class to produce a format of the transaction that can be given to SQL.</span></span>  
  
3.  <span data-ttu-id="e56ef-139"><xref:System.Transactions>chama o <xref:System.Transactions.ITransactionPromoter.Promote%2A> método o <xref:System.Transactions.ITransactionPromoter> interface implementada pelo CN1.</span><span class="sxs-lookup"><span data-stu-id="e56ef-139"><xref:System.Transactions> calls the <xref:System.Transactions.ITransactionPromoter.Promote%2A> method on the <xref:System.Transactions.ITransactionPromoter> interface implemented by CN1.</span></span>  
  
4.  <span data-ttu-id="e56ef-140">Neste ponto, CN1 aumenta a transação, usando um mecanismo específico para o SQL 2005 e <xref:System.Data>.</span><span class="sxs-lookup"><span data-stu-id="e56ef-140">At this point, CN1 escalates the transaction, using some mechanism specific to SQL 2005 and <xref:System.Data>.</span></span>  
  
5.  <span data-ttu-id="e56ef-141">O valor de retorno de <xref:System.Transactions.ITransactionPromoter.Promote%2A> método é uma matriz de bytes que contém um token de propagação da transação.</span><span class="sxs-lookup"><span data-stu-id="e56ef-141">The return value from the <xref:System.Transactions.ITransactionPromoter.Promote%2A> method is a byte array that contains a propagation token for the transaction.</span></span> <span data-ttu-id="e56ef-142"><xref:System.Transactions>usa esse token propagaition para criar uma transação do DTC que ele pode incorporar a transação local.</span><span class="sxs-lookup"><span data-stu-id="e56ef-142"><xref:System.Transactions> uses this propagaition token to create a DTC transaction that it can incorporate into the local transaction.</span></span>  
  
6.  <span data-ttu-id="e56ef-143">Neste ponto, CN2 pode usar os dados recebidos de chamar um dos métodos por <xref:System.Transactions.TransactionInterop> para passar a transação para SQL.</span><span class="sxs-lookup"><span data-stu-id="e56ef-143">At this point, CN2 can use the data received from calling one of the methods by <xref:System.Transactions.TransactionInterop> to pass the transaction to SQL.</span></span>  
  
7.  <span data-ttu-id="e56ef-144">Agora, ambos estão inscritos em uma transação distribuída do DTC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-144">Now, both are enlisted in a DTC distributed transaction.</span></span>  
  
## <a name="single-phase-commit-optimization"></a><span data-ttu-id="e56ef-145">Otimização de confirmação de fase única</span><span class="sxs-lookup"><span data-stu-id="e56ef-145">Single Phase Commit Optimization</span></span>  
 <span data-ttu-id="e56ef-146">O protocolo de confirmação de fase única é mais eficiente em tempo de execução, como todas as atualizações são realizadas sem qualquer coordenação explícita.</span><span class="sxs-lookup"><span data-stu-id="e56ef-146">The Single Phase Commit protocol is more efficient at runtime as all updates are done without any explicit coordination.</span></span> <span data-ttu-id="e56ef-147">Para tirar proveito dessa otimização, você deve implementar um Gerenciador de recursos usando <xref:System.Transactions.ISinglePhaseNotification> para o recurso de interface e se inscrever em uma transação usando o <xref:System.Transactions.Transaction.EnlistDurable%2A> ou <xref:System.Transactions.Transaction.EnlistVolatile%2A> método.</span><span class="sxs-lookup"><span data-stu-id="e56ef-147">To take advantage of this optimization, you should implement a resource manager using <xref:System.Transactions.ISinglePhaseNotification> interface for the resource and enlist in a transaction using the <xref:System.Transactions.Transaction.EnlistDurable%2A> or <xref:System.Transactions.Transaction.EnlistVolatile%2A> method.</span></span> <span data-ttu-id="e56ef-148">Especificamente, o *EnlistmentOptions* deve ser igual ao parâmetro <xref:System.Transactions.EnlistmentOptions.None> para garantir que uma confirmação de fase única será executada.</span><span class="sxs-lookup"><span data-stu-id="e56ef-148">Specifically, the *EnlistmentOptions* parameter should equal to <xref:System.Transactions.EnlistmentOptions.None> to ensure that a single phase commit would be performed.</span></span>  
  
 <span data-ttu-id="e56ef-149">Como o <xref:System.Transactions.ISinglePhaseNotification> interface deriva de <xref:System.Transactions.IEnlistmentNotification> a interface, se o RM não está qualificado para confirmação de fase única, ele pode ainda receber a fase de duas notificações de confirmação.</span><span class="sxs-lookup"><span data-stu-id="e56ef-149">Since the <xref:System.Transactions.ISinglePhaseNotification> interface derives from the <xref:System.Transactions.IEnlistmentNotification> interface, if your RM is not eligible for single phase commit, it can still receive the two phase commit notifications.</span></span>  <span data-ttu-id="e56ef-150">Se receber o RM um <xref:System.Transactions.ISinglePhaseNotification.SinglePhaseCommit%2A> notificação do TM, ele deve tentar fazer o trabalho necessário para confirmar e proporcionalmente informam o Gerenciador de transações se a transação deve ser confirmada ou revertida chamando o <xref:System.Transactions.SinglePhaseEnlistment.Committed%2A>, <xref:System.Transactions.SinglePhaseEnlistment.Aborted%2A>, ou <xref:System.Transactions.SinglePhaseEnlistment.InDoubt%2A> método o <xref:System.Transactions.SinglePhaseEnlistment> parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e56ef-150">If your RM receives a <xref:System.Transactions.ISinglePhaseNotification.SinglePhaseCommit%2A> notification from the TM, it should try to do the work necessary for it to commit and correspondingly inform the transaction manager if the transaction is to be committed or rolled back by calling the <xref:System.Transactions.SinglePhaseEnlistment.Committed%2A>, <xref:System.Transactions.SinglePhaseEnlistment.Aborted%2A>, or <xref:System.Transactions.SinglePhaseEnlistment.InDoubt%2A> method on the <xref:System.Transactions.SinglePhaseEnlistment> parameter.</span></span> <span data-ttu-id="e56ef-151">Uma resposta de <xref:System.Transactions.Enlistment.Done%2A> sobre a inscrição neste estágio implica a semântica de somente leitura.</span><span class="sxs-lookup"><span data-stu-id="e56ef-151">A response of <xref:System.Transactions.Enlistment.Done%2A> on the enlistment at this stage implies ReadOnly semantics.</span></span> <span data-ttu-id="e56ef-152">Portanto, você não deve responder <xref:System.Transactions.Enlistment.Done%2A> além de qualquer um dos outros métodos.</span><span class="sxs-lookup"><span data-stu-id="e56ef-152">Therefore, you should not reply <xref:System.Transactions.Enlistment.Done%2A> in addition to any of the other methods.</span></span>  
  
 <span data-ttu-id="e56ef-153">Se houver apenas uma inscrição voláteis e nenhuma inscrição durável, a inscrição volátil recebe a notificação de SPC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-153">If there is only one volatile enlistment and no durable enlistment, the volatile enlistment receives SPC notification.</span></span>  <span data-ttu-id="e56ef-154">Se houver qualquer inscrições voláteis e apenas uma inscrição durável, as inscrições voláteis recebem 2PC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-154">If there are any volatile enlistments and only one durable enlistment, the volatile enlistments receive 2PC.</span></span> <span data-ttu-id="e56ef-155">Quando ele for concluído, a distribuição durável recebe SPC.</span><span class="sxs-lookup"><span data-stu-id="e56ef-155">When it is completed, the durable enlistment receives SPC.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e56ef-156">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e56ef-156">See Also</span></span>  
 [<span data-ttu-id="e56ef-157">Inscrição de recursos como participantes em uma transação</span><span class="sxs-lookup"><span data-stu-id="e56ef-157">Enlisting Resources as Participants in a Transaction</span></span>](../../../../docs/framework/data/transactions/enlisting-resources-as-participants-in-a-transaction.md)  
 [<span data-ttu-id="e56ef-158">Confirmar uma transação de fase única e de várias fases</span><span class="sxs-lookup"><span data-stu-id="e56ef-158">Committing a Transaction in Single-Phase and Multi-Phase</span></span>](../../../../docs/framework/data/transactions/committing-a-transaction-in-single-phase-and-multi-phase.md)