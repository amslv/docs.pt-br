---
title: "Como criar um aplicativo ASP.NET Web Forms baseado em declarações usando o WIF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: efb264dd-f47b-49a9-85ee-9f45d4425765
caps.latest.revision: 7
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d5b81e20ed1b39c7750329718729905484eb7fa1
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-build-claims-aware-aspnet-web-forms-application-using-wif"></a><span data-ttu-id="5b4e8-102">Como criar um aplicativo ASP.NET Web Forms baseado em declarações usando o WIF</span><span class="sxs-lookup"><span data-stu-id="5b4e8-102">How To: Build Claims-Aware ASP.NET Web Forms Application Using WIF</span></span>
## <a name="applies-to"></a><span data-ttu-id="5b4e8-103">Aplica-se a</span><span class="sxs-lookup"><span data-stu-id="5b4e8-103">Applies To</span></span>  
  
-   <span data-ttu-id="5b4e8-104">Microsoft® Windows® Identity Foundation (WIF)</span><span class="sxs-lookup"><span data-stu-id="5b4e8-104">Microsoft® Windows® Identity Foundation (WIF)</span></span>  
  
-   <span data-ttu-id="5b4e8-105">Web Forms do ASP.NET®</span><span class="sxs-lookup"><span data-stu-id="5b4e8-105">ASP.NET® Web Forms</span></span>  
  
## <a name="summary"></a><span data-ttu-id="5b4e8-106">Resumo</span><span class="sxs-lookup"><span data-stu-id="5b4e8-106">Summary</span></span>  
 <span data-ttu-id="5b4e8-107">Estas Instruções fornecem procedimentos passo a passo detalhados para criar um aplicativo Web ASP.NET Web Forms simples baseado em declarações.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-107">This How-To provides detailed step-by-step procedures for creating simple claims-aware ASP.NET Web Forms application.</span></span> <span data-ttu-id="5b4e8-108">Também fornecem instruções sobre como testar o aplicativo Web ASP.NET Web Forms simples baseado em declarações para uma implementação bem-sucedida da autenticação federada.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-108">It also provides instructions for how to test the simple claims-aware ASP.NET Web Forms application for successful implementation of federated authentication.</span></span> <span data-ttu-id="5b4e8-109">Estas Instruções não contêm instruções detalhadas para a criação de um STS (Serviço de Token de Segurança) e pressupõe que você já tenha configurado um.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-109">This How-To does not have detailed instructions for creating a Security Token Service (STS), and assumes you have already configured an STS.</span></span>  
  
## <a name="contents"></a><span data-ttu-id="5b4e8-110">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="5b4e8-110">Contents</span></span>  
  
-   <span data-ttu-id="5b4e8-111">Objetivos</span><span class="sxs-lookup"><span data-stu-id="5b4e8-111">Objectives</span></span>  
  
-   <span data-ttu-id="5b4e8-112">Resumo das etapas</span><span class="sxs-lookup"><span data-stu-id="5b4e8-112">Summary of Steps</span></span>  
  
-   <span data-ttu-id="5b4e8-113">Etapa 1 – criar um aplicativo ASP.NET Web Forms simples</span><span class="sxs-lookup"><span data-stu-id="5b4e8-113">Step 1 – Create a Simple ASP.NET Web Forms Application</span></span>  
  
-   <span data-ttu-id="5b4e8-114">Etapa 2 – Configurar um aplicativo ASP.NET Web Forms para autenticação baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-114">Step 2 – Configure ASP.NET Web Forms Application for Claims-Based Authentication</span></span>  
  
-   <span data-ttu-id="5b4e8-115">Etapa 3 – Testar a solução</span><span class="sxs-lookup"><span data-stu-id="5b4e8-115">Step 3 – Test Your Solution</span></span>  
  
## <a name="objectives"></a><span data-ttu-id="5b4e8-116">Objetivos</span><span class="sxs-lookup"><span data-stu-id="5b4e8-116">Objectives</span></span>  
  
-   <span data-ttu-id="5b4e8-117">Configurar um aplicativo ASP.NET Web Forms para autenticação baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-117">Configure ASP.NET Web Forms application for claims-based authentication</span></span>  
  
