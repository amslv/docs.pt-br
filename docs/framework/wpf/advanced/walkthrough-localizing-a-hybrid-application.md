---
title: "Instruções passo a passo: localizando um aplicativo híbrido"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- localization [WPF interoperability]
- hybrid applications [WPF interoperability]
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
caps.latest.revision: "17"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 5e1425eafd0f1663aaf82185e0f32bf2a3bea509
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="walkthrough-localizing-a-hybrid-application"></a><span data-ttu-id="c3cc0-102">Instruções passo a passo: localizando um aplicativo híbrido</span><span class="sxs-lookup"><span data-stu-id="c3cc0-102">Walkthrough: Localizing a Hybrid Application</span></span>
<span data-ttu-id="c3cc0-103">Este passo a passo mostra como localizar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elementos em um [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-com base em aplicativo híbrido.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-103">This walkthrough shows you how to localize [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elements in a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-based hybrid application.</span></span>  
  
 <span data-ttu-id="c3cc0-104">As tarefas ilustradas neste passo a passo incluem:</span><span class="sxs-lookup"><span data-stu-id="c3cc0-104">Tasks illustrated in this walkthrough include:</span></span>  
  
-   <span data-ttu-id="c3cc0-105">Criando o [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] projeto do host.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-105">Creating the [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] host project.</span></span>  
  
-   <span data-ttu-id="c3cc0-106">Atributo de conteúdo localizável.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-106">Adding localizable content.</span></span>  
  
-   <span data-ttu-id="c3cc0-107">Habilitando a localização.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-107">Enabling localization.</span></span>  
  
-   <span data-ttu-id="c3cc0-108">Atribuindo identificadores de recursos.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-108">Assigning resource identifiers.</span></span>  
  
-   <span data-ttu-id="c3cc0-109">Usando a ferramenta LocBaml para produzir um assembly satélite.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-109">Using the LocBaml tool to produce a satellite assembly.</span></span>  
  
 <span data-ttu-id="c3cc0-110">Para uma listagem de código completa das tarefas ilustradas neste passo a passo, consulte [Localizando um exemplo de aplicativo híbrido](http://go.microsoft.com/fwlink/?LinkID=160015).</span><span class="sxs-lookup"><span data-stu-id="c3cc0-110">For a complete code listing of the tasks illustrated in this walkthrough, see [Localizing a Hybrid Application Sample](http://go.microsoft.com/fwlink/?LinkID=160015).</span></span>  
  
 <span data-ttu-id="c3cc0-111">Quando tiver terminado, você terá um aplicativo híbrido localizado.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-111">When you are finished, you will have a localized hybrid application.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="c3cc0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3cc0-112">Prerequisites</span></span>  
 <span data-ttu-id="c3cc0-113">Você precisa dos seguintes componentes para concluir esta instrução passo a passo:</span><span class="sxs-lookup"><span data-stu-id="c3cc0-113">You need the following components to complete this walkthrough:</span></span>  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)]<span data-ttu-id="c3cc0-114">.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-114">.</span></span>  
  
## <a name="creating-the-windows-forms-host-project"></a><span data-ttu-id="c3cc0-115">Criando o projeto de host do Windows Forms</span><span class="sxs-lookup"><span data-stu-id="c3cc0-115">Creating the Windows Forms Host Project</span></span>  
 <span data-ttu-id="c3cc0-116">A primeira etapa é criar o [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] aplicativo do projeto e adicionar um [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] elemento com conteúdo que você irá localizar.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-116">The first step is to create the [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] application project and add a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] element with content that you will localize.</span></span>  
  
#### <a name="to-create-the-host-project"></a><span data-ttu-id="c3cc0-117">Criar o projeto de host</span><span class="sxs-lookup"><span data-stu-id="c3cc0-117">To create the host project</span></span>  
  
