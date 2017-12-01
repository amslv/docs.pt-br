---
title: "Como: Implementar um padrão de fluxo de dados de produtor-consumidor"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TPL dataflow library, implementing producer-consumer pattern
- Task Parallel Library, dataflows
- producer-consumer patterns, implementing [TPL]
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: e1aba08e8364d8a21f70ab480d58041115a4849e
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="how-to-implement-a-producer-consumer-dataflow-pattern"></a><span data-ttu-id="18574-102">Como: Implementar um padrão de fluxo de dados de produtor-consumidor</span><span class="sxs-lookup"><span data-stu-id="18574-102">How to: Implement a Producer-Consumer Dataflow Pattern</span></span>
<span data-ttu-id="18574-103">Este documento descreve como usar a biblioteca de fluxo de dados TPL para implementar um padrão de produtor-consumidor.</span><span class="sxs-lookup"><span data-stu-id="18574-103">This document describes how to use the TPL Dataflow Library to implement a producer-consumer pattern.</span></span> <span data-ttu-id="18574-104">Nesse padrão, o *produtor* envia mensagens para um bloco de mensagens e o *consumidor* lê mensagens esse bloco.</span><span class="sxs-lookup"><span data-stu-id="18574-104">In this pattern, the *producer* sends messages to a message block, and the *consumer* reads messages from that block.</span></span>  
  
> [!TIP]
>  <span data-ttu-id="18574-105">A biblioteca de fluxo de dados TPL (<xref:System.Threading.Tasks.Dataflow?displayProperty=nameWithType> namespace) não é distribuído com o [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].</span><span class="sxs-lookup"><span data-stu-id="18574-105">The TPL Dataflow Library (<xref:System.Threading.Tasks.Dataflow?displayProperty=nameWithType> namespace) is not distributed with the [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].</span></span> <span data-ttu-id="18574-106">Para instalar o <xref:System.Threading.Tasks.Dataflow> namespace, abra seu projeto no [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], escolha **gerenciar pacotes NuGet** no menu projeto e pesquise online o `Microsoft.Tpl.Dataflow` pacote.</span><span class="sxs-lookup"><span data-stu-id="18574-106">To install the <xref:System.Threading.Tasks.Dataflow> namespace, open your project in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], choose **Manage NuGet Packages** from the Project menu, and search online for the `Microsoft.Tpl.Dataflow` package.</span></span>  
  