-   <span data-ttu-id="5b4e8-118">Testar um aplicativo Web ASP.NET Web Forms bem-sucedido baseado em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-118">Test successful claims-aware ASP.NET Web Forms application</span></span>  
  
## <a name="summary-of-steps"></a><span data-ttu-id="5b4e8-119">Resumo das etapas</span><span class="sxs-lookup"><span data-stu-id="5b4e8-119">Summary of Steps</span></span>  
  
-   <span data-ttu-id="5b4e8-120">Etapa 1 – Criar um aplicativo ASP.NET Web Forms simples</span><span class="sxs-lookup"><span data-stu-id="5b4e8-120">Step 1 – Create Simple ASP.NET Web Forms Application</span></span>  
  
-   <span data-ttu-id="5b4e8-121">Etapa 2 – Configurar um aplicativo ASP.NET Web Forms para autenticação federada</span><span class="sxs-lookup"><span data-stu-id="5b4e8-121">Step 2 – Configure ASP.NET Web Forms Application for Federated Authentication</span></span>  
  
-   <span data-ttu-id="5b4e8-122">Etapa 3 – Testar a solução</span><span class="sxs-lookup"><span data-stu-id="5b4e8-122">Step 3 – Test Your Solution</span></span>  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a><span data-ttu-id="5b4e8-123">Etapa 1 – criar um aplicativo ASP.NET Web Forms simples</span><span class="sxs-lookup"><span data-stu-id="5b4e8-123">Step 1 – Create a Simple ASP.NET Web Forms Application</span></span>  
 <span data-ttu-id="5b4e8-124">Nesta etapa, você criará um novo aplicativo ASP.NET Web Forms.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-124">In this step, you will create a new ASP.NET Web Forms application.</span></span>  
  
#### <a name="to-create-a-simple-aspnet-application"></a><span data-ttu-id="5b4e8-125">Para criar um aplicativo ASP.NET simples</span><span class="sxs-lookup"><span data-stu-id="5b4e8-125">To create a simple ASP.NET application</span></span>  
  
1.  <span data-ttu-id="5b4e8-126">Inicie o Visual Studio, clique em **Arquivo**, **Novo** e, depois, em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-126">Start Visual Studio and click **File**, **New**, and then **Project**.</span></span>  
  
2.  <span data-ttu-id="5b4e8-127">Na janela **Novo Projeto**, clique em **Aplicativo ASP.NET Web Forms**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-127">In the **New Project** window, click **ASP.NET Web Forms Application**.</span></span>  
  
3.  <span data-ttu-id="5b4e8-128">Em **Nome**, insira `TestApp` e pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-128">In **Name**, enter `TestApp` and press **OK**.</span></span>  
  
## <a name="step-2--configure-aspnet-web-forms-application-for-claims-based-authentication"></a><span data-ttu-id="5b4e8-129">Etapa 2 – Configurar um aplicativo ASP.NET Web Forms para autenticação baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-129">Step 2 – Configure ASP.NET Web Forms Application for Claims-Based Authentication</span></span>  
 <span data-ttu-id="5b4e8-130">Nesta etapa, você adicionará entradas de configuração ao arquivo de configuração *Web.config* do aplicativo Web ASP.NET Web Forms para torná-lo baseado em declarações.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-130">In this step you will add configuration entries to the *Web.config* configuration file of your ASP.NET Web Forms application to make it claims-aware.</span></span>  
  
#### <a name="to-configure-aspnet-application-for-claims-based-authentication"></a><span data-ttu-id="5b4e8-131">Para configurar um aplicativo ASP.NET para autenticação baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-131">To configure ASP.NET application for claims-based authentication</span></span>  
  
1.  <span data-ttu-id="5b4e8-132">Adicione as seguintes entradas de seção de configuração ao arquivo de configuração *Web.config* imediatamente após o elemento de abertura **\<configuration>**:</span><span class="sxs-lookup"><span data-stu-id="5b4e8-132">Add the following configuration section entries to the *Web.config* configuration file immediately after the **\<configuration>** opening element:</span></span>  
  
    ```xml  
    <configSections>  
      <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
      <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    </configSections>  
    ```  
  