1.  <span data-ttu-id="c3cc0-118">Crie um projeto de aplicativo WPF chamado `LocalizingWpfInWf`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-118">Create a WPF Application project named `LocalizingWpfInWf`.</span></span> <span data-ttu-id="c3cc0-119">Para obter mais informações, consulte [Como criar um projeto de aplicativos do Windows](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa).</span><span class="sxs-lookup"><span data-stu-id="c3cc0-119">For more information, see [How to: Create a Windows Application Project](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa).</span></span>  
  
2.  <span data-ttu-id="c3cc0-120">Adicionar um [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> elemento chamado `SimpleControl` ao projeto.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-120">Add a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.UserControl> element called `SimpleControl` to the project.</span></span>  
  
3.  <span data-ttu-id="c3cc0-121">Use o <xref:System.Windows.Forms.Integration.ElementHost> controle para colocar um `SimpleControl` elemento no formulário.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-121">Use the <xref:System.Windows.Forms.Integration.ElementHost> control to place a `SimpleControl` element on the form.</span></span> <span data-ttu-id="c3cc0-122">Para obter mais informações, consulte [passo a passo: hospedando um controle composto do WPF 3D em Windows Forms](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md).</span><span class="sxs-lookup"><span data-stu-id="c3cc0-122">For more information, see [Walkthrough: Hosting a 3-D WPF Composite Control in Windows Forms](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md).</span></span>  
  
## <a name="adding-localizable-content"></a><span data-ttu-id="c3cc0-123">Adicionando conteúdo localizável</span><span class="sxs-lookup"><span data-stu-id="c3cc0-123">Adding Localizable Content</span></span>  
 <span data-ttu-id="c3cc0-124">Em seguida, você adicionará um [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle de rótulo e defina o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] do conteúdo de elemento em uma cadeia de caracteres localizável.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-124">Next, you will add a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] label control and set the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] element's content to a localizable string.</span></span>  
  
#### <a name="to-add-localizable-content"></a><span data-ttu-id="c3cc0-125">Para adicionar um conteúdo localizável</span><span class="sxs-lookup"><span data-stu-id="c3cc0-125">To add localizable content</span></span>  
  
1.  <span data-ttu-id="c3cc0-126">No Solution Explorer, clique duas vezes em **SimpleControl.xaml** para abri-lo no [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].</span><span class="sxs-lookup"><span data-stu-id="c3cc0-126">In Solution Explorer, double-click **SimpleControl.xaml** to open it in the [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].</span></span>  
  
2.  <span data-ttu-id="c3cc0-127">Definir o conteúdo do <xref:System.Windows.Controls.Button> controlar usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-127">Set the content of the <xref:System.Windows.Controls.Button> control using the following code.</span></span>  
  
     [!code-xaml[LocalizingWpfInWf#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]  
  
3.  <span data-ttu-id="c3cc0-128">No Solution Explorer, clique duas vezes em **Form1** para abri-lo no Designer de formulários do Windows.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-128">In Solution Explorer, double-click **Form1** to open it in the Windows Forms Designer.</span></span>  
  
4.  <span data-ttu-id="c3cc0-129">Abra a caixa de ferramentas e clique duas vezes em **rótulo** para adicionar um controle de rótulo para o formulário.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-129">Open the Toolbox and double-click **Label** to add a label control to the form.</span></span> <span data-ttu-id="c3cc0-130">Defina o valor de seu <xref:System.Windows.Forms.Control.Text%2A> propriedade `"Hello"`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-130">Set the value of its <xref:System.Windows.Forms.Control.Text%2A> property to `"Hello"`.</span></span>  
  
5.  <span data-ttu-id="c3cc0-131">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-131">Press F5 to build and run the application.</span></span>  
  
     <span data-ttu-id="c3cc0-132">Ambos os `SimpleControl` elemento e o controle de rótulo exibem o texto **"Hello"**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-132">Both the `SimpleControl` element and the label control display the text **"Hello"**.</span></span>  
  
## <a name="enabling-localization"></a><span data-ttu-id="c3cc0-133">Habilitando a localização</span><span class="sxs-lookup"><span data-stu-id="c3cc0-133">Enabling Localization</span></span>  
 <span data-ttu-id="c3cc0-134">O Designer de Formulários do Windows fornece configurações para habilitar a localização em um assembly satélite.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-134">The Windows Forms Designer provides settings for enabling localization in a satellite assembly.</span></span>  
  
#### <a name="to-enable-localization"></a><span data-ttu-id="c3cc0-135">Para permitir a localização</span><span class="sxs-lookup"><span data-stu-id="c3cc0-135">To enable localization</span></span>  
  
1.  <span data-ttu-id="c3cc0-136">No Solution Explorer, clique duas vezes em **Form1.cs** para abri-lo no Designer de formulários do Windows.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-136">In Solution Explorer, double-click **Form1.cs** to open it in the Windows Forms Designer.</span></span>  
  
2.  <span data-ttu-id="c3cc0-137">Na janela Propriedades, defina o valor no formato **Localizable** propriedade `true`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-137">In the Properties window, set the value of the form's **Localizable** property to `true`.</span></span>  
  
3.  <span data-ttu-id="c3cc0-138">Na janela Propriedades, defina o valor da **idioma** propriedade **Espanhol (Espanha)**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-138">In the Properties window, set the value of the **Language** property to **Spanish (Spain)**.</span></span>  
  
4.  <span data-ttu-id="c3cc0-139">No Designer de Formulários do Windows, selecione o controle de rótulo.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-139">In the Windows Forms Designer, select the label control.</span></span>  
  
5.  <span data-ttu-id="c3cc0-140">Na janela Propriedades, defina o valor da <xref:System.Windows.Forms.Control.Text%2A> propriedade `"Hola"`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-140">In the Properties window, set the value of the <xref:System.Windows.Forms.Control.Text%2A> property to `"Hola"`.</span></span>  
  
     <span data-ttu-id="c3cc0-141">Um novo arquivo de recursos chamado Form1.es-ES.resx é adicionado ao projeto.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-141">A new resource file named Form1.es-ES.resx is added to the project.</span></span>  
  
6.  <span data-ttu-id="c3cc0-142">No Gerenciador de soluções, clique com botão direito **Form1.cs** e clique em **Exibir código** para abri-lo no Editor de códigos.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-142">In Solution Explorer, right-click **Form1.cs** and click **View Code** to open it in the Code Editor.</span></span>  
  
7.  <span data-ttu-id="c3cc0-143">Copie o seguinte código para o `Form1` construtor, antes da chamada `InitializeComponent`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-143">Copy the following code into the `Form1` constructor, preceding the call to `InitializeComponent`.</span></span>  
  
     [!code-csharp[LocalizingWpfInWf#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]  
  
8.  <span data-ttu-id="c3cc0-144">No Gerenciador de soluções, clique com botão direito **LocalizingWpfInWf** e clique em **descarregar projeto**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-144">In Solution Explorer, right-click **LocalizingWpfInWf** and click **Unload Project**.</span></span>  
  
     <span data-ttu-id="c3cc0-145">O nome do projeto é rotulado **(não disponível)**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-145">The project name is labeled **(unavailable)**.</span></span>  
  
9. <span data-ttu-id="c3cc0-146">Clique com botão direito **LocalizingWpfInWf**e clique em **LocalizingWpfInWf.csproj editar**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-146">Right-click **LocalizingWpfInWf**, and click **Edit LocalizingWpfInWf.csproj**.</span></span>  
  
     <span data-ttu-id="c3cc0-147">O arquivo de projeto é aberto no Editor de Códigos.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-147">The project file opens in the Code Editor.</span></span>  
  
10. <span data-ttu-id="c3cc0-148">Copie a seguinte linha no primeiro `PropertyGroup` no arquivo de projeto.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-148">Copy the following line into the first `PropertyGroup` in the project file.</span></span>  
  
    ```xml  
    <UICulture>en-US</UICulture>   
    ```  
  
11. <span data-ttu-id="c3cc0-149">Salve o arquivo de projeto e feche-o.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-149">Save the project file and close it.</span></span>  
  
12. <span data-ttu-id="c3cc0-150">No Gerenciador de soluções, clique com botão direito **LocalizingWpfInWf** e clique em **recarregar projeto**.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-150">In Solution Explorer, right-click **LocalizingWpfInWf** and click **Reload Project**.</span></span>  
  
## <a name="assigning-resource-identifiers"></a><span data-ttu-id="c3cc0-151">Atribuindo identificadores de recursos</span><span class="sxs-lookup"><span data-stu-id="c3cc0-151">Assigning Resource Identifiers</span></span>  
 <span data-ttu-id="c3cc0-152">Você pode mapear o conteúdo localizável para assemblies de recursos usando identificadores de recurso.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-152">You can map your localizable content to resource assemblies by using resource identifiers.</span></span> <span data-ttu-id="c3cc0-153">O aplicativo MsBuild.exe atribui automaticamente identificadores de recursos quando você especificar o `updateuid` opção.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-153">The MsBuild.exe application automatically assigns resource identifiers when you specify the `updateuid` option.</span></span>  
  
#### <a name="to-assign-resource-identifiers"></a><span data-ttu-id="c3cc0-154">Para atribuir identificadores de recursos</span><span class="sxs-lookup"><span data-stu-id="c3cc0-154">To assign resource identifiers</span></span>  
  
1.  <span data-ttu-id="c3cc0-155">No Menu Iniciar, abra o [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] Prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-155">From the Start Menu, open the [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] Command Prompt.</span></span>  
  
2.  <span data-ttu-id="c3cc0-156">Use o comando a seguir para atribuir identificadores de recurso ao seu conteúdo localizável.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-156">Use the following command to assign resource identifiers to your localizable content.</span></span>  
  
    ```  
    msbuild /t:updateuid LocalizingWpfInWf.csproj  
    ```  
  
3.  <span data-ttu-id="c3cc0-157">No Solution Explorer, clique duas vezes em **SimpleControl.xaml** para abri-lo no Editor de códigos.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-157">In Solution Explorer, double-click **SimpleControl.xaml** to open it in the Code Editor.</span></span> <span data-ttu-id="c3cc0-158">Você verá que o `msbuild` comando adicionou o `Uid` a todos os elementos de atributo.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-158">You will see that the `msbuild` command has added the `Uid` attribute to all the elements.</span></span> <span data-ttu-id="c3cc0-159">Isso facilita a localização por meio da atribuição de identificadores de recurso.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-159">This facilitates localization through the assignment of resource identifiers.</span></span>  
  
     [!code-xaml[LocalizingWpfInWf#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]  
  
4.  <span data-ttu-id="c3cc0-160">Pressione F6 para compilar a solução.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-160">Press F6 to build the solution.</span></span>  
  
## <a name="using-locbaml-to-produce-a-satellite-assembly"></a><span data-ttu-id="c3cc0-161">Usando LocBaml para produzir um assembly satélite</span><span class="sxs-lookup"><span data-stu-id="c3cc0-161">Using LocBaml to Produce a Satellite Assembly</span></span>  
 <span data-ttu-id="c3cc0-162">O conteúdo localizado estiver armazenado em um recurso somente *assembly satélite*.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-162">Your localized content is stored in a resource-only *satellite assembly*.</span></span> <span data-ttu-id="c3cc0-163">Use a ferramenta de linha de comando LocBaml.exe para produzir um assembly localizado para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-163">Use the command-line tool LocBaml.exe to produce a localized assembly for your [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] content.</span></span>  
  
#### <a name="to-produce-a-satellite-assembly"></a><span data-ttu-id="c3cc0-164">Para produzir um assembly satélite</span><span class="sxs-lookup"><span data-stu-id="c3cc0-164">To produce a satellite assembly</span></span>  
  
1.  <span data-ttu-id="c3cc0-165">Copie LocBaml.exe para sua pasta do projeto obj\Debug.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-165">Copy LocBaml.exe to your project's obj\Debug folder.</span></span> <span data-ttu-id="c3cc0-166">Para obter mais informações, consulte [localizar um aplicativo](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md).</span><span class="sxs-lookup"><span data-stu-id="c3cc0-166">For more information, see [Localize an Application](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md).</span></span>  
  
2.  <span data-ttu-id="c3cc0-167">Na janela do Prompt de Comando, use o seguinte comando para extrair cadeias de caracteres de recurso em um arquivo temporário.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-167">In the Command Prompt window, use the following command to extract resource strings into a temporary file.</span></span>  
  
    ```  
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv  
    ```  
  
3.  <span data-ttu-id="c3cc0-168">Abra o arquivo temp.csv com [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] ou outro editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-168">Open the temp.csv file with [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] or another text editor.</span></span> <span data-ttu-id="c3cc0-169">Substitua a cadeia de caracteres `"Hello"` com sua tradução de espanhol, `"Hola"`.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-169">Replace the string `"Hello"` with its Spanish translation, `"Hola"`.</span></span>  
  
4.  <span data-ttu-id="c3cc0-170">Salve o arquivo temp.csv.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-170">Save the temp.csv file.</span></span>  
  
5.  <span data-ttu-id="c3cc0-171">Use o seguinte comando para gerar o arquivo de recurso localizado.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-171">Use the following command to generate the localized resource file.</span></span>  
  
    ```  
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES  
    ```  
  
     <span data-ttu-id="c3cc0-172">O arquivo LocalizingWpfInWf.g.es-ES.resources é criado na pasta obj\Debug.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-172">The LocalizingWpfInWf.g.es-ES.resources file is created in the obj\Debug folder.</span></span>  
  
6.  <span data-ttu-id="c3cc0-173">Use o seguinte comando para compilar o assembly satélite localizado.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-173">Use the following command to build the localized satellite assembly.</span></span>  
  
    ```  
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources  
    ```  
  
     <span data-ttu-id="c3cc0-174">O arquivo LocalizingWpfInWf.resources.dll é criado na pasta obj\Debug.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-174">The LocalizingWpfInWf.resources.dll file is created in the obj\Debug folder.</span></span>  
  
7.  <span data-ttu-id="c3cc0-175">Copie o arquivo LocalizingWpfInWf.resources.dll para a pasta do projeto bin\Debug\es-ES.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-175">Copy the LocalizingWpfInWf.resources.dll file to the project's bin\Debug\es-ES folder.</span></span> <span data-ttu-id="c3cc0-176">Substitua o arquivo existente.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-176">Replace the existing file.</span></span>  
  
8.  <span data-ttu-id="c3cc0-177">Execute LocalizingWpfInWf.exe, que está localizado na pasta bin\Debug de seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-177">Run LocalizingWpfInWf.exe, which is located in your project's bin\Debug folder.</span></span> <span data-ttu-id="c3cc0-178">Não recompilar o aplicativo ou o assembly satélite será substituído.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-178">Do not rebuild the application or the satellite assembly will be overwritten.</span></span>  
  
     <span data-ttu-id="c3cc0-179">O aplicativo mostra as cadeias de caracteres localizadas em vez de cadeias de caracteres em inglês.</span><span class="sxs-lookup"><span data-stu-id="c3cc0-179">The application shows the localized strings instead of the English strings.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c3cc0-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c3cc0-180">See Also</span></span>  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 [<span data-ttu-id="c3cc0-181">Localizar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="c3cc0-181">Localize an Application</span></span>](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)  
 [<span data-ttu-id="c3cc0-182">Passo a passo: Localizando Windows Forms</span><span class="sxs-lookup"><span data-stu-id="c3cc0-182">Walkthrough: Localizing Windows Forms</span></span>](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5)  
 [<span data-ttu-id="c3cc0-183">Designer do WPF</span><span class="sxs-lookup"><span data-stu-id="c3cc0-183">WPF Designer</span></span>](http://msdn.microsoft.com/en-us/c6c65214-8411-4e16-b254-163ed4099c26)