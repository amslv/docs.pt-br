---
title: "Serviço de AJAX com exemplo de JSON e XML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
caps.latest.revision: "15"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: c0913a94f2fffd74890d7f996b2b103ed52f8d2f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="ajax-service-with-json-and-xml-sample"></a><span data-ttu-id="61c8b-102">Serviço de AJAX com exemplo de JSON e XML</span><span class="sxs-lookup"><span data-stu-id="61c8b-102">AJAX Service with JSON and XML Sample</span></span>
<span data-ttu-id="61c8b-103">Este exemplo demonstra como usar [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] para criar um serviço assíncrona AJAX JavaScript and XML () que retorna dados JSON JavaScript Object Notation () ou XML.</span><span class="sxs-lookup"><span data-stu-id="61c8b-103">This sample demonstrates how to use [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] to create an Asynchronous JavaScript and XML (AJAX) service that returns either JavaScript Object Notation (JSON) or XML data.</span></span> <span data-ttu-id="61c8b-104">Você pode acessar um serviço de AJAX usando código JavaScript de um cliente de navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="61c8b-104">You can access an AJAX service by using JavaScript code from a Web browser client.</span></span> <span data-ttu-id="61c8b-105">Este exemplo se baseia o [serviço AJAX básico](../../../../docs/framework/wcf/samples/basic-ajax-service.md) exemplo.</span><span class="sxs-lookup"><span data-stu-id="61c8b-105">This sample builds on the [Basic AJAX Service](../../../../docs/framework/wcf/samples/basic-ajax-service.md) sample.</span></span>  
  
 <span data-ttu-id="61c8b-106">Ao contrário de outros exemplos de AJAX, este exemplo não usa o ASP.NET AJAX e o <xref:System.Web.UI.ScriptManager> controle.</span><span class="sxs-lookup"><span data-stu-id="61c8b-106">Unlike the other AJAX samples, this sample does not use ASP.NET AJAX and the <xref:System.Web.UI.ScriptManager> control.</span></span> <span data-ttu-id="61c8b-107">Com alguma configuração adicional, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX serviços podem ser acessados de qualquer página HTML por meio de JavaScript, e esse cenário é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="61c8b-107">With some additional configuration, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX services can be accessed from any HTML page through JavaScript, and this scenario is shown here.</span></span> <span data-ttu-id="61c8b-108">Para obter um exemplo do uso de [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] com o ASP.NET AJAX, consulte [AJAX exemplos](http://msdn.microsoft.com/en-us/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).</span><span class="sxs-lookup"><span data-stu-id="61c8b-108">For an example of using [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] with ASP.NET AJAX, see [AJAX Samples](http://msdn.microsoft.com/en-us/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).</span></span>  
  
 <span data-ttu-id="61c8b-109">Este exemplo mostra como alternar o tipo de resposta de uma operação entre JSON e XML.</span><span class="sxs-lookup"><span data-stu-id="61c8b-109">This sample shows how to switch the response type of an operation between JSON and XML.</span></span> <span data-ttu-id="61c8b-110">Essa funcionalidade está disponível, independentemente se o serviço está configurado para ser acessado por ASP.NET AJAX ou por uma página de cliente HTML/JavaScript.</span><span class="sxs-lookup"><span data-stu-id="61c8b-110">This functionality is available regardless of whether the service is configured to be accessed by ASP.NET AJAX or by an HTML/JavaScript client page.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="61c8b-111">As instruções de procedimento e a compilação de configuração para este exemplo estão localizadas no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="61c8b-111">The setup procedure and build instructions for this sample are located at the end of this topic.</span></span>  
  
 <span data-ttu-id="61c8b-112">Para habilitar o uso de clientes não - ASP.NET AJAX, use <xref:System.ServiceModel.Activation.WebServiceHostFactory> (não <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>) no arquivo. svc.</span><span class="sxs-lookup"><span data-stu-id="61c8b-112">To enable the use of non-ASP.NET AJAX clients, use <xref:System.ServiceModel.Activation.WebServiceHostFactory> (not <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>) in the .svc file.</span></span> <span data-ttu-id="61c8b-113"><xref:System.ServiceModel.Activation.WebServiceHostFactory>Adiciona um <xref:System.ServiceModel.Description.WebHttpEndpoint> ponto de extremidade padrão para o serviço.</span><span class="sxs-lookup"><span data-stu-id="61c8b-113"><xref:System.ServiceModel.Activation.WebServiceHostFactory> adds a <xref:System.ServiceModel.Description.WebHttpEndpoint> standard endpoint to the service.</span></span> <span data-ttu-id="61c8b-114">O ponto de extremidade é configurado em um endereço vazio em relação ao arquivo. svc; Isso significa que o endereço do serviço é http://localhost/ServiceModelSamples/service.svc com nenhuma sufixos adicionais que não seja o nome da operação.</span><span class="sxs-lookup"><span data-stu-id="61c8b-114">The endpoint is configured at an empty address relative to the .svc file; this means that the address of the service is http://localhost/ServiceModelSamples/service.svc, with no additional suffixes other than the operation name.</span></span>  
  
```html  
<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>  
```  
  
 <span data-ttu-id="61c8b-115">A seção a seguir no Web. config pode ser usada para fazer alterações de configuração adicionais para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="61c8b-115">The following section in Web.config can be used to make additional configuration changes to the endpoint.</span></span> <span data-ttu-id="61c8b-116">Ele pode ser removido se nenhuma alteração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="61c8b-116">It can be removed if no extra changes are needed.</span></span>  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name="" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 <span data-ttu-id="61c8b-117">Os dados padrão de formato para <xref:System.ServiceModel.Description.WebHttpEndpoint> for XML, enquanto o formato de dados padrão para <xref:System.ServiceModel.Description.WebScriptEndpoint> é JSON.</span><span class="sxs-lookup"><span data-stu-id="61c8b-117">The default data format for <xref:System.ServiceModel.Description.WebHttpEndpoint> is XML, while the default data format for <xref:System.ServiceModel.Description.WebScriptEndpoint> is JSON.</span></span> <span data-ttu-id="61c8b-118">Para obter mais informações, consulte [criar serviços do WCF AJAX sem ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md).</span><span class="sxs-lookup"><span data-stu-id="61c8b-118">For more information, see [Creating WCF AJAX Services without ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md).</span></span>  
  
 <span data-ttu-id="61c8b-119">O serviço no exemplo a seguir é um padrão [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] serviço com duas operações.</span><span class="sxs-lookup"><span data-stu-id="61c8b-119">The service in the following sample is a standard [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] service with two operations.</span></span> <span data-ttu-id="61c8b-120">Ambas as operações requerem o <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> estilo de corpo de <xref:System.ServiceModel.Web.WebGetAttribute> ou <xref:System.ServiceModel.Web.WebInvokeAttribute> atributos, que é específico para o `webHttp` comportamento e não possui a opção de formato de dados JSON/XML.</span><span class="sxs-lookup"><span data-stu-id="61c8b-120">Both operations require the <xref:System.ServiceModel.Web.WebMessageBodyStyle.Wrapped> body style on the <xref:System.ServiceModel.Web.WebGetAttribute> or <xref:System.ServiceModel.Web.WebInvokeAttribute> attributes, which is specific to the `webHttp` behavior and has no bearing on the JSON/XML data format switch.</span></span>  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathXml(double n1, double n2);  
```  
  
 <span data-ttu-id="61c8b-121">O formato da resposta para a operação é especificado como XML, que é o padrão definindo para o [ \<webHttp >](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) comportamento.</span><span class="sxs-lookup"><span data-stu-id="61c8b-121">The response format for the operation is specified as XML, which is the default setting for the [\<webHttp>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) behavior.</span></span> <span data-ttu-id="61c8b-122">No entanto, é recomendável explicitamente especificar o formato da resposta.</span><span class="sxs-lookup"><span data-stu-id="61c8b-122">However, it is good practice explicitly specify the response format.</span></span>  
  
 <span data-ttu-id="61c8b-123">Outra operação usa o `WebInvokeAttribute` de atributo e especifique explicitamente o JSON em vez de XML para a resposta.</span><span class="sxs-lookup"><span data-stu-id="61c8b-123">The other operation uses the `WebInvokeAttribute` attribute and explicitly specifies JSON instead of XML for the response.</span></span>  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathJson(double n1, double n2);  
```  
  
 <span data-ttu-id="61c8b-124">Observe que, em ambos os casos, as operações retornam um tipo complexo, `MathResult`, que é um padrão [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] tipo de contrato de dados.</span><span class="sxs-lookup"><span data-stu-id="61c8b-124">Note that in both cases the operations return a complex type, `MathResult`, which is a standard [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] data contract type.</span></span>  
  
 <span data-ttu-id="61c8b-125">O cliente XmlAjaxClientPage.htm de página da Web contém código JavaScript que invoca uma das duas operações anteriores quando o usuário clica o **cálculos (retorno JSON)** ou **cálculos (retorno XML)**  botões na página.</span><span class="sxs-lookup"><span data-stu-id="61c8b-125">The client Web page XmlAjaxClientPage.htm contains JavaScript code that invokes one of the preceding two operations when the user clicks the **Perform calculation (return JSON)** or **Perform calculation (return XML)** buttons on the page.</span></span> <span data-ttu-id="61c8b-126">O código para chamar o serviço constrói um corpo JSON e a envia usando HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="61c8b-126">The code to invoke the service constructs a JSON body and sends it using HTTP POST.</span></span> <span data-ttu-id="61c8b-127">A solicitação é criada manualmente em JavaScript, ao contrário de [serviço AJAX básico](../../../../docs/framework/wcf/samples/basic-ajax-service.md) exemplo e os outros exemplos usando ASP.NET AJAX.</span><span class="sxs-lookup"><span data-stu-id="61c8b-127">The request is created manually in JavaScript, unlike the [Basic AJAX Service](../../../../docs/framework/wcf/samples/basic-ajax-service.md) sample and the other samples using ASP.NET AJAX.</span></span>  
  
```  
// Create HTTP request  
var xmlHttp;  
// Request instantiation code omitted…  
// Result handler code omitted…  
  
// Build the operation URL  
var url = "service.svc/ajaxEndpoint/";  
url = url + operation;  
  
// Build the body of the JSON message  
var body = '{"n1":';  
body = body + document.getElementById("num1").value + ',"n2":';  
body = body + document.getElementById("num2").value + '}';  
  
// Send the HTTP request  
xmlHttp.open("POST", url, true);  
xmlHttp.setRequestHeader("Content-type", "application/json");  
xmlHttp.send(body);  
```  
  
 <span data-ttu-id="61c8b-128">Quando o serviço responde, a resposta será exibida sem nenhum processamento adicional em uma caixa de texto na página.</span><span class="sxs-lookup"><span data-stu-id="61c8b-128">When the service responds, the response is displayed without any further processing in a textbox on the page.</span></span> <span data-ttu-id="61c8b-129">Isso é implementado para fins de demonstração permitir que você observar diretamente os formatos de dados XML e JSON usados.</span><span class="sxs-lookup"><span data-stu-id="61c8b-129">This is implemented for demonstration purposes to allow you to directly observe the XML and JSON data formats used.</span></span>  
  
```  
// Create result handler   
xmlHttp.onreadystatechange=function(){  
     if(xmlHttp.readyState == 4){  
          document.getElementById("result").value = xmlHttp.responseText;  
     }  
}  
```  
  
> [!IMPORTANT]
>  <span data-ttu-id="61c8b-130">Os exemplos podem já estar instalados no seu computador.</span><span class="sxs-lookup"><span data-stu-id="61c8b-130">The samples may already be installed on your machine.</span></span> <span data-ttu-id="61c8b-131">Verifique o seguinte diretório (padrão) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="61c8b-131">Check for the following (default) directory before continuing.</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  <span data-ttu-id="61c8b-132">Se este diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos do Windows Workflow Foundation (WF) para o .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) para baixar todos os [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos.</span><span class="sxs-lookup"><span data-stu-id="61c8b-132">If this directory does not exist, go to [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) to download all [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] and [!INCLUDE[wf1](../../../../includes/wf1-md.md)] samples.</span></span> <span data-ttu-id="61c8b-133">Este exemplo está localizado no seguinte diretório.</span><span class="sxs-lookup"><span data-stu-id="61c8b-133">This sample is located in the following directory.</span></span>  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`  
  
#### <a name="to-set-up-build-and-run-the-sample"></a><span data-ttu-id="61c8b-134">Para configurar, compilar, e executar o exemplo</span><span class="sxs-lookup"><span data-stu-id="61c8b-134">To set up, build, and run the sample</span></span>  
  
1.  <span data-ttu-id="61c8b-135">Certifique-se de que você executou o [único procedimento de instalação para os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span><span class="sxs-lookup"><span data-stu-id="61c8b-135">Ensure that you have performed the [One-Time Setup Procedure for the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).</span></span>  
  
2.  <span data-ttu-id="61c8b-136">Compile a solução XmlAjaxService.sln conforme descrito em [compilar os exemplos do Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).</span><span class="sxs-lookup"><span data-stu-id="61c8b-136">Build the solution XmlAjaxService.sln as described in [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).</span></span>  
  
3.  <span data-ttu-id="61c8b-137">Navegue até http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm (não abrir XmlAjaxClientPage.htm no navegador do diretório do projeto).</span><span class="sxs-lookup"><span data-stu-id="61c8b-137">Navigate to http://localhost/ServiceModelSamples/XmlAjaxClientPage.htm (do not open XmlAjaxClientPage.htm in the browser from the project directory).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="61c8b-138">Consulte também</span><span class="sxs-lookup"><span data-stu-id="61c8b-138">See Also</span></span>  
 [<span data-ttu-id="61c8b-139">Serviço de AJAX utilizando o HTTP POST</span><span class="sxs-lookup"><span data-stu-id="61c8b-139">AJAX Service Using HTTP POST</span></span>](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)