2.  <span data-ttu-id="5b4e8-133">Adicione um elemento **\<location>** que habilita o acesso aos metadados de federação do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="5b4e8-133">Add a **\<location>** element that enables access to the application’s federation metadata:</span></span>  
  
    ```xml  
    <location path="FederationMetadata">  
      <system.web>  
        <authorization>  
          <allow users="*" />  
        </authorization>  
      </system.web>  
    </location>  
    ```  
  
3.  <span data-ttu-id="5b4e8-134">Adicione as seguintes entradas de configuração nos elementos **\<system.web>** para negar usuários, desabilitar a autenticação nativa e permitir que o WIF gerencie a autenticação.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-134">Add the following configuration entries within the **\<system.web>** elements to deny users, disable native authentication, and enable WIF to manage authentication.</span></span>  
  
    ```xml  
    <authorization>  
      <deny users="?" />  
    </authorization>  
    <authentication mode="None" />  
    ```  
  
4.  <span data-ttu-id="5b4e8-135">Adicione um elemento **\<system.webServer>** que define os módulos para autenticação federada.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-135">Add a **\<system.webServer>** element that defines the modules for federated authentication.</span></span> <span data-ttu-id="5b4e8-136">Observe que o atributo *PublicKeyToken* deve ser igual ao atributo *PublicKeyToken* das entradas **\<configSections>** adicionadas anteriormente:</span><span class="sxs-lookup"><span data-stu-id="5b4e8-136">Note that the *PublicKeyToken* attribute must be the same as the *PublicKeyToken* attribute for the **\<configSections>** entries added earlier:</span></span>  
  
    ```xml  
    <system.webServer>  
      <modules>  
        <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
        <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      </modules>  
    </system.webServer>  
    ```  
  
