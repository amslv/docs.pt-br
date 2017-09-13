---
title: Derivando de WebResponse
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Deriving from WebResponse
ms.assetid: f11d4866-a199-4087-9306-a5a4c18b13db
caps.latest.revision: 7
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 627e5170dbf33b9b42ec7e46e77e6ff2fa874463
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="deriving-from-webresponse"></a><span data-ttu-id="da33a-102">Derivando de WebResponse</span><span class="sxs-lookup"><span data-stu-id="da33a-102">Deriving from WebResponse</span></span>
<span data-ttu-id="da33a-103">A classe <xref:System.Net.WebResponse> é uma classe base abstrata que fornece os métodos e as propriedades básicas para criar uma resposta específica ao protocolo que se ajusta ao modelo de protocolo conectável do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="da33a-103">The <xref:System.Net.WebResponse> class is an abstract base class that provides the basic methods and properties for creating a protocol-specific response that fits the .NET Framework pluggable protocol model.</span></span> <span data-ttu-id="da33a-104">Os aplicativos que usam a classe <xref:System.Net.WebRequest> para solicitar dados de recursos recebem as respostas em uma **WebResponse**.</span><span class="sxs-lookup"><span data-stu-id="da33a-104">Applications that use the <xref:System.Net.WebRequest> class to request data from resources receive the responses in a **WebResponse**.</span></span> <span data-ttu-id="da33a-105">Os descendentes de **WebResponse** específicos ao protocolo devem implementar os membros abstratos da classe **WebResponse**.</span><span class="sxs-lookup"><span data-stu-id="da33a-105">Protocol-specific **WebResponse** descendants must implement the abstract members of the **WebResponse** class.</span></span>  
  
 <span data-ttu-id="da33a-106">A classe **WebRequest** associada deve criar descendentes de **WebResponse**.</span><span class="sxs-lookup"><span data-stu-id="da33a-106">The associated **WebRequest** class must create **WebResponse** descendants.</span></span> <span data-ttu-id="da33a-107">Por exemplo, as instâncias <xref:System.Net.HttpWebResponse> são criadas apenas como o resultado da chamada a <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=fullName> ou <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="da33a-107">For example, <xref:System.Net.HttpWebResponse> instances are created only as the result of calling <xref:System.Net.HttpWebRequest.GetResponse%2A?displayProperty=fullName> or <xref:System.Net.HttpWebRequest.EndGetResponse%2A?displayProperty=fullName>.</span></span> <span data-ttu-id="da33a-108">Cada **WebResponse** contém o resultado de uma solicitação para um recurso e não se destina a ser reutilizada.</span><span class="sxs-lookup"><span data-stu-id="da33a-108">Each **WebResponse** contains the result of a request to a resource and is not intended to be reused.</span></span>  
  
## <a name="contentlength-property"></a><span data-ttu-id="da33a-109">Propriedade ContentLength</span><span class="sxs-lookup"><span data-stu-id="da33a-109">ContentLength Property</span></span>  
 <span data-ttu-id="da33a-110">A propriedade <xref:System.Net.WebResponse.ContentLength%2A> indica o número de bytes de dados disponíveis no fluxo retornado pelo método <xref:System.Net.WebResponse.GetResponseStream%2A>.</span><span class="sxs-lookup"><span data-stu-id="da33a-110">The <xref:System.Net.WebResponse.ContentLength%2A> property indicates the number of bytes of data that are available from the stream returned by the <xref:System.Net.WebResponse.GetResponseStream%2A> method.</span></span> <span data-ttu-id="da33a-111">A propriedade **ContentLength** não indica o número de bytes de informações de cabeçalho ou de metadados retornados pelo servidor; indica somente o número de bytes de dados no próprio recurso solicitado.</span><span class="sxs-lookup"><span data-stu-id="da33a-111">The **ContentLength** property does not indicate the number of bytes of header or metadata information returned by the server; it indicates only the number of bytes of data in the requested resource itself.</span></span>  
  
