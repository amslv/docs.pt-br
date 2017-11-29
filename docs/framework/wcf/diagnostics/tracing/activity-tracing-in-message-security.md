---
title: "Rastreamento de atividades em segurança de mensagens"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68862534-3b2e-4270-b097-8121b12a2c97
caps.latest.revision: "7"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.openlocfilehash: 60156e284c55d765de417fe891185d1aba720816
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="activity-tracing-in-message-security"></a><span data-ttu-id="16559-102">Rastreamento de atividades em segurança de mensagens</span><span class="sxs-lookup"><span data-stu-id="16559-102">Activity Tracing in Message Security</span></span>
<span data-ttu-id="16559-103">Este tópico descreve o rastreamento de atividades para o processamento de segurança, o que acontece no seguinte três fases.</span><span class="sxs-lookup"><span data-stu-id="16559-103">This topic describes activity tracing for security processing, which happens in the following three phases.</span></span>  
  
-   <span data-ttu-id="16559-104">Troca de negociação/SCT.</span><span class="sxs-lookup"><span data-stu-id="16559-104">Negotiation/SCT exchange.</span></span> <span data-ttu-id="16559-105">Isso pode acontecer no transporte posteriormente (por meio de troca de dados binários) ou camada de mensagem (por meio de trocas de mensagens SOAP).</span><span class="sxs-lookup"><span data-stu-id="16559-105">This can happen at the transport later (through binary data exchange) or message layer (through SOAP message exchanges).</span></span>  
  
-   <span data-ttu-id="16559-106">Mensagem criptografia/descriptografia, com a autenticação e verificação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="16559-106">Message encryption/decryption, with signature verification and authentication.</span></span> <span data-ttu-id="16559-107">Rastreamentos aparecem na atividade de ambiente, normalmente "ação de processo".</span><span class="sxs-lookup"><span data-stu-id="16559-107">Traces appear in the ambient activity, typically "Process Action."</span></span>  
  
-   <span data-ttu-id="16559-108">Autorização e verificação.</span><span class="sxs-lookup"><span data-stu-id="16559-108">Authorization and verification.</span></span> <span data-ttu-id="16559-109">Isso pode acontecer localmente ou quando a comunicação entre pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="16559-109">This can happen locally or when communicating between endpoints.</span></span>  
  
## <a name="negotiationsct-exchange"></a><span data-ttu-id="16559-110">Troca de negociação/SCT</span><span class="sxs-lookup"><span data-stu-id="16559-110">Negotiation/SCT exchange</span></span>  
 <span data-ttu-id="16559-111">Na fase de troca de negociação/SCT, são criados dois tipos de atividade no cliente: "Definir a sessão segura" e "Fechar sessão segura".</span><span class="sxs-lookup"><span data-stu-id="16559-111">In the negotiation/SCT exchange phase, two activity types are created on the client: "Set up Secure Session" and "Close Secure Session."</span></span> <span data-ttu-id="16559-112">"Configurar sessão segura" abrange rastreamentos de trocas de mensagens a primeira/RSTR/SCT, enquanto "Fechar sessão segura" inclui rastreamentos da mensagem de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="16559-112">"Set up Secure Session" encompasses traces for the RST/RSTR/SCT message exchanges, while "Close Secure Session" includes traces for the Cancel message.</span></span>  
  
 <span data-ttu-id="16559-113">No servidor, cada solicitação/resposta para a primeira/RSTR/SCT aparece em sua própria atividade.</span><span class="sxs-lookup"><span data-stu-id="16559-113">On the server, each request/reply for the RST/RSTR/SCT appears in its own activity.</span></span> <span data-ttu-id="16559-114">Se `propagateActivity` = `true` no servidor e para cliente, atividades no servidor têm a mesma ID e aparecem juntos na "instalação seguro sessão" quando visualizado no Visualizador de rastreamento de serviço.</span><span class="sxs-lookup"><span data-stu-id="16559-114">If `propagateActivity`=`true` on both the server and client, activities on the server have the same ID, and appear together in the "Setup Secure Session" when viewed through Service Trace Viewer.</span></span>  
  
 <span data-ttu-id="16559-115">Esse modelo de rastreamento de atividade é válido para a autenticação NTLM, autenticação de certificado e autenticação de senha/nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="16559-115">This activity tracing model is valid for user name/password authentication, certificate authentication, and NTLM authentication.</span></span>  
  
 <span data-ttu-id="16559-116">A tabela a seguir lista as atividades e rastreamentos para negociação e exchange SCT.</span><span class="sxs-lookup"><span data-stu-id="16559-116">The following table lists the activities and traces for negotiation and SCT exchange.</span></span>  
  
