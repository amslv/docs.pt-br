---
title: "Como definir o modo de segurança"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Mode property
- WCF, security mode
- WCF, security
ms.assetid: 6e01dd9f-b5dd-4474-b24c-06e124de4ff7
caps.latest.revision: "22"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.openlocfilehash: 595999bfa7d3472fc31274a0c9652af5416d2da5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-set-the-security-mode"></a><span data-ttu-id="377ef-102">Como definir o modo de segurança</span><span class="sxs-lookup"><span data-stu-id="377ef-102">How to: Set the Security Mode</span></span>
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)]<span data-ttu-id="377ef-103">a segurança tem três modos de segurança comuns encontrados em associações mais predefinidas: transporte, mensagem e "transporte com credencial de mensagem".</span><span class="sxs-lookup"><span data-stu-id="377ef-103"> security has three common security modes that are found on most predefined bindings: transport, message, and "transport with message credential."</span></span> <span data-ttu-id="377ef-104">Dois modos adicionais são específicos para duas ligações: o modo "somente credencial transporte" encontrado na <xref:System.ServiceModel.BasicHttpBinding>e o "Dois", encontrado na <xref:System.ServiceModel.NetMsmqBinding>.</span><span class="sxs-lookup"><span data-stu-id="377ef-104">Two additional modes are specific to two bindings: the "transport-credential only" mode found on the <xref:System.ServiceModel.BasicHttpBinding>, and the "Both" mode, found on the <xref:System.ServiceModel.NetMsmqBinding>.</span></span> <span data-ttu-id="377ef-105">No entanto, neste tópico se concentra em três modos de segurança comuns: <xref:System.ServiceModel.SecurityMode.Transport>, <xref:System.ServiceModel.SecurityMode.Message>, e <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>.</span><span class="sxs-lookup"><span data-stu-id="377ef-105">However, this topic concentrates on the three common security modes: <xref:System.ServiceModel.SecurityMode.Transport>, <xref:System.ServiceModel.SecurityMode.Message>, and <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>.</span></span>  
  
 <span data-ttu-id="377ef-106">Observe que nem todos predefinida associação oferece suporte a todos os modos.</span><span class="sxs-lookup"><span data-stu-id="377ef-106">Note that not every predefined binding supports all of these modes.</span></span> <span data-ttu-id="377ef-107">Este tópico define o modo com o <xref:System.ServiceModel.WSHttpBinding> e <xref:System.ServiceModel.NetTcpBinding> classes e demonstra como definir o modo de forma programática e por meio da configuração.</span><span class="sxs-lookup"><span data-stu-id="377ef-107">This topic sets the mode with the <xref:System.ServiceModel.WSHttpBinding> and <xref:System.ServiceModel.NetTcpBinding> classes and demonstrates how to set the mode both programmatically and through configuration.</span></span>  
  
 [!INCLUDE[crabout](../../../includes/crdefault-md.md)]<span data-ttu-id="377ef-108">[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] segurança, consulte [visão geral de segurança](../../../docs/framework/wcf/feature-details/security-overview.md), [protegendo serviços](../../../docs/framework/wcf/securing-services.md), e [protegendo serviços e clientes](../../../docs/framework/wcf/feature-details/securing-services-and-clients.md).</span><span class="sxs-lookup"><span data-stu-id="377ef-108"> [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] security, see [Security Overview](../../../docs/framework/wcf/feature-details/security-overview.md), [Securing Services](../../../docs/framework/wcf/securing-services.md), and [Securing Services and Clients](../../../docs/framework/wcf/feature-details/securing-services-and-clients.md).</span></span> [!INCLUDE[crabout](../../../includes/crabout-md.md)]<span data-ttu-id="377ef-109">modo e a mensagem de transporte, consulte [segurança de transporte](../../../docs/framework/wcf/feature-details/transport-security.md) e [segurança de mensagem](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="377ef-109"> transport mode and message, see [Transport Security](../../../docs/framework/wcf/feature-details/transport-security.md) and [Message Security](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md).</span></span>  
  
### <a name="to-set-the-security-mode-in-code"></a><span data-ttu-id="377ef-110">Para definir o modo de segurança no código</span><span class="sxs-lookup"><span data-stu-id="377ef-110">To set the security mode in code</span></span>  
  
1.  <span data-ttu-id="377ef-111">Crie uma instância da classe de associação que você está usando.</span><span class="sxs-lookup"><span data-stu-id="377ef-111">Create an instance of the binding class that you are using.</span></span> <span data-ttu-id="377ef-112">Para obter uma lista de associações predefinidas, consulte [System-Provided associações](../../../docs/framework/wcf/system-provided-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="377ef-112">For a list of predefined bindings, see [System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md).</span></span> <span data-ttu-id="377ef-113">Este exemplo cria uma instância do <xref:System.ServiceModel.WSHttpBinding> classe.</span><span class="sxs-lookup"><span data-stu-id="377ef-113">This example creates an instance of the <xref:System.ServiceModel.WSHttpBinding> class.</span></span>  
  
2.  <span data-ttu-id="377ef-114">Definir o `Mode` propriedade do objeto retornado pelo `Security` propriedade.</span><span class="sxs-lookup"><span data-stu-id="377ef-114">Set the `Mode` property of the object returned by the `Security` property.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#1)]
     [!code-vb[c_SettingSecurityMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#1)]  
  
     <span data-ttu-id="377ef-115">Como alternativa, defina o modo de mensagem, conforme mostrado no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="377ef-115">Alternatively, set the mode to message, as shown in the following code.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#2)]
     [!code-vb[c_SettingSecurityMode#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#2)]  
  
     <span data-ttu-id="377ef-116">Ou defina o modo de transporte com as credenciais de mensagem, conforme mostrado no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="377ef-116">Or set the mode to transport with message credentials, as shown in the following code.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#3)]
     [!code-vb[c_SettingSecurityMode#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#3)]  
  
3.  <span data-ttu-id="377ef-117">Você também pode definir o modo no construtor da associação, conforme mostrado no código a seguir.</span><span class="sxs-lookup"><span data-stu-id="377ef-117">You can also set the mode in the constructor of the binding, as shown in the following code.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#4)]
     [!code-vb[c_SettingSecurityMode#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#4)]  
  
## <a name="setting-the-clientcredentialtype-property"></a><span data-ttu-id="377ef-118">Definindo a propriedade ClientCredentialType</span><span class="sxs-lookup"><span data-stu-id="377ef-118">Setting the ClientCredentialType Property</span></span>  
 <span data-ttu-id="377ef-119">Definir o modo como um dos três valores determina como você definir o `ClientCredentialType` propriedade.</span><span class="sxs-lookup"><span data-stu-id="377ef-119">Setting the mode to one of the three values determines how you set the `ClientCredentialType` property.</span></span> <span data-ttu-id="377ef-120">Por exemplo, usando o <xref:System.ServiceModel.WSHttpBinding> classe, definindo o modo como `Transport` significa que você deve definir o <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> propriedade o <xref:System.ServiceModel.HttpTransportSecurity> classe para um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="377ef-120">For example, using the <xref:System.ServiceModel.WSHttpBinding> class, setting the mode to `Transport` means you must set the <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> property of the <xref:System.ServiceModel.HttpTransportSecurity> class to an appropriate value.</span></span>  
  
#### <a name="to-set-the-clientcredentialtype-property-for-transport-mode"></a><span data-ttu-id="377ef-121">Para definir a propriedade ClientCredentialType para o modo de transporte</span><span class="sxs-lookup"><span data-stu-id="377ef-121">To set the ClientCredentialType property for Transport mode</span></span>  
  
1.  <span data-ttu-id="377ef-122">Crie uma instância da associação.</span><span class="sxs-lookup"><span data-stu-id="377ef-122">Create an instance of the binding.</span></span>  
  
2.  <span data-ttu-id="377ef-123">Defina a propriedade `Mode` como `Transport`.</span><span class="sxs-lookup"><span data-stu-id="377ef-123">Set the `Mode` property to `Transport`.</span></span>  
  
3.  <span data-ttu-id="377ef-124">Definir o `ClientCredential` propriedade para um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="377ef-124">Set the `ClientCredential` property to an appropriate value.</span></span> <span data-ttu-id="377ef-125">O código a seguir define a propriedade como `Windows`.</span><span class="sxs-lookup"><span data-stu-id="377ef-125">The following code sets the property to `Windows`.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#5)]
     [!code-vb[c_SettingSecurityMode#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#5)]  
  
#### <a name="to-set-the-clientcredentialtype-property-for-message-mode"></a><span data-ttu-id="377ef-126">Para definir a propriedade ClientCredentialType para o modo de mensagem</span><span class="sxs-lookup"><span data-stu-id="377ef-126">To set the ClientCredentialType property for Message mode</span></span>  
  
1.  <span data-ttu-id="377ef-127">Crie uma instância da associação.</span><span class="sxs-lookup"><span data-stu-id="377ef-127">Create an instance of the binding.</span></span>  
  
2.  <span data-ttu-id="377ef-128">Defina a propriedade `Mode` como `Message`.</span><span class="sxs-lookup"><span data-stu-id="377ef-128">Set the `Mode` property to `Message`.</span></span>  
  
3.  <span data-ttu-id="377ef-129">Definir o `ClientCredential` propriedade para um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="377ef-129">Set the `ClientCredential` property to an appropriate value.</span></span> <span data-ttu-id="377ef-130">O código a seguir define a propriedade como `Certificate`.</span><span class="sxs-lookup"><span data-stu-id="377ef-130">The following code sets the property to `Certificate`.</span></span>  
  
     [!code-csharp[c_SettingSecurityMode#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#6)]
     [!code-vb[c_SettingSecurityMode#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#6)]  
  
#### <a name="to-set-the-mode-and-clientcredentialtype-property-in-configuration"></a><span data-ttu-id="377ef-131">Para definir a propriedade de modo e ClientCredentialType na configuração</span><span class="sxs-lookup"><span data-stu-id="377ef-131">To set the Mode and ClientCredentialType property in configuration</span></span>  
  
1.  <span data-ttu-id="377ef-132">Adicionar um elemento de associação apropriado para o [ \<associações >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) elemento do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="377ef-132">Add an appropriate binding element to the [\<bindings>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) element of the configuration file.</span></span> <span data-ttu-id="377ef-133">O exemplo a seguir adiciona uma [ \<wsHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) elemento.</span><span class="sxs-lookup"><span data-stu-id="377ef-133">The following example adds a [\<wsHttpBinding>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) element.</span></span>  
  
2.  <span data-ttu-id="377ef-134">Adicionar um `<binding>` elemento e defina seu `name` de atributo para um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="377ef-134">Add a `<binding>` element and set its `name` attribute to an appropriate value.</span></span>  
  
3.  <span data-ttu-id="377ef-135">Adicionar um `<security>` elemento e defina o `mode` atributo `Message`, `Transport`, ou `TransportWithMessageCredential`.</span><span class="sxs-lookup"><span data-stu-id="377ef-135">Add a `<security>` element and set the `mode` attribute to `Message`, `Transport`, or `TransportWithMessageCredential`.</span></span>  
  
4.  <span data-ttu-id="377ef-136">Se o modo é definido como `Transport`, adicione um `<transport>` elemento e defina o `clientCredential` de atributo para um valor apropriado.</span><span class="sxs-lookup"><span data-stu-id="377ef-136">If the mode is set to `Transport`, add a `<transport>` element and set the `clientCredential` attribute to an appropriate value.</span></span>  
  
     <span data-ttu-id="377ef-137">O exemplo a seguir define o modo como "`Transport"`e, em seguida, define o `clientCredentialType` atributo do `<transport>` elemento"`Windows"`.</span><span class="sxs-lookup"><span data-stu-id="377ef-137">The following example sets the mode to "`Transport"`, and then sets the `clientCredentialType` attribute of the `<transport>` element to "`Windows"`.</span></span>  
  
    ```xml  
    <wsHttpBinding>  
    <binding name="TransportSecurity">  
        <security mode="Transport" />  
           <transport clientCredentialType = "Windows" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     <span data-ttu-id="377ef-138">Como alternativa, defina o `security mode` para "`Message"`, seguido por um `<"message">` elemento.</span><span class="sxs-lookup"><span data-stu-id="377ef-138">Alternatively, set the `security mode` to "`Message"`, followed by a `<"message">` element.</span></span> <span data-ttu-id="377ef-139">Este exemplo define o `clientCredentialType` para "`Certificate"`.</span><span class="sxs-lookup"><span data-stu-id="377ef-139">This example sets the `clientCredentialType` to "`Certificate"`.</span></span>  
  
    ```xml  
    <wsHttpBinding>  
    <binding name="MessageSecurity">  
        <security mode="Message" />  
           <message clientCredentialType = "Certificate" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     <span data-ttu-id="377ef-140">Usando o <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential> valor é um caso especial e é explicado abaixo.</span><span class="sxs-lookup"><span data-stu-id="377ef-140">Using the <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential> value is a special case, and is explained below.</span></span>  
  
### <a name="using-transportwithmessagecredential"></a><span data-ttu-id="377ef-141">Usando TransportWithMessageCredential</span><span class="sxs-lookup"><span data-stu-id="377ef-141">Using TransportWithMessageCredential</span></span>  
 <span data-ttu-id="377ef-142">Ao definir o modo de segurança para `TransportWithMessageCredential`, o transporte determina o mecanismo real que fornece a segurança no nível de transporte.</span><span class="sxs-lookup"><span data-stu-id="377ef-142">When setting the security mode to `TransportWithMessageCredential`, the transport determines the actual mechanism that provides the transport-level security.</span></span> <span data-ttu-id="377ef-143">Por exemplo, o protocolo HTTP usa o protocolo (SSL) sobre HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="377ef-143">For example, the HTTP protocol uses Secure Sockets Layer (SSL) over HTTP (HTTPS).</span></span> <span data-ttu-id="377ef-144">Portanto, definir o `ClientCredentialType` propriedade de qualquer objeto de segurança de transporte (como <xref:System.ServiceModel.HttpTransportSecurity>) será ignorado.</span><span class="sxs-lookup"><span data-stu-id="377ef-144">Therefore, setting the `ClientCredentialType` property of any transport security object (such as <xref:System.ServiceModel.HttpTransportSecurity>) is ignored.</span></span>  <span data-ttu-id="377ef-145">Em outras palavras, você só pode definir o `ClientCredentialType` do objeto de segurança de mensagem (para o `WSHttpBinding` de associação, o <xref:System.ServiceModel.NonDualMessageSecurityOverHttp> objeto).</span><span class="sxs-lookup"><span data-stu-id="377ef-145">In other words, you can only set the `ClientCredentialType` of the message security object (for the `WSHttpBinding` binding, the <xref:System.ServiceModel.NonDualMessageSecurityOverHttp> object).</span></span>  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<span data-ttu-id="377ef-146">[Como: usar a segurança de transporte e as credenciais de mensagem](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="377ef-146"> [How to: Use Transport Security and Message Credentials](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="377ef-147">Consulte também</span><span class="sxs-lookup"><span data-stu-id="377ef-147">See Also</span></span>  
 [<span data-ttu-id="377ef-148">Como: configurar uma porta com um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="377ef-148">How to: Configure a Port with an SSL Certificate</span></span>](../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)  
 [<span data-ttu-id="377ef-149">Como: usar a segurança de transporte e as credenciais de mensagem</span><span class="sxs-lookup"><span data-stu-id="377ef-149">How to: Use Transport Security and Message Credentials</span></span>](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)  
 [<span data-ttu-id="377ef-150">Segurança de transporte</span><span class="sxs-lookup"><span data-stu-id="377ef-150">Transport Security</span></span>](../../../docs/framework/wcf/feature-details/transport-security.md)  
 [<span data-ttu-id="377ef-151">Segurança de mensagem</span><span class="sxs-lookup"><span data-stu-id="377ef-151">Message Security</span></span>](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)  
 [<span data-ttu-id="377ef-152">Visão geral de segurança</span><span class="sxs-lookup"><span data-stu-id="377ef-152">Security Overview</span></span>](../../../docs/framework/wcf/feature-details/security-overview.md)  
 <span data-ttu-id="377ef-153">[System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md) (Associações fornecidas pelo sistema)</span><span class="sxs-lookup"><span data-stu-id="377ef-153">[System-Provided Bindings](../../../docs/framework/wcf/system-provided-bindings.md)</span></span>  
 [<span data-ttu-id="377ef-154">\<segurança ></span><span class="sxs-lookup"><span data-stu-id="377ef-154">\<security></span></span>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)  
 [<span data-ttu-id="377ef-155">\<segurança ></span><span class="sxs-lookup"><span data-stu-id="377ef-155">\<security></span></span>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)  
 [<span data-ttu-id="377ef-156">\<segurança ></span><span class="sxs-lookup"><span data-stu-id="377ef-156">\<security></span></span>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)