---
title: "Conceitos básicos de transação"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 353f4ee2-e6bf-4b1c-b1c8-385fc8a486c0
caps.latest.revision: "3"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: a21de968f5fbd241bd71169cf9f444b84c05b599
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="transaction-fundamentals"></a><span data-ttu-id="a5018-102">Conceitos básicos de transação</span><span class="sxs-lookup"><span data-stu-id="a5018-102">Transaction Fundamentals</span></span>
<span data-ttu-id="a5018-103">Transações associar várias tarefas.</span><span class="sxs-lookup"><span data-stu-id="a5018-103">Transactions bind multiple tasks together.</span></span> <span data-ttu-id="a5018-104">Por exemplo, imagine que um aplicativo executa duas tarefas.</span><span class="sxs-lookup"><span data-stu-id="a5018-104">For example, imagine that an application performs two tasks.</span></span> <span data-ttu-id="a5018-105">Primeiro, ele cria uma nova tabela em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a5018-105">First, it creates a new table in a database.</span></span> <span data-ttu-id="a5018-106">Em seguida, ele chama um objeto especializado para coletar, formatar e inserir dados na nova tabela.</span><span class="sxs-lookup"><span data-stu-id="a5018-106">Next, it calls a specialized object to collect, format, and insert data into the new table.</span></span> <span data-ttu-id="a5018-107">Essas duas tarefas estão relacionadas e até mesmo interdependentes, que você deseja evitar a criação de uma nova tabela, a menos que você pode preenchê-lo com dados.</span><span class="sxs-lookup"><span data-stu-id="a5018-107">These two tasks are related and even interdependent, such that you want to avoid creating a new table unless you can fill it with data.</span></span> <span data-ttu-id="a5018-108">Ambas as tarefas dentro do escopo de uma única transação em execução impõe a conexão entre elas.</span><span class="sxs-lookup"><span data-stu-id="a5018-108">Executing both tasks within the scope of a single transaction enforces the connection between them.</span></span> <span data-ttu-id="a5018-109">Se a segunda tarefa falhar, a primeira tarefa será revertida para um ponto antes que a nova tabela foi criada.</span><span class="sxs-lookup"><span data-stu-id="a5018-109">If the second task fails, the first task is rolled back to a point before the new table was created.</span></span>  
  
 <span data-ttu-id="a5018-110">Para garantir um comportamento previsível, todas as transações devem ter as propriedades básicas de ACID (atômicas, consistentes, isoladas e duráveis).</span><span class="sxs-lookup"><span data-stu-id="a5018-110">To ensure predictable behavior, all transactions must possess the basic ACID properties (atomic, consistent, isolated, and durable).</span></span> <span data-ttu-id="a5018-111">Essas propriedades reforçam a função de transações de missão crítica como propostas de tudo ou nada.</span><span class="sxs-lookup"><span data-stu-id="a5018-111">These properties reinforce the role of mission-critical transactions as all-or-none propositions.</span></span> <span data-ttu-id="a5018-112">Para obter mais informações sobre ACID, consulte [propriedades ACID](http://go.microsoft.com/fwlink/?LinkId=98791).</span><span class="sxs-lookup"><span data-stu-id="a5018-112">For more information on ACID, please see [ACID Properties](http://go.microsoft.com/fwlink/?LinkId=98791).</span></span> <span data-ttu-id="a5018-113">Em resumo, ACID garante que um conjunto de relacionadas tarefas ter êxito ou falharem como uma unidade.</span><span class="sxs-lookup"><span data-stu-id="a5018-113">In summary, ACID guarantees that a set of related tasks either succeed or fail as a unit.</span></span> <span data-ttu-id="a5018-114">Na transação terminologia, a transação seja confirmada ou anulada.</span><span class="sxs-lookup"><span data-stu-id="a5018-114">In transaction processing terminology, the transaction either commits or aborts.</span></span> <span data-ttu-id="a5018-115">Para uma transação de confirmação, todos os participantes devem garantir que qualquer alteração nos dados será permanente.</span><span class="sxs-lookup"><span data-stu-id="a5018-115">For a transaction to commit, all participants must guarantee that any change to data will be permanent.</span></span> <span data-ttu-id="a5018-116">As alterações devem persistir mesmo que haja falhas do sistema ou outros eventos imprevisíveis.</span><span class="sxs-lookup"><span data-stu-id="a5018-116">Changes must persist despite system crashes or other unforeseen events.</span></span> <span data-ttu-id="a5018-117">Se até mesmo um único participante não fizer essa garantia, a transação inteira falhará.</span><span class="sxs-lookup"><span data-stu-id="a5018-117">If even a single participant fails to make this guarantee, the entire transaction fails.</span></span> <span data-ttu-id="a5018-118">Todas as alterações de dados dentro do escopo da transação serão revertidas para um ponto específico do conjunto.</span><span class="sxs-lookup"><span data-stu-id="a5018-118">All changes to data within the scope of the transaction are rolled back to a specific set point.</span></span>  
  
 <span data-ttu-id="a5018-119">Uma transação pode ser restrito a um recurso de dados simples, como uma fila de banco de dados ou mensagem.</span><span class="sxs-lookup"><span data-stu-id="a5018-119">A transaction can be confined to a single data resource, such as a database or message queue.</span></span> <span data-ttu-id="a5018-120">Nesse cenário, a transação local é gerenciada pelo Gerenciador de transações fornecida pelo <xref:System.Transactions> , que gera o ganho de desempenho.</span><span class="sxs-lookup"><span data-stu-id="a5018-120">In this scenario, the local transaction is managed by the Transaction Manager provided by <xref:System.Transactions> , which generates performance gain.</span></span> <span data-ttu-id="a5018-121">Controlado pelo recurso de dados, essas transações são eficientes e fáceis de gerenciar.</span><span class="sxs-lookup"><span data-stu-id="a5018-121">Controlled by the data resource, these transactions are efficient and easy to manage.</span></span>  
  
 <span data-ttu-id="a5018-122">As transações também podem abranger vários recursos de dados.</span><span class="sxs-lookup"><span data-stu-id="a5018-122">Transactions can also span multiple data resources.</span></span> <span data-ttu-id="a5018-123">Transações distribuídas lhe oferece a capacidade de incorporar várias operações distintas que ocorrem em diferentes sistemas em uma única passagem ou falha da ação.</span><span class="sxs-lookup"><span data-stu-id="a5018-123">Distributed transactions give you the ability to incorporate several distinct operations occurring on different systems into a single pass or fail action.</span></span> <span data-ttu-id="a5018-124">Nesse cenário, as transações são coordenadas pelo Microsoft Distributed transação coordenador (MSDTC) que reside em cada sistema.</span><span class="sxs-lookup"><span data-stu-id="a5018-124">In this scenario, the transactions are coordinated by the Microsoft Distributed Transaction Coordinator (MSDTC) that resides in each system.</span></span>  
  
 <span data-ttu-id="a5018-125">Quando você desenvolve um aplicativo transacional usando as classes fornecidas pela <xref:System.Transactions>, você não precisa se preocupar sobre que tipo de transações que você precisa, ou o Gerenciador de transações envolvidos.</span><span class="sxs-lookup"><span data-stu-id="a5018-125">When you develop a transactional application using the classes provided by <xref:System.Transactions>, you do not need to worry about what kind of transactions you need, or the transaction manager involved.</span></span> <span data-ttu-id="a5018-126">O <xref:System.Transactions> infra-estrutura gerencia automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="a5018-126">The <xref:System.Transactions> infrastructure automatically manages these for you.</span></span>  
  
 <span data-ttu-id="a5018-127">Quando você cria uma transação, você pode especificar o nível de isolamento que se aplica à transação.</span><span class="sxs-lookup"><span data-stu-id="a5018-127">When you create a transaction, you can specify the isolation level that applies to the transaction.</span></span> <span data-ttu-id="a5018-128">O nível de isolamento definido pelo <xref:System.Transactions.IsolationLevel> da classe, determina o nível de acesso que outras transações deve ter os dados afetado pela sua transação.</span><span class="sxs-lookup"><span data-stu-id="a5018-128">The isolation level, defined by the <xref:System.Transactions.IsolationLevel> class, determines what level of access other transactions will have to the data affected by your transaction.</span></span>  
  
 <span data-ttu-id="a5018-129">Você pode criar transações usando o ADO.NET, <xref:System.EnterpriseServices>, ou o modelo de programação transacional fornecido pelo <xref:System.Transactions> namespace.</span><span class="sxs-lookup"><span data-stu-id="a5018-129">You can create transactions using ADO.NET, <xref:System.EnterpriseServices>, or the transactional programming model provided by the <xref:System.Transactions> namespace.</span></span> <span data-ttu-id="a5018-130">O [recursos fornecidos pelo System. Transactions](../../../../docs/framework/data/transactions/features-provided-by-system-transactions.md) tópico aborda os recursos que você pode usar para escrever um aplicativo transacional usando o <xref:System.Transactions> namespace.</span><span class="sxs-lookup"><span data-stu-id="a5018-130">The [Features Provided by System.Transactions](../../../../docs/framework/data/transactions/features-provided-by-system-transactions.md) topic discusses the features that you can use to write a transactional application using the <xref:System.Transactions> namespace.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a5018-131">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a5018-131">See Also</span></span>  
 <span data-ttu-id="a5018-132">[Features Provided by System.Transactions](../../../../docs/framework/data/transactions/features-provided-by-system-transactions.md) (Recursos fornecidos por System.Transactions)</span><span class="sxs-lookup"><span data-stu-id="a5018-132">[Features Provided by System.Transactions](../../../../docs/framework/data/transactions/features-provided-by-system-transactions.md)</span></span>