||<span data-ttu-id="16559-117">Ocorre quando a negociação/SCT trocar de tempo</span><span class="sxs-lookup"><span data-stu-id="16559-117">Time when Negotiation/SCT exchange happens</span></span>|<span data-ttu-id="16559-118">Atividades</span><span class="sxs-lookup"><span data-stu-id="16559-118">Activities</span></span>|<span data-ttu-id="16559-119">rastreamentos</span><span class="sxs-lookup"><span data-stu-id="16559-119">Traces</span></span>|  
|-|-------------------------------------------------|----------------|------------|  
|<span data-ttu-id="16559-120">Transporte seguro</span><span class="sxs-lookup"><span data-stu-id="16559-120">Secure Transport</span></span><br /><br /> <span data-ttu-id="16559-121">SSL (HTTPS)</span><span class="sxs-lookup"><span data-stu-id="16559-121">(HTTPS, SSL)</span></span>|<span data-ttu-id="16559-122">Na primeira mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="16559-122">On first message received.</span></span>|<span data-ttu-id="16559-123">Rastreamentos são emitidos na atividade de ambiente.</span><span class="sxs-lookup"><span data-stu-id="16559-123">Traces are emitted in the ambient activity.</span></span>|<span data-ttu-id="16559-124">-Exchange rastreamentos</span><span class="sxs-lookup"><span data-stu-id="16559-124">-   Exchange traces</span></span><br /><span data-ttu-id="16559-125">-Proteger o canal estabelecido</span><span class="sxs-lookup"><span data-stu-id="16559-125">-   Secure channel established</span></span><br /><span data-ttu-id="16559-126">-Compartilhamento segredos obtidos.</span><span class="sxs-lookup"><span data-stu-id="16559-126">-   Share secrets obtained.</span></span>|  
|<span data-ttu-id="16559-127">Camada de mensagem segura</span><span class="sxs-lookup"><span data-stu-id="16559-127">Secure Message Layer</span></span><br /><br /> <span data-ttu-id="16559-128">(WSHTTP)</span><span class="sxs-lookup"><span data-stu-id="16559-128">(WSHTTP)</span></span>|<span data-ttu-id="16559-129">Na primeira mensagem recebida.</span><span class="sxs-lookup"><span data-stu-id="16559-129">On first message received.</span></span>|<span data-ttu-id="16559-130">No cliente:</span><span class="sxs-lookup"><span data-stu-id="16559-130">On the client:</span></span><br /><br /> <span data-ttu-id="16559-131">-"Instalação sessão segura" fora de processo "ação" da primeira mensagem, para cada solicitação/resposta para a primeira/RSTR/SCT.</span><span class="sxs-lookup"><span data-stu-id="16559-131">-   "Setup Secure Session" out of "Process Action" of that first message, for each request/reply for RST/RSTR/SCT.</span></span><br /><span data-ttu-id="16559-132">-"Fechar a sessão segura" para a troca de cancelamento, fora de "atividade Proxy fechar".</span><span class="sxs-lookup"><span data-stu-id="16559-132">-   "Close Secure Session" for the CANCEL exchange, out of the "Close Proxy activity."</span></span> <span data-ttu-id="16559-133">Essa atividade pode acontecer fora de algumas outras atividades ambiente, dependendo de quando a sessão segura está fechada.</span><span class="sxs-lookup"><span data-stu-id="16559-133">This activity may happen out of some other ambient activity, depending on when the secure session is closed.</span></span><br /><br /> <span data-ttu-id="16559-134">No servidor:</span><span class="sxs-lookup"><span data-stu-id="16559-134">On the server:</span></span><br /><br /> <span data-ttu-id="16559-135">-Uma atividade de "Processo ação" para cada solicitação/resposta para a primeira/SCT/Cancelar no servidor.</span><span class="sxs-lookup"><span data-stu-id="16559-135">-   One "Process Action" activity for each request/reply for RST/SCT/Cancel on the server.</span></span> <span data-ttu-id="16559-136">Se `propagateActivity` = `true`, atividades RSTR/primeira/SCT são mescladas com "Definir a sessão de segurança" e Cancelar é mesclada com a atividade "Fechar" do cliente.</span><span class="sxs-lookup"><span data-stu-id="16559-136">If `propagateActivity`=`true`, RST/RSTR/SCT activities are merged with "Set up Security Session", and Cancel is merged with the "Close" activity from the client.</span></span><br /><br /> <span data-ttu-id="16559-137">Há duas etapas para "Definir a sessão segura":</span><span class="sxs-lookup"><span data-stu-id="16559-137">There are two stages for "Set up Secure Session":</span></span><br /><br /> <span data-ttu-id="16559-138">1.  Negociação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="16559-138">1.  Authentication negotiation.</span></span> <span data-ttu-id="16559-139">Isso é opcional se o cliente já tiver as credenciais apropriadas.</span><span class="sxs-lookup"><span data-stu-id="16559-139">This is optional if the client already has the proper credentials.</span></span> <span data-ttu-id="16559-140">Essa fase pode ser feita por meio do transporte seguro, ou as trocas de mensagens.</span><span class="sxs-lookup"><span data-stu-id="16559-140">This phase can be done through secure transport, or through message exchanges.</span></span> <span data-ttu-id="16559-141">No último caso, 1 ou 2 trocas de primeira/RSTR podem acontecer.</span><span class="sxs-lookup"><span data-stu-id="16559-141">In the latter case, 1 or 2 RST/RSTR exchanges can happen.</span></span> <span data-ttu-id="16559-142">Essas trocas, os rastreamentos são emitidos em novas atividades de solicitação/resposta criadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="16559-142">For these exchanges, traces are emitted in new request/reply activities as previously designed.</span></span><br /><span data-ttu-id="16559-143">2.  Proteger o estabelecimento da sessão SCT (), no qual uma troca de primeira/RSTR acontece aqui.</span><span class="sxs-lookup"><span data-stu-id="16559-143">2.  Secure session establishment (SCT), in which one RST/RSTR exchange happens here.</span></span> <span data-ttu-id="16559-144">Isso tem as mesmas atividades de ambiente, conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="16559-144">This has the same ambient activities as described previously.</span></span>|<span data-ttu-id="16559-145">-Exchange rastreamentos</span><span class="sxs-lookup"><span data-stu-id="16559-145">-   Exchange traces</span></span><br /><span data-ttu-id="16559-146">-Proteger o canal estabelecido</span><span class="sxs-lookup"><span data-stu-id="16559-146">-   Secure channel established</span></span><br /><span data-ttu-id="16559-147">-Compartilhamento segredos obtidos.</span><span class="sxs-lookup"><span data-stu-id="16559-147">-   Share secrets obtained.</span></span>|  
  