## <a name="contenttype-property"></a><span data-ttu-id="da33a-112">Propriedade ContentType</span><span class="sxs-lookup"><span data-stu-id="da33a-112">ContentType Property</span></span>  
 <span data-ttu-id="da33a-113">A propriedade <xref:System.Net.WebResponse.ContentType%2A> fornece informações especiais que o protocolo exige que sejam enviadas ao cliente para identificar o tipo de conteúdo que está sendo enviado pelo servidor.</span><span class="sxs-lookup"><span data-stu-id="da33a-113">The <xref:System.Net.WebResponse.ContentType%2A> property provides any special information that your protocol requires you to send to the client to identify the type of content being sent by the server.</span></span> <span data-ttu-id="da33a-114">Normalmente, esse é o tipo de conteúdo MIME dos dados retornados.</span><span class="sxs-lookup"><span data-stu-id="da33a-114">Typically this is the MIME content type of any data returned.</span></span>  
  
## <a name="headers-property"></a><span data-ttu-id="da33a-115">Propriedade Headers</span><span class="sxs-lookup"><span data-stu-id="da33a-115">Headers Property</span></span>  
 <span data-ttu-id="da33a-116">A propriedade <xref:System.Net.WebResponse.Headers%2A> contém uma coleção arbitrária de pares de nome/valor de metadados associados à resposta.</span><span class="sxs-lookup"><span data-stu-id="da33a-116">The <xref:System.Net.WebResponse.Headers%2A> property contains an arbitrary collection of name/value pairs of metadata associated with the response.</span></span> <span data-ttu-id="da33a-117">Todos os metadados necessários para o protocolo que podem ser expressos como um par nome/valor podem ser incluídos na propriedade **Headers**.</span><span class="sxs-lookup"><span data-stu-id="da33a-117">Any metadata needed by the protocol that can be expressed as a name/value pair can be included in the **Headers** property.</span></span>  
  
 <span data-ttu-id="da33a-118">Não é necessário usar a propriedade **Headers** para usar os metadados do cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="da33a-118">You are not required to use the **Headers** property to use header metadata.</span></span> <span data-ttu-id="da33a-119">Os metadados específicos ao protocolo podem ser expostos como propriedades; por exemplo, a propriedade <xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=fullName> expõe o cabeçalho HTTP **Last-Modified**.</span><span class="sxs-lookup"><span data-stu-id="da33a-119">Protocol-specific metadata can be exposed as properties; for example, the <xref:System.Net.HttpWebResponse.LastModified%2A?displayProperty=fullName> property exposes the **Last-Modified** HTTP header.</span></span> <span data-ttu-id="da33a-120">Ao expor os metadados do cabeçalho como uma propriedade, você não deve permitir que a mesma propriedade seja definida usando a propriedade **Headers**.</span><span class="sxs-lookup"><span data-stu-id="da33a-120">When you expose header metadata as a property, you should not allow the same property to be set using the **Headers** property.</span></span>  
  
## <a name="responseuri-property"></a><span data-ttu-id="da33a-121">Propriedade ResponseUri</span><span class="sxs-lookup"><span data-stu-id="da33a-121">ResponseUri Property</span></span>  
 <span data-ttu-id="da33a-122">A propriedade <xref:System.Net.WebResponse.ResponseUri%2A> contém o URI do recurso que, de fato, forneceu a resposta.</span><span class="sxs-lookup"><span data-stu-id="da33a-122">The <xref:System.Net.WebResponse.ResponseUri%2A> property contains the URI of the resource that actually provided the response.</span></span> <span data-ttu-id="da33a-123">Para protocolos que não dão suporte ao redirecionamento, o **ResponseUri** será o mesmo que a propriedade <xref:System.Net.WebRequest.RequestUri%2A> da **WebRequest** que criou a resposta.</span><span class="sxs-lookup"><span data-stu-id="da33a-123">For protocols that do not support redirection, **ResponseUri** will be the same as the <xref:System.Net.WebRequest.RequestUri%2A> property of the **WebRequest** that created the response.</span></span> <span data-ttu-id="da33a-124">Se o protocolo der suporte ao redirecionamento da solicitação, o **ResponseUri** conterá o URI da resposta.</span><span class="sxs-lookup"><span data-stu-id="da33a-124">If the protocol supports redirecting the request, **ResponseUri** will contain the URI of the response.</span></span>  
  