5.  <span data-ttu-id="5b4e8-137">Adicione as entradas de configuração relacionadas ao Windows Identity Foundation a seguir e garanta que a URL e o número da porta do aplicativo ASP.NET correspondam aos valores na entrada **\<audienceUris>**, no atributo **realm** do elemento **\<wsFederation>** e no atributo **reply** do elemento **\<wsFederation>**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-137">Add the following Windows Identity Foundation related configuration entries and ensure that your ASP.NET application’s URL and port number match the values in the **\<audienceUris>** entry, **realm** attribute of the **\<wsFederation>** element, and the **reply** attribute of the **\<wsFederation>** element.</span></span> <span data-ttu-id="5b4e8-138">Também garanta que o valor **issuer** se ajuste à URL do STS (Serviço de Token de Segurança).</span><span class="sxs-lookup"><span data-stu-id="5b4e8-138">Also ensure that the **issuer** value fits your Security Token Service (STS) URL.</span></span>  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <audienceUris>  
                <add value="http://localhost:28503/" />  
            </audienceUris>  
            <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
                <trustedIssuers>  
                    <add thumbprint="1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234" name="YourSTSName" />  
                </trustedIssuers>   
            </issuerNameRegistry>  
            <certificateValidation certificateValidationMode="None" />  
        </identityConfiguration>  
    </system.identityModel>  
    <system.identityModel.services>  
        <federationConfiguration>  
            <cookieHandler requireSsl="false" />  
            <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:13922/wsFederationSTS/Issue" realm="http://localhost:28503/" reply="http://localhost:28503/" requireHttps="false" />  
        </federationConfiguration>  
    </system.identityModel.services>  
    ```  
  
6.  <span data-ttu-id="5b4e8-139">Adicione uma referência ao assembly <xref:System.IdentityModel>.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-139">Add reference to the <xref:System.IdentityModel> assembly.</span></span>  
  
7.  <span data-ttu-id="5b4e8-140">Compile a solução para verificar se não há erros.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-140">Compile the solution to make sure there are no errors.</span></span>  
  
## <a name="step-3--test-your-solution"></a><span data-ttu-id="5b4e8-141">Etapa 3 – Testar a solução</span><span class="sxs-lookup"><span data-stu-id="5b4e8-141">Step 3 – Test Your Solution</span></span>  
 <span data-ttu-id="5b4e8-142">Nesta etapa, você testará o aplicativo Web ASP.NET Web Forms configurado para a autenticação baseada em declarações.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-142">In this step you will test your ASP.NET Web Forms application configured for claims-based authentication.</span></span> <span data-ttu-id="5b4e8-143">Para executar um teste básico, você adicionará um código que exibe as declarações no token emitido pelo STS (Serviço de Token de Segurança).</span><span class="sxs-lookup"><span data-stu-id="5b4e8-143">To perform a basic test, you will add code that displays claims in the token issued by the Security Token Service (STS).</span></span>  
  
#### <a name="to-test-your-aspnet-web-form-application-for-claims-based-authentication"></a><span data-ttu-id="5b4e8-144">Para testar o aplicativo ASP.NET Web Forms para autenticação baseada em declarações</span><span class="sxs-lookup"><span data-stu-id="5b4e8-144">To test your ASP.NET Web Form application for claims-based authentication</span></span>  
  
1.  <span data-ttu-id="5b4e8-145">Abra o arquivo **Default.aspx** no projeto **TestApp** e substitua sua marcação existente pela seguinte marcação:</span><span class="sxs-lookup"><span data-stu-id="5b4e8-145">Open the **Default.aspx** file under the **TestApp** project and replace its existing markup with the following markup:</span></span>  
  
    ```  
    %@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head id="Head1" runat="server">  
        <title></title>  
    </head>  
    <body>  
        <h1><asp:label ID="signedIn" runat="server" /></h1>  
        <asp:label ID="claimType" runat="server" />  
        <asp:label ID="claimValue" runat="server" />  
        <asp:label ID="claimValueType" runat="server" />  
        <asp:label ID="claimSubjectName" runat="server" />  
        <asp:label ID="claimIssuer" runat="server" />  
    </body>  
    </html>  
    ```  
  
2.  <span data-ttu-id="5b4e8-146">Salve **Default.aspx** e, depois, abra seu arquivo code-behind chamado **Default.aspx.cs**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-146">Save **Default.aspx**, and then open its code behind file named **Default.aspx.cs**.</span></span>  
  
    > [!NOTE]
    >  <span data-ttu-id="5b4e8-147">**Default.aspx.cs** pode estar oculto sob **Default.aspx** no Gerenciador de Soluções.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-147">**Default.aspx.cs** may be hidden beneath **Default.aspx** in Solution Explorer.</span></span> <span data-ttu-id="5b4e8-148">Se **Default.aspx.cs** não estiver visível, expanda **Default.aspx** clicando no triângulo ao lado dele.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-148">If **Default.aspx.cs** is not visible, expand **Default.aspx** by clicking on the triangle next to it.</span></span>  
  
3.  <span data-ttu-id="5b4e8-149">Substitua o código existente no método **Page_Load** de **Default.aspx.cs** pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="5b4e8-149">Replace the existing code in the **Page_Load** method of **Default.aspx.cs** with the following code:</span></span>  
  
    ```csharp  
    using System;  
    using System.IdentityModel;  
    using System.Security.Claims;  
    using System.Threading;  
    using System.Web.UI;  
  
    namespace TestApp  
    {  
        public partial class _Default : System.Web.UI.Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
                if (claimsPrincipal != null)  
                {  
                    signedIn.Text = "You are signed in.";  
  
                    foreach (Claim claim in claimsPrincipal.Claims)  
                    {  
                        claimType.Text = claim.Type;  
                        claimValue.Text = claim.Value;  
                        claimValueType.Text = claim.ValueType;  
                        claimSubjectName.Text = claim.Subject.Name;  
                        claimIssuer.Text = claim.Issuer;  
                    }  
                }  
                else  
                {  
                    signedIn.Text = "You are not signed in.";  
                }  
            }  
        }  
    }  
    ```  
  
4.  <span data-ttu-id="5b4e8-150">Salve **Default.aspx.cs** e crie a solução.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-150">Save **Default.aspx.cs**, and build the solution.</span></span>  
  
5.  <span data-ttu-id="5b4e8-151">Execute a solução pressionando a tecla **F5**.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-151">Run the solution by pressing the **F5** key.</span></span>  
  
6.  <span data-ttu-id="5b4e8-152">Você deverá ver a página que exibe as declarações no token que foi emitido por você pelo Serviço de Token de Segurança.</span><span class="sxs-lookup"><span data-stu-id="5b4e8-152">You should be presented with the page that displays the claims in the token that was issued to you by the Security Token Service.</span></span>