> [!NOTE]
>  <span data-ttu-id="16559-148">No modo de segurança misto, autenticação de negociação ocorre em trocas de binárias, mas SCT acontece na troca de mensagens.</span><span class="sxs-lookup"><span data-stu-id="16559-148">In mixed security mode, negotiation authentication happens in binary exchanges, but SCT happens in message exchange.</span></span> <span data-ttu-id="16559-149">No modo de transporte puro, negociação ocorre apenas no transporte sem atividades adicionais.</span><span class="sxs-lookup"><span data-stu-id="16559-149">In pure transport mode, negotiation happens only in transport with no additional activities.</span></span>  
  
## <a name="message-encryption-and-decryption"></a><span data-ttu-id="16559-150">Descriptografia e criptografia de mensagens</span><span class="sxs-lookup"><span data-stu-id="16559-150">Message Encryption and Decryption</span></span>  
 <span data-ttu-id="16559-151">A tabela a seguir lista as atividades e rastreamentos de criptografia/descriptografia de mensagem, bem como autenticação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="16559-151">The following table lists the activities and traces for message encryption/decryption, as well as signature authentication.</span></span>  
  
||<span data-ttu-id="16559-152">Transporte seguro</span><span class="sxs-lookup"><span data-stu-id="16559-152">Secure Transport</span></span><br /><br /> <span data-ttu-id="16559-153">(HTTPS, SSL) e a camada de mensagem de segurança</span><span class="sxs-lookup"><span data-stu-id="16559-153">(HTTPS, SSL) and Secure Message Layer</span></span><br /><br /> <span data-ttu-id="16559-154">(WSHTTP)</span><span class="sxs-lookup"><span data-stu-id="16559-154">(WSHTTP)</span></span>|  
|-|---------------------------------------------------------------------------------|  
|<span data-ttu-id="16559-155">Hora em que mensagem criptografia/descriptografia, bem como autenticação de assinatura acontece</span><span class="sxs-lookup"><span data-stu-id="16559-155">Time when message encryption/decryption, as well as signature authentication happens</span></span>|<span data-ttu-id="16559-156">Na mensagem recebida</span><span class="sxs-lookup"><span data-stu-id="16559-156">On message received</span></span>|  
|<span data-ttu-id="16559-157">Atividades</span><span class="sxs-lookup"><span data-stu-id="16559-157">Activities</span></span>|<span data-ttu-id="16559-158">Rastreamentos são emitidos na atividade de ProcessAction no cliente e no servidor.</span><span class="sxs-lookup"><span data-stu-id="16559-158">Traces are emitted in the ProcessAction activity on the client and server.</span></span>|  
|<span data-ttu-id="16559-159">rastreamentos</span><span class="sxs-lookup"><span data-stu-id="16559-159">Traces</span></span>|<span data-ttu-id="16559-160">-sendSecurityHeader (remetente):</span><span class="sxs-lookup"><span data-stu-id="16559-160">-   sendSecurityHeader (sender):</span></span><br /><span data-ttu-id="16559-161">-Mensagem de entrada</span><span class="sxs-lookup"><span data-stu-id="16559-161">-   Sign message</span></span><br /><span data-ttu-id="16559-162">-Criptografar dados de solicitação</span><span class="sxs-lookup"><span data-stu-id="16559-162">-   Encrypt request data</span></span><br /><span data-ttu-id="16559-163">-receiveSecurityHeader (destinatário):</span><span class="sxs-lookup"><span data-stu-id="16559-163">-   receiveSecurityHeader (receiver):</span></span><br /><span data-ttu-id="16559-164">-Verificar a assinatura</span><span class="sxs-lookup"><span data-stu-id="16559-164">-   Verify signature</span></span><br /><span data-ttu-id="16559-165">-Descriptografar dados de resposta</span><span class="sxs-lookup"><span data-stu-id="16559-165">-   Decrypt response data</span></span><br /><span data-ttu-id="16559-166">-Autenticação</span><span class="sxs-lookup"><span data-stu-id="16559-166">-   Authentication</span></span>|  
  
