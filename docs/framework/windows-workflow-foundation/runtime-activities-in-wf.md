---
title: "Atividades em tempo de execução de WF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5ae8c31-19bc-4655-88b3-6b75cd6a1bd5
caps.latest.revision: "11"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: f3aca3fcdd4fa8d73bf3412d7c20697847d0a699
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="runtime-activities-in-wf"></a><span data-ttu-id="71244-102">Atividades em tempo de execução de WF</span><span class="sxs-lookup"><span data-stu-id="71244-102">Runtime Activities in WF</span></span>
[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]<span data-ttu-id="71244-103"> fornece vários sistema forneceu atividades acessando recursos de tempo de execução de fluxo de trabalho, como a persistência e o encerramento.</span><span class="sxs-lookup"><span data-stu-id="71244-103"> provides several system-provided activities for accessing the features of the workflow runtime, such as persistence and termination.</span></span>  
  
|<span data-ttu-id="71244-104">Atividade</span><span class="sxs-lookup"><span data-stu-id="71244-104">Activity</span></span>|<span data-ttu-id="71244-105">Descrição</span><span class="sxs-lookup"><span data-stu-id="71244-105">Description</span></span>|  
|--------------|-----------------|  
|<xref:System.Activities.Statements.Persist>|<span data-ttu-id="71244-106">Solicita explicitamente que o fluxo de trabalho persiste seu estado.</span><span class="sxs-lookup"><span data-stu-id="71244-106">Explicitly requests that the workflow persist its state.</span></span>|  
|<xref:System.Activities.Statements.TerminateWorkflow>|<span data-ttu-id="71244-107">Finaliza a instância em execução de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="71244-107">Terminates the running workflow instance.</span></span>|  
|<xref:System.Activities.Statements.NoPersistScope>|<span data-ttu-id="71244-108">Uma atividade do contêiner que impede que as atividades filhos persistam.</span><span class="sxs-lookup"><span data-stu-id="71244-108">A container activity that prevents child activities from persisting.</span></span>|