## <a name="example"></a><span data-ttu-id="18574-107">Exemplo</span><span class="sxs-lookup"><span data-stu-id="18574-107">Example</span></span>  
 <span data-ttu-id="18574-108">O exemplo a seguir demonstra um modelo básico de produtor-consumidor que usa o fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="18574-108">The following example demonstrates a basic producer- consumer model that uses dataflow.</span></span> <span data-ttu-id="18574-109">O `Produce` método grava matrizes que contêm aleatórios bytes de dados para um <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=nameWithType> objeto e o `Consume` método lê bytes de um <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=nameWithType> objeto.</span><span class="sxs-lookup"><span data-stu-id="18574-109">The `Produce` method writes arrays that contain random bytes of data to a <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=nameWithType> object and the `Consume` method reads bytes from a <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=nameWithType> object.</span></span> <span data-ttu-id="18574-110">Ao agir no <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> e <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> interfaces, em vez de seus tipos derivados, você pode escrever o código reutilizável que pode agir em uma variedade de tipos de bloco de fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="18574-110">By acting on the <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> and <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> interfaces, instead of their derived types, you can write reusable code that can act on a variety of dataflow block types.</span></span> <span data-ttu-id="18574-111">Este exemplo usa o <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> classe.</span><span class="sxs-lookup"><span data-stu-id="18574-111">This example uses the <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> class.</span></span> <span data-ttu-id="18574-112">Porque o <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> classe atua como uma fonte ambos os blocos e como um bloco de destino, o produtor e consumidor podem usar um objeto compartilhado para transferir dados.</span><span class="sxs-lookup"><span data-stu-id="18574-112">Because the <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> class acts as both a source block and as a target block, the producer and the consumer can use a shared object to transfer data.</span></span>  
  
 <span data-ttu-id="18574-113">O `Produce` chamadas de método de <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> método em um loop de forma síncrona gravar dados para o bloco de destino.</span><span class="sxs-lookup"><span data-stu-id="18574-113">The `Produce` method calls the <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> method in a loop to synchronously write data to the target block.</span></span> <span data-ttu-id="18574-114">Após o `Produce` método grava todos os dados para o bloco de destino, ele chama o <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> método para indicar que o bloco nunca terá dados adicionais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="18574-114">After the `Produce` method writes all data to the target block, it calls the <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> method to indicate that the block will never have additional data available.</span></span> <span data-ttu-id="18574-115">O `Consume` método usa o [async](~/docs/csharp/language-reference/keywords/async.md) e [await](~/docs/csharp/language-reference/keywords/await.md) operadores ([Async](~/docs/visual-basic/language-reference/modifiers/async.md) e [Await](~/docs/visual-basic/language-reference/operators/await-operator.md) em [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) para computar de forma assíncrona o número total de bytes recebidos do <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> objeto.</span><span class="sxs-lookup"><span data-stu-id="18574-115">The `Consume` method uses the [async](~/docs/csharp/language-reference/keywords/async.md) and [await](~/docs/csharp/language-reference/keywords/await.md) operators ([Async](~/docs/visual-basic/language-reference/modifiers/async.md) and [Await](~/docs/visual-basic/language-reference/operators/await-operator.md) in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) to asynchronously compute the total number of bytes that are received from the <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> object.</span></span> <span data-ttu-id="18574-116">Para agir de forma assíncrona, o `Consume` chamadas de método de <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> método para receber uma notificação quando o bloco de origem tem dados disponíveis e quando o bloco de código-fonte nunca terá dados adicionais disponíveis.</span><span class="sxs-lookup"><span data-stu-id="18574-116">To act asynchronously, the `Consume` method calls the <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> method to receive a notification when the source block has data available and when the source block will never have additional data available.</span></span>  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="18574-117">Compilando o código</span><span class="sxs-lookup"><span data-stu-id="18574-117">Compiling the Code</span></span>  
 <span data-ttu-id="18574-118">Copie o código de exemplo e cole-o em um projeto do Visual Studio ou colá-lo em um arquivo chamado `DataflowProducerConsumer.cs` (`DataflowProducerConsumer.vb` para [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]), e, em seguida, execute o seguinte comando em uma janela de Prompt de comando do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="18574-118">Copy the example code and paste it in a Visual Studio project, or paste it in a file that is named `DataflowProducerConsumer.cs` (`DataflowProducerConsumer.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]), and then run the following command in a Visual Studio Command Prompt window.</span></span>  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 <span data-ttu-id="18574-119">**CSC.exe /r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.cs**</span><span class="sxs-lookup"><span data-stu-id="18574-119">**csc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.cs**</span></span>  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 <span data-ttu-id="18574-120">**Vbc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.vb**</span><span class="sxs-lookup"><span data-stu-id="18574-120">**vbc.exe /r:System.Threading.Tasks.Dataflow.dll DataflowProducerConsumer.vb**</span></span>  
  
## <a name="robust-programming"></a><span data-ttu-id="18574-121">Programação robusta</span><span class="sxs-lookup"><span data-stu-id="18574-121">Robust Programming</span></span>  
 <span data-ttu-id="18574-122">Este exemplo usa apenas um consumidor para processar os dados de origem.</span><span class="sxs-lookup"><span data-stu-id="18574-122">This example uses just one consumer to process the source data.</span></span> <span data-ttu-id="18574-123">Se você tiver vários consumidores em seu aplicativo, use o <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> método para ler dados do bloco de código-fonte, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="18574-123">If you have multiple consumers in your application, use the <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> method to read data from the source block, as shown in the following example.</span></span>  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]  
  
 <span data-ttu-id="18574-124">O <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> método retorna `False` quando não há dados disponíveis.</span><span class="sxs-lookup"><span data-stu-id="18574-124">The <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> method returns `False` when no data is available.</span></span> <span data-ttu-id="18574-125">Quando vários consumidores devem acessar simultaneamente o bloco de código-fonte, esse mecanismo garante que dados ainda estão disponíveis após a chamada a <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A>.</span><span class="sxs-lookup"><span data-stu-id="18574-125">When multiple consumers must access the source block concurrently, this mechanism guarantees that data is still available after the call to <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A>.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="18574-126">Consulte também</span><span class="sxs-lookup"><span data-stu-id="18574-126">See Also</span></span>  
 [<span data-ttu-id="18574-127">Fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="18574-127">Dataflow</span></span>](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)