> [!NOTE]
>  <span data-ttu-id="16559-167">No modo de transporte puro, mensagem de criptografia/descriptografia ocorre apenas no transporte sem atividades adicionais.</span><span class="sxs-lookup"><span data-stu-id="16559-167">In pure transport mode, message encryption/decryption happens only in transport with no additional activities.</span></span>  
  
## <a name="authorization-and-verification"></a><span data-ttu-id="16559-168">Autorização e verificação</span><span class="sxs-lookup"><span data-stu-id="16559-168">Authorization and Verification</span></span>  
 <span data-ttu-id="16559-169">A tabela a seguir lista as atividades e rastreamentos para autorização.</span><span class="sxs-lookup"><span data-stu-id="16559-169">The following table lists the activities and traces for authorization.</span></span>  
  
||<span data-ttu-id="16559-170">Quando ocorre a autorização do tempo</span><span class="sxs-lookup"><span data-stu-id="16559-170">Time when authorization happens</span></span>|<span data-ttu-id="16559-171">Atividades</span><span class="sxs-lookup"><span data-stu-id="16559-171">Activities</span></span>|<span data-ttu-id="16559-172">rastreamentos</span><span class="sxs-lookup"><span data-stu-id="16559-172">Traces</span></span>|  
|-|-------------------------------------|----------------|------------|  
|<span data-ttu-id="16559-173">Local (padrão)</span><span class="sxs-lookup"><span data-stu-id="16559-173">Local (default)</span></span>|<span data-ttu-id="16559-174">Depois que a mensagem é descriptografada no servidor</span><span class="sxs-lookup"><span data-stu-id="16559-174">After the message is decrypted on the server</span></span>|<span data-ttu-id="16559-175">Rastreamentos são emitidos na atividade de ProcessAction no servidor.</span><span class="sxs-lookup"><span data-stu-id="16559-175">Traces are emitted in the ProcessAction activity at the server.</span></span>|<span data-ttu-id="16559-176">Usuário autorizado.</span><span class="sxs-lookup"><span data-stu-id="16559-176">User authorized.</span></span>|  
|<span data-ttu-id="16559-177">Remoto</span><span class="sxs-lookup"><span data-stu-id="16559-177">Remote</span></span>|<span data-ttu-id="16559-178">Depois que a mensagem é descriptografada no servidor</span><span class="sxs-lookup"><span data-stu-id="16559-178">After the message is decrypted on the server</span></span>|<span data-ttu-id="16559-179">Rastreamentos são emitidos em uma nova atividade invocada pela atividade ProcessAction.</span><span class="sxs-lookup"><span data-stu-id="16559-179">Traces are emitted in a new activity invoked by the ProcessAction activity.</span></span>|<span data-ttu-id="16559-180">Usuário autorizado.</span><span class="sxs-lookup"><span data-stu-id="16559-180">User authorized.</span></span>|