## <a name="close-method"></a><span data-ttu-id="da33a-125">Método Close</span><span class="sxs-lookup"><span data-stu-id="da33a-125">Close Method</span></span>  
 <span data-ttu-id="da33a-126">O método <xref:System.Net.WebResponse.Close%2A> fecha todas as conexões feitas pela solicitação e pela resposta e limpa os recursos usados pela resposta.</span><span class="sxs-lookup"><span data-stu-id="da33a-126">The <xref:System.Net.WebResponse.Close%2A> method closes any connections made by the request and response and cleans up resources used by the response.</span></span> <span data-ttu-id="da33a-127">O método **Close** fecha todas as instâncias de fluxo usadas pela resposta, mas não gera uma exceção se o fluxo de resposta foi fechado anteriormente por uma chamada ao método <xref:System.IO.Stream.Close%2A?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="da33a-127">The **Close** method closes any stream instances used by the response, but it does not throw an exception if the response stream was previously closed by a call to the <xref:System.IO.Stream.Close%2A?displayProperty=fullName> method.</span></span>  
  
## <a name="getresponsestream-method"></a><span data-ttu-id="da33a-128">Método GetResponseStream</span><span class="sxs-lookup"><span data-stu-id="da33a-128">GetResponseStream Method</span></span>  
 <span data-ttu-id="da33a-129">O método <xref:System.Net.WebResponse.GetResponseStream%2A> retorna um fluxo que contém a resposta do recurso solicitado.</span><span class="sxs-lookup"><span data-stu-id="da33a-129">The <xref:System.Net.WebResponse.GetResponseStream%2A> method returns a stream containing the response from the requested resource.</span></span> <span data-ttu-id="da33a-130">O fluxo de resposta contém apenas os dados retornados pelo recurso; o cabeçalho ou os metadados incluídos na resposta devem ser removidos da resposta e expostos ao aplicativo por meio de propriedades específicas ao protocolo ou da propriedade **Headers**.</span><span class="sxs-lookup"><span data-stu-id="da33a-130">The response stream contains only the data returned by the resource; any header or metadata included in the response should be stripped from the response and exposed to the application through protocol-specific properties or the **Headers** property.</span></span>  
  
 <span data-ttu-id="da33a-131">A instância de fluxo retornada pelo método **GetResponseStream** pertence ao aplicativo e pode ser fechada sem fechar a **WebResponse**.</span><span class="sxs-lookup"><span data-stu-id="da33a-131">The stream instance returned by the **GetResponseStream** method is owned by the application and can be closed without closing the **WebResponse**.</span></span> <span data-ttu-id="da33a-132">Por convenção, uma chamada ao método **WebResponse.Close** também fecha o fluxo retornado por **GetResponse**.</span><span class="sxs-lookup"><span data-stu-id="da33a-132">By convention, calling the **WebResponse.Close** method also closes the stream returned by **GetResponse**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="da33a-133">Consulte também</span><span class="sxs-lookup"><span data-stu-id="da33a-133">See Also</span></span>  
 <span data-ttu-id="da33a-134"><xref:System.Net.WebResponse></span><span class="sxs-lookup"><span data-stu-id="da33a-134"><xref:System.Net.WebResponse></span></span>   
 <span data-ttu-id="da33a-135"><xref:System.Net.HttpWebResponse></span><span class="sxs-lookup"><span data-stu-id="da33a-135"><xref:System.Net.HttpWebResponse></span></span>   
 <span data-ttu-id="da33a-136"><xref:System.Net.FileWebResponse></span><span class="sxs-lookup"><span data-stu-id="da33a-136"><xref:System.Net.FileWebResponse></span></span>   
 <span data-ttu-id="da33a-137">[Programando protocolos conectáveis](../../../docs/framework/network-programming/programming-pluggable-protocols.md) </span><span class="sxs-lookup"><span data-stu-id="da33a-137">[Programming Pluggable Protocols](../../../docs/framework/network-programming/programming-pluggable-protocols.md) </span></span>  
 [<span data-ttu-id="da33a-138">Derivando de WebRequest</span><span class="sxs-lookup"><span data-stu-id="da33a-138">Deriving from WebRequest</span></span>](../../../docs/framework/network-programming/deriving-from-webrequest.md)
