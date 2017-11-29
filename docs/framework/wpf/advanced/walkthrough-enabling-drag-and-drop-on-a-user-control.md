---
title: "Instruções passo a passo: habilitando arrastar e soltar em um controle de usuário"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthrough [WPF], drag-and-drop
- drag-and-drop [WPF], walkthrough
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 360b453b2a25b6822485f18cc81cb43e313949eb
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2017
---
# <a name="walkthrough-enabling-drag-and-drop-on-a-user-control"></a><span data-ttu-id="7ed97-102">Instruções passo a passo: habilitando arrastar e soltar em um controle de usuário</span><span class="sxs-lookup"><span data-stu-id="7ed97-102">Walkthrough: Enabling Drag and Drop on a User Control</span></span>
<span data-ttu-id="7ed97-103">Este passo a passo demonstra como criar um controle de usuário personalizado que pode participar na transferência de dados por arrastar e soltar no [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].</span><span class="sxs-lookup"><span data-stu-id="7ed97-103">This walkthrough demonstrates how to create a custom user control that can participate in drag-and-drop data transfer in [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)].</span></span>  
  
 <span data-ttu-id="7ed97-104">Neste passo a passo, você criará um personalizado WPF <xref:System.Windows.Controls.UserControl> que representa uma forma de círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-104">In this walkthrough, you will create a custom WPF <xref:System.Windows.Controls.UserControl> that represents a circle shape.</span></span> <span data-ttu-id="7ed97-105">Você implementará a funcionalidade no controle para permitir a transferência de dados por meio de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-105">You will implement functionality on the control to enable data transfer through drag-and-drop.</span></span> <span data-ttu-id="7ed97-106">Por exemplo, se você arrastar de um controle do círculo para outro, os dados de cor de preenchimento serão copiados do círculo de origem para o destino.</span><span class="sxs-lookup"><span data-stu-id="7ed97-106">For example, if you drag from one Circle control to another, the Fill color data is copied from the source Circle to the target.</span></span> <span data-ttu-id="7ed97-107">Se você arrastar um controle do círculo para um <xref:System.Windows.Controls.TextBox>, a representação de cadeia de caracteres da cor de preenchimento é copiada para o <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-107">If you drag from a Circle control to a <xref:System.Windows.Controls.TextBox>, the string representation of the Fill color is copied to the <xref:System.Windows.Controls.TextBox>.</span></span> <span data-ttu-id="7ed97-108">Você também criará um pequeno aplicativo que contém dois controles de painel e um <xref:System.Windows.Controls.TextBox> para testar a funcionalidade de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-108">You will also create a small application that contains two panel controls and a <xref:System.Windows.Controls.TextBox> to test the drag-and-drop functionality.</span></span> <span data-ttu-id="7ed97-109">Será gravado um código que permite que os painéis processem os dados do círculo que foram soltos, o que permitirá mover ou copiar círculos da coleção de filhos de um painel para o outro.</span><span class="sxs-lookup"><span data-stu-id="7ed97-109">You will write code that enables the panels to process dropped Circle data, which will enable you to move or copy Circles from the Children collection of one panel to the other.</span></span>  
  
 <span data-ttu-id="7ed97-110">Esta explicação passo a passo ilustra as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-110">This walkthrough illustrates the following tasks:</span></span>  
  
-   <span data-ttu-id="7ed97-111">Crie um controle de usuário personalizado.</span><span class="sxs-lookup"><span data-stu-id="7ed97-111">Create a custom user control.</span></span>  
  
-   <span data-ttu-id="7ed97-112">Habilite o controle de usuário como uma fonte de arrastar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-112">Enable the user control to be a drag source.</span></span>  
  
-   <span data-ttu-id="7ed97-113">Habilite o controle de usuário como um destino de soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-113">Enable the user control to be a drop target.</span></span>  
  
-   <span data-ttu-id="7ed97-114">Habilite um painel para receber dados que foram soltos pelo controle de usuário.</span><span class="sxs-lookup"><span data-stu-id="7ed97-114">Enable a panel to receive data dropped from the user control.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7ed97-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ed97-115">Prerequisites</span></span>  
 <span data-ttu-id="7ed97-116">Você precisa dos seguintes componentes para concluir esta instrução passo a passo:</span><span class="sxs-lookup"><span data-stu-id="7ed97-116">You need the following components to complete this walkthrough:</span></span>  
  
-   <span data-ttu-id="7ed97-117">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="7ed97-117">Visual Studio 2010</span></span>  
  
## <a name="creating-the-application-project"></a><span data-ttu-id="7ed97-118">Criando o projeto de aplicativo</span><span class="sxs-lookup"><span data-stu-id="7ed97-118">Creating the Application Project</span></span>  
 <span data-ttu-id="7ed97-119">Nesta seção, você criará a infraestrutura de aplicativo, que inclui uma página principal com dois painéis e um <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-119">In this section, you will create the application infrastructure, which includes a main page with two panels and a <xref:System.Windows.Controls.TextBox>.</span></span>  
  
### <a name="to-create-the-project"></a><span data-ttu-id="7ed97-120">Para criar o projeto</span><span class="sxs-lookup"><span data-stu-id="7ed97-120">To create the project</span></span>  
  
1.  <span data-ttu-id="7ed97-121">Crie um novo projeto de aplicativo do WPF no Visual Basic ou no Visual C#, chamado `DragDropExample`.</span><span class="sxs-lookup"><span data-stu-id="7ed97-121">Create a new WPF Application project in Visual Basic or Visual C# named `DragDropExample`.</span></span> <span data-ttu-id="7ed97-122">Para obter mais informações, consulte [Como criar um novo projeto de aplicativo do WPF](http://msdn.microsoft.com/en-us/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).</span><span class="sxs-lookup"><span data-stu-id="7ed97-122">For more information, see [How to: Create a New WPF Application Project](http://msdn.microsoft.com/en-us/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).</span></span>  
  
2.  <span data-ttu-id="7ed97-123">Abra MainWindow.xaml.</span><span class="sxs-lookup"><span data-stu-id="7ed97-123">Open MainWindow.xaml.</span></span>  
  
3.  <span data-ttu-id="7ed97-124">Adicione a seguinte marcação entre a abertura e fechamento <xref:System.Windows.Controls.Grid> marcas.</span><span class="sxs-lookup"><span data-stu-id="7ed97-124">Add the following markup between the opening and closing <xref:System.Windows.Controls.Grid> tags.</span></span>  
  
     <span data-ttu-id="7ed97-125">Essa marcação cria a interface do usuário para o aplicativo de teste.</span><span class="sxs-lookup"><span data-stu-id="7ed97-125">This markup creates the user interface for the test application.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#PanelsStep1XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]  
  
## <a name="adding-a-new-user-control-to-the-project"></a><span data-ttu-id="7ed97-126">Adicionando um novo controle de usuário ao projeto</span><span class="sxs-lookup"><span data-stu-id="7ed97-126">Adding a New User Control to the Project</span></span>  
 <span data-ttu-id="7ed97-127">Nesta seção, você adicionará um novo controle de usuário ao projeto.</span><span class="sxs-lookup"><span data-stu-id="7ed97-127">In this section, you will add a new user control to the project.</span></span>  
  
### <a name="to-add-a-new-user-control"></a><span data-ttu-id="7ed97-128">Para adicionar um novo controle de usuário</span><span class="sxs-lookup"><span data-stu-id="7ed97-128">To add a new user control</span></span>  
  
1.  <span data-ttu-id="7ed97-129">No menu Projeto, selecione **Adicionar controle de usuário**.</span><span class="sxs-lookup"><span data-stu-id="7ed97-129">On the Project menu, select **Add User Control**.</span></span>  
  
2.  <span data-ttu-id="7ed97-130">Na caixa de diálogo Adicionar novo item, altere o nome para `Circle.xaml` e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7ed97-130">In the Add New Item dialog box, change the name to `Circle.xaml`, and click **Add**.</span></span>  
  
     <span data-ttu-id="7ed97-131">O Circle.xaml e seu code-behind são adicionados ao projeto.</span><span class="sxs-lookup"><span data-stu-id="7ed97-131">Circle.xaml and its code-behind is added to the project.</span></span>  
  
3.  <span data-ttu-id="7ed97-132">Abra o Circle.xaml.</span><span class="sxs-lookup"><span data-stu-id="7ed97-132">Open Circle.xaml.</span></span>  
  
     <span data-ttu-id="7ed97-133">Esse arquivo conterá os elementos de interface do usuário do controle de usuário.</span><span class="sxs-lookup"><span data-stu-id="7ed97-133">This file will contain the user interface elements of the user control.</span></span>  
  
4.  <span data-ttu-id="7ed97-134">Adicione a seguinte marcação para a raiz <xref:System.Windows.Controls.Grid> para criar um controle de usuário simples que tem um círculo azul como sua interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="7ed97-134">Add the following markup to the root <xref:System.Windows.Controls.Grid> to create a simple user control that has a blue circle as its UI.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#EllipseXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]  
  
5.  <span data-ttu-id="7ed97-135">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-135">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
6.  <span data-ttu-id="7ed97-136">No C#, adicione o código a seguir após o construtor padrão para criar um construtor de cópia.</span><span class="sxs-lookup"><span data-stu-id="7ed97-136">In C#, add the following code after the default constructor to create a copy constructor.</span></span> <span data-ttu-id="7ed97-137">No Visual Basic, adicione o código a seguir para criar um construtor padrão e um construtor de cópia.</span><span class="sxs-lookup"><span data-stu-id="7ed97-137">In Visual Basic, add the following code to create both a default constructor and a copy constructor.</span></span>  
  
     <span data-ttu-id="7ed97-138">Para permitir que o controle de usuário seja copiado, você pode adicionar um método de construtor de cópia no arquivo code-behind.</span><span class="sxs-lookup"><span data-stu-id="7ed97-138">In order to allow the user control to be copied, you add a copy constructor method in the code-behind file.</span></span> <span data-ttu-id="7ed97-139">No controle de usuário simplificado do círculo, será copiado apenas o preenchimento e o tamanho do controle de usuário.</span><span class="sxs-lookup"><span data-stu-id="7ed97-139">In the simplified Circle user control, you will only copy the Fill and the size of the of the user control.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]  
  
### <a name="to-add-the-user-control-to-the-main-window"></a><span data-ttu-id="7ed97-140">Para adicionar o controle de usuário à janela principal</span><span class="sxs-lookup"><span data-stu-id="7ed97-140">To add the user control to the main window</span></span>  
  
1.  <span data-ttu-id="7ed97-141">Abra MainWindow.xaml.</span><span class="sxs-lookup"><span data-stu-id="7ed97-141">Open MainWindow.xaml.</span></span>  
  
2.  <span data-ttu-id="7ed97-142">Adicionar o XAML a seguir para a abertura <xref:System.Windows.Window> marca para criar uma referência de namespace XML para o aplicativo atual.</span><span class="sxs-lookup"><span data-stu-id="7ed97-142">Add the following XAML to the opening <xref:System.Windows.Window> tag to create an XML namespace reference to the current application.</span></span>  
  
    ```  
    xmlns:local="clr-namespace:DragDropExample"  
    ```  
  
3.  <span data-ttu-id="7ed97-143">Na primeira <xref:System.Windows.Controls.StackPanel>, adicionar o XAML a seguir para criar duas instâncias do controle de usuário círculo no primeiro painel.</span><span class="sxs-lookup"><span data-stu-id="7ed97-143">In the first <xref:System.Windows.Controls.StackPanel>, add the following XAML to create two instances of the Circle user control in the first panel.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#CirclesXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]  
  
     <span data-ttu-id="7ed97-144">O XAML completo para o painel tem a aparência a seguir.</span><span class="sxs-lookup"><span data-stu-id="7ed97-144">The full XAML for the panel looks like the following.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#PanelsStep2XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]  
  
## <a name="implementing-drag-source-events-in-the-user-control"></a><span data-ttu-id="7ed97-145">Implementando eventos de origem do arrasto no controle de usuário</span><span class="sxs-lookup"><span data-stu-id="7ed97-145">Implementing Drag Source Events in the User Control</span></span>  
 <span data-ttu-id="7ed97-146">Nesta seção, você substituirá o <xref:System.Windows.UIElement.OnMouseMove%2A> método e iniciar a operação de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-146">In this section, you will override the <xref:System.Windows.UIElement.OnMouseMove%2A> method and initiate the drag-and-drop operation.</span></span>  
  
 <span data-ttu-id="7ed97-147">Se um arraste for iniciado (um botão do mouse é pressionado e o mouse é movido), você incluirá os dados a serem transferidos para um <xref:System.Windows.DataObject>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-147">If a drag is started (a mouse button is pressed and the mouse is moved), you will package the data to be transferred into a <xref:System.Windows.DataObject>.</span></span> <span data-ttu-id="7ed97-148">Nesse caso, o controle do círculo empacotará três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-148">In this case, the Circle control will package three data items; a string representation of its Fill color, a double representation of its height, and a copy of itself.</span></span>  
  
### <a name="to-initiate-a-drag-and-drop-operation"></a><span data-ttu-id="7ed97-149">Para iniciar uma operação do tipo “arrastar e soltar”</span><span class="sxs-lookup"><span data-stu-id="7ed97-149">To initiate a drag-and-drop operation</span></span>  
  
1.  <span data-ttu-id="7ed97-150">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-150">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
2.  <span data-ttu-id="7ed97-151">Adicione o seguinte <xref:System.Windows.UIElement.OnMouseMove%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.MouseMove> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-151">Add the following <xref:System.Windows.UIElement.OnMouseMove%2A> override to provide class handling for the <xref:System.Windows.UIElement.MouseMove> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]  
  
     <span data-ttu-id="7ed97-152">Isso <xref:System.Windows.UIElement.OnMouseMove%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-152">This <xref:System.Windows.UIElement.OnMouseMove%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-153">Verifica se o botão esquerdo do mouse é pressionado enquanto o mouse se move.</span><span class="sxs-lookup"><span data-stu-id="7ed97-153">Checks whether the left mouse button is pressed while the mouse is moving.</span></span>  
  
    -   <span data-ttu-id="7ed97-154">Empacota os dados de círculo em uma <xref:System.Windows.DataObject>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-154">Packages the Circle data into a <xref:System.Windows.DataObject>.</span></span> <span data-ttu-id="7ed97-155">Nesse caso, o controle do círculo empacota três itens de dados; uma representação de cadeia de caracteres da cor de preenchimento, uma representação dupla da altura e uma cópia de si mesmo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-155">In this case, the Circle control packages three data items; a string representation of its Fill color, a double representation of its height, and a copy of itself.</span></span>  
  
    -   <span data-ttu-id="7ed97-156">Chama estático <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> método para iniciar a operação de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-156">Calls the static <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> method to initiate the drag-and-drop operation.</span></span> <span data-ttu-id="7ed97-157">Passe os seguintes três parâmetros para o <xref:System.Windows.DragDrop.DoDragDrop%2A> método:</span><span class="sxs-lookup"><span data-stu-id="7ed97-157">You pass the following three parameters to the <xref:System.Windows.DragDrop.DoDragDrop%2A> method:</span></span>  
  
        -   <span data-ttu-id="7ed97-158">`dragSource` – Uma referência para esse controle.</span><span class="sxs-lookup"><span data-stu-id="7ed97-158">`dragSource` – A reference to this control.</span></span>  
  
        -   <span data-ttu-id="7ed97-159">`data`– A <xref:System.Windows.DataObject> criado no código anterior.</span><span class="sxs-lookup"><span data-stu-id="7ed97-159">`data` – The <xref:System.Windows.DataObject> created in the previous code.</span></span>  
  
        -   <span data-ttu-id="7ed97-160">`allowedEffects`– As operações de arrastar e soltar permitidas, que são <xref:System.Windows.DragDropEffects.Copy> ou <xref:System.Windows.DragDropEffects.Move>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-160">`allowedEffects` – The allowed drag-and-drop operations, which are <xref:System.Windows.DragDropEffects.Copy> or <xref:System.Windows.DragDropEffects.Move>.</span></span>  
  
3.  <span data-ttu-id="7ed97-161">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-161">Press F5 to build and run the application.</span></span>  
  
4.  <span data-ttu-id="7ed97-162">Clique em um dos controles do círculo e arraste-o sobre painéis, o círculo e o <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-162">Click one of the Circle controls and drag it over the panels, the other Circle, and the <xref:System.Windows.Controls.TextBox>.</span></span> <span data-ttu-id="7ed97-163">Ao arrastar sobre o <xref:System.Windows.Controls.TextBox>, o cursor muda para indicar uma movimentação.</span><span class="sxs-lookup"><span data-stu-id="7ed97-163">When dragging over the <xref:System.Windows.Controls.TextBox>, the cursor changes to indicate a move.</span></span>  
  
5.  <span data-ttu-id="7ed97-164">Ao arrastar um círculo sobre o <xref:System.Windows.Controls.TextBox>, pressione a tecla CTRL.</span><span class="sxs-lookup"><span data-stu-id="7ed97-164">While dragging a Circle over the <xref:System.Windows.Controls.TextBox>, press the CTRL key.</span></span> <span data-ttu-id="7ed97-165">Observe como o cursor muda para indicar uma cópia.</span><span class="sxs-lookup"><span data-stu-id="7ed97-165">Notice how the cursor changes to indicate a copy.</span></span>  
  
6.  <span data-ttu-id="7ed97-166">Arraste e solte um círculo para o <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-166">Drag and drop a Circle onto the <xref:System.Windows.Controls.TextBox>.</span></span> <span data-ttu-id="7ed97-167">A representação de cadeia de caracteres da cor de preenchimento do círculo é acrescentada ao <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-167">The string representation of the Circle’s fill color is appended to the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
     <span data-ttu-id="7ed97-168">![Representação de cadeia de caracteres da cor de preenchimento do círculo](../../../../docs/framework/wpf/advanced/media/dragdrop-colorstring.png "DragDrop_ColorString")</span><span class="sxs-lookup"><span data-stu-id="7ed97-168">![String representation of Circle's fill color](../../../../docs/framework/wpf/advanced/media/dragdrop-colorstring.png "DragDrop_ColorString")</span></span>  
  
 <span data-ttu-id="7ed97-169">Por padrão, o cursor será alterado durante uma operação do tipo “arrastar e soltar” para indicar qual será o efeito de soltar os dados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-169">By default, the cursor will change during a drag-and-drop operation to indicate what effect dropping the data will have.</span></span> <span data-ttu-id="7ed97-170">Você pode personalizar os comentários especificados para o usuário manipulando o <xref:System.Windows.UIElement.GiveFeedback> evento e definindo um cursor diferente.</span><span class="sxs-lookup"><span data-stu-id="7ed97-170">You can customize the feedback given to the user by handling the <xref:System.Windows.UIElement.GiveFeedback> event and setting a different cursor.</span></span>  
  
### <a name="to-give-feedback-to-the-user"></a><span data-ttu-id="7ed97-171">Para fornecer comentários ao usuário</span><span class="sxs-lookup"><span data-stu-id="7ed97-171">To give feedback to the user</span></span>  
  
1.  <span data-ttu-id="7ed97-172">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-172">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
2.  <span data-ttu-id="7ed97-173">Adicione o seguinte <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.GiveFeedback> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-173">Add the following <xref:System.Windows.UIElement.OnGiveFeedback%2A> override to provide class handling for the <xref:System.Windows.UIElement.GiveFeedback> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]  
  
     <span data-ttu-id="7ed97-174">Isso <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-174">This <xref:System.Windows.UIElement.OnGiveFeedback%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-175">Verifica o <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valores que são definidos no destino de soltar <xref:System.Windows.UIElement.DragOver> manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-175">Checks the <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> values that are set in the drop target's <xref:System.Windows.UIElement.DragOver> event handler.</span></span>  
  
    -   <span data-ttu-id="7ed97-176">Define um cursor personalizado com base no <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> valor.</span><span class="sxs-lookup"><span data-stu-id="7ed97-176">Sets a custom cursor based on the <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> value.</span></span> <span data-ttu-id="7ed97-177">O cursor deve fornecer comentários visuais ao usuário a respeito de qual será o efeito de soltar os dados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-177">The cursor is intended to give visual feedback to the user about what effect dropping the data will have.</span></span>  
  
3.  <span data-ttu-id="7ed97-178">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-178">Press F5 to build and run the application.</span></span>  
  
4.  <span data-ttu-id="7ed97-179">Arraste um círculo controle sobre os painéis, o círculo, e o <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-179">Drag one of the Circle controls over the panels, the other Circle, and the <xref:System.Windows.Controls.TextBox>.</span></span> <span data-ttu-id="7ed97-180">Observe que os cursores agora são os cursores personalizados que você especificou no <xref:System.Windows.UIElement.OnGiveFeedback%2A> substituir.</span><span class="sxs-lookup"><span data-stu-id="7ed97-180">Notice that the cursors are now the custom cursors that you specified in the <xref:System.Windows.UIElement.OnGiveFeedback%2A> override.</span></span>  
  
     <span data-ttu-id="7ed97-181">![Arraste e solte com os cursores personalizados](../../../../docs/framework/wpf/advanced/media/dragdrop-customcursor.png "DragDrop_CustomCursor")</span><span class="sxs-lookup"><span data-stu-id="7ed97-181">![Drag and drop with custom cursors](../../../../docs/framework/wpf/advanced/media/dragdrop-customcursor.png "DragDrop_CustomCursor")</span></span>  
  
5.  <span data-ttu-id="7ed97-182">Selecione o texto `green` do <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-182">Select the text `green` from the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
6.  <span data-ttu-id="7ed97-183">Arraste o texto `green` para um controle do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-183">Drag the `green` text to a Circle control.</span></span> <span data-ttu-id="7ed97-184">Observe que os cursores padrão são mostrados para indicar os efeitos da operação do tipo “arrastar e soltar”.</span><span class="sxs-lookup"><span data-stu-id="7ed97-184">Notice that the default cursors are shown to indicate the effects of the drag-and-drop operation.</span></span> <span data-ttu-id="7ed97-185">O cursor de comentários sempre é definido pela fonte de arrastar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-185">The feedback cursor is always set by the drag source.</span></span>  
  
## <a name="implementing-drop-target-events-in-the-user-control"></a><span data-ttu-id="7ed97-186">Implementando eventos de destino de soltar no controle de usuário</span><span class="sxs-lookup"><span data-stu-id="7ed97-186">Implementing Drop Target Events in the User Control</span></span>  
 <span data-ttu-id="7ed97-187">Nesta seção, você especificará que o controle de usuário é um destino de soltar, substituirá os métodos que permitem que o controle de usuário seja um destino de soltar e processará os dados soltos nele.</span><span class="sxs-lookup"><span data-stu-id="7ed97-187">In this section, you will specify that the user control is a drop target, override the methods that enable the user control to be a drop target, and process the data that is dropped on it.</span></span>  
  
### <a name="to-enable-the-user-control-to-be-a-drop-target"></a><span data-ttu-id="7ed97-188">Para permitir que o controle de usuário seja um destino de soltar</span><span class="sxs-lookup"><span data-stu-id="7ed97-188">To enable the user control to be a drop target</span></span>  
  
1.  <span data-ttu-id="7ed97-189">Abra o Circle.xaml.</span><span class="sxs-lookup"><span data-stu-id="7ed97-189">Open Circle.xaml.</span></span>  
  
2.  <span data-ttu-id="7ed97-190">Na abertura <xref:System.Windows.Controls.UserControl> marca, adicione o <xref:System.Windows.UIElement.AllowDrop%2A> propriedade e defina-a como `true`.</span><span class="sxs-lookup"><span data-stu-id="7ed97-190">In the opening <xref:System.Windows.Controls.UserControl> tag, add the <xref:System.Windows.UIElement.AllowDrop%2A> property and set it to `true`.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#UCTagXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]  
  
 <span data-ttu-id="7ed97-191">O <xref:System.Windows.UIElement.OnDrop%2A> método é chamado quando o <xref:System.Windows.UIElement.AllowDrop%2A> está definida como `true` e dados de origem do arrasto são arrastados para o controle de usuário do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-191">The <xref:System.Windows.UIElement.OnDrop%2A> method is called when the <xref:System.Windows.UIElement.AllowDrop%2A> property is set to `true` and data from the drag source is dropped on the Circle user control.</span></span> <span data-ttu-id="7ed97-192">Nesse método, você processará os dados que foram soltos e aplicará os dados ao círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-192">In this method, you will process the data that was dropped and apply the data to the Circle.</span></span>  
  
### <a name="to-process-the-dropped-data"></a><span data-ttu-id="7ed97-193">Para processar os dados soltos</span><span class="sxs-lookup"><span data-stu-id="7ed97-193">To process the dropped data</span></span>  
  
1.  <span data-ttu-id="7ed97-194">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-194">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
2.  <span data-ttu-id="7ed97-195">Adicione o seguinte <xref:System.Windows.UIElement.OnDrop%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.Drop> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-195">Add the following <xref:System.Windows.UIElement.OnDrop%2A> override to provide class handling for the <xref:System.Windows.UIElement.Drop> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]  
  
     <span data-ttu-id="7ed97-196">Isso <xref:System.Windows.UIElement.OnDrop%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-196">This <xref:System.Windows.UIElement.OnDrop%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-197">Usa o <xref:System.Windows.DataObject.GetDataPresent%2A> método para verificar se os dados arrastados contém um objeto de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7ed97-197">Uses the <xref:System.Windows.DataObject.GetDataPresent%2A> method to check if the dragged data contains a string object.</span></span>  
  
    -   <span data-ttu-id="7ed97-198">Usa o <xref:System.Windows.DataObject.GetData%2A> método para extrair os dados de cadeia de caracteres se ele estiver presente.</span><span class="sxs-lookup"><span data-stu-id="7ed97-198">Uses the <xref:System.Windows.DataObject.GetData%2A> method to extract the string data if it is present.</span></span>  
  
    -   <span data-ttu-id="7ed97-199">Usa um <xref:System.Windows.Media.BrushConverter> ao tentar converter a cadeia de caracteres para um <xref:System.Windows.Media.Brush>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-199">Uses a <xref:System.Windows.Media.BrushConverter> to try to convert the string to a <xref:System.Windows.Media.Brush>.</span></span>  
  
    -   <span data-ttu-id="7ed97-200">Se a conversão for bem-sucedida, o pincel aplica-se a <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse> que fornece a interface do usuário do controle do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-200">If the conversion is successful, applies the brush to the <xref:System.Windows.Shapes.Shape.Fill%2A> of the <xref:System.Windows.Shapes.Ellipse> that provides the UI of the Circle control.</span></span>  
  
    -   <span data-ttu-id="7ed97-201">Marcas de <xref:System.Windows.UIElement.Drop> eventos tratados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-201">Marks the <xref:System.Windows.UIElement.Drop> event as handled.</span></span> <span data-ttu-id="7ed97-202">O evento de soltar deve ser marcado como manipulado para que os outros elementos que o recebem saibam que foi manipulado pelo controle de usuário do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-202">You should mark the drop event as handled so that other elements that receive this event know that the Circle user control handled it.</span></span>  
  
3.  <span data-ttu-id="7ed97-203">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-203">Press F5 to build and run the application.</span></span>  
  
4.  <span data-ttu-id="7ed97-204">Selecione o texto `green` no <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-204">Select the text `green` in the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
5.  <span data-ttu-id="7ed97-205">Arraste o texto para um controle do círculo e solte-o.</span><span class="sxs-lookup"><span data-stu-id="7ed97-205">Drag the text to a Circle control and drop it.</span></span> <span data-ttu-id="7ed97-206">O círculo muda de azul para verde.</span><span class="sxs-lookup"><span data-stu-id="7ed97-206">The Circle changes from blue to green.</span></span>  
  
     <span data-ttu-id="7ed97-207">![Converta uma cadeia de caracteres em um pincel](../../../../docs/framework/wpf/advanced/media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")</span><span class="sxs-lookup"><span data-stu-id="7ed97-207">![Convert a string to a brush](../../../../docs/framework/wpf/advanced/media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")</span></span>  
  
6.  <span data-ttu-id="7ed97-208">Digite o texto `green` no <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-208">Type the text `green` in the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
7.  <span data-ttu-id="7ed97-209">Selecione o texto `gre` no <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-209">Select the text `gre` in the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
8.  <span data-ttu-id="7ed97-210">Arraste-o para um controle do círculo e solte-o.</span><span class="sxs-lookup"><span data-stu-id="7ed97-210">Drag it to a Circle control and drop it.</span></span> <span data-ttu-id="7ed97-211">Observe que o cursor muda para indicar que é permitido soltar; porém, a cor do círculo não muda, porque `gre` não é uma cor válida.</span><span class="sxs-lookup"><span data-stu-id="7ed97-211">Notice that the cursor changes to indicate that the drop is allowed, but the color of the Circle does not change because `gre` is not a valid color.</span></span>  
  
9. <span data-ttu-id="7ed97-212">Arraste do controle do círculo verde e solte no controle do círculo azul.</span><span class="sxs-lookup"><span data-stu-id="7ed97-212">Drag from the green Circle control and drop on the blue Circle control.</span></span> <span data-ttu-id="7ed97-213">O círculo muda de azul para verde.</span><span class="sxs-lookup"><span data-stu-id="7ed97-213">The Circle changes from blue to green.</span></span> <span data-ttu-id="7ed97-214">Observe que o cursor é mostrado depende se o <xref:System.Windows.Controls.TextBox> ou o círculo é a origem do arrasto.</span><span class="sxs-lookup"><span data-stu-id="7ed97-214">Notice that which cursor is shown depends on whether the <xref:System.Windows.Controls.TextBox> or the Circle is the drag source.</span></span>  
  
 <span data-ttu-id="7ed97-215">Definindo o <xref:System.Windows.UIElement.AllowDrop%2A> propriedade `true` e processamento de dados descartados é tudo o que é necessário para habilitar um elemento seja um destino de soltar.</span><span class="sxs-lookup"><span data-stu-id="7ed97-215">Setting the <xref:System.Windows.UIElement.AllowDrop%2A> property to `true` and processing the dropped data is all that is required to enable an element to be a drop target.</span></span> <span data-ttu-id="7ed97-216">No entanto, para fornecer uma melhor experiência de usuário, você deve também tratar o <xref:System.Windows.UIElement.DragEnter>, <xref:System.Windows.UIElement.DragLeave>, e <xref:System.Windows.UIElement.DragOver> eventos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-216">However, to provide a better user experience, you should also handle the <xref:System.Windows.UIElement.DragEnter>, <xref:System.Windows.UIElement.DragLeave>, and <xref:System.Windows.UIElement.DragOver> events.</span></span> <span data-ttu-id="7ed97-217">Nesses eventos, é possível executar verificações e fornecer comentários adicionais ao usuário antes de soltar os dados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-217">In these events, you can perform checks and provide additional feedback to the user before the data is dropped.</span></span>  
  
 <span data-ttu-id="7ed97-218">Quando dados são arrastados sobre o controle de usuário do círculo, o controle deve notificar a fonte de arrasto se os dados arrastados podem ser processados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-218">When data is dragged over the Circle user control, the control should notify the drag source whether it can process the data that is being dragged.</span></span> <span data-ttu-id="7ed97-219">Se o controle não souber como processar os dados, deverá recusá-los quando forem soltos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-219">If the control does not know how to process the data, it should refuse the drop.</span></span> <span data-ttu-id="7ed97-220">Para fazer isso, você irá manipular o <xref:System.Windows.UIElement.DragOver> evento e defina o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="7ed97-220">To do this, you will handle the <xref:System.Windows.UIElement.DragOver> event and set the <xref:System.Windows.DragEventArgs.Effects%2A> property.</span></span>  
  
### <a name="to-verify-that-the-data-drop-is-allowed"></a><span data-ttu-id="7ed97-221">Para verificar se é permitido soltar os dados</span><span class="sxs-lookup"><span data-stu-id="7ed97-221">To verify that the data drop is allowed</span></span>  
  
1.  <span data-ttu-id="7ed97-222">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-222">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
2.  <span data-ttu-id="7ed97-223">Adicione o seguinte <xref:System.Windows.UIElement.OnDragOver%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragOver> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-223">Add the following <xref:System.Windows.UIElement.OnDragOver%2A> override to provide class handling for the <xref:System.Windows.UIElement.DragOver> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]  
  
     <span data-ttu-id="7ed97-224">Isso <xref:System.Windows.UIElement.OnDragOver%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-224">This <xref:System.Windows.UIElement.OnDragOver%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-225">Define a propriedade <xref:System.Windows.DragEventArgs.Effects%2A> como <xref:System.Windows.DragDropEffects.None>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-225">Sets the <xref:System.Windows.DragEventArgs.Effects%2A> property to <xref:System.Windows.DragDropEffects.None>.</span></span>  
  
    -   <span data-ttu-id="7ed97-226">Executa as mesmas verificações são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se o controle de usuário do círculo pode processar os dados arrastados.</span><span class="sxs-lookup"><span data-stu-id="7ed97-226">Performs the same checks that are performed in the <xref:System.Windows.UIElement.OnDrop%2A> method to determine whether the Circle user control can process the dragged data.</span></span>  
  
    -   <span data-ttu-id="7ed97-227">Se o controle de usuário pode processar os dados, define o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Copy> ou <xref:System.Windows.DragDropEffects.Move>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-227">If the user control can process the data, sets the <xref:System.Windows.DragEventArgs.Effects%2A> property to <xref:System.Windows.DragDropEffects.Copy> or <xref:System.Windows.DragDropEffects.Move>.</span></span>  
  
3.  <span data-ttu-id="7ed97-228">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-228">Press F5 to build and run the application.</span></span>  
  
4.  <span data-ttu-id="7ed97-229">Selecione o texto `gre` no <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-229">Select the text `gre` in the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
5.  <span data-ttu-id="7ed97-230">Arraste o texto para um controle do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-230">Drag the text to a Circle control.</span></span> <span data-ttu-id="7ed97-231">Observe que, agora, o cursor muda para indicar que não é permitido soltar, porque `gre` não é uma cor válida.</span><span class="sxs-lookup"><span data-stu-id="7ed97-231">Notice that the cursor now changes to indicate that the drop is not allowed because `gre` is not a valid color.</span></span>  
  
 <span data-ttu-id="7ed97-232">É possível aprimorar ainda mais a experiência do usuário por meio da aplicação de uma visualização da operação do tipo “soltar”.</span><span class="sxs-lookup"><span data-stu-id="7ed97-232">You can further enhance the user experience by applying a preview of the drop operation.</span></span> <span data-ttu-id="7ed97-233">Para o controle de usuário do círculo, você substituirá o <xref:System.Windows.UIElement.OnDragEnter%2A> e <xref:System.Windows.UIElement.OnDragLeave%2A> métodos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-233">For the Circle user control, you will override the <xref:System.Windows.UIElement.OnDragEnter%2A> and <xref:System.Windows.UIElement.OnDragLeave%2A> methods.</span></span> <span data-ttu-id="7ed97-234">Quando os dados são arrastados sobre o controle, o plano de fundo atual <xref:System.Windows.Shapes.Shape.Fill%2A> é salvo em uma variável de espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="7ed97-234">When the data is dragged over the control, the current background <xref:System.Windows.Shapes.Shape.Fill%2A> is saved in a placeholder variable.</span></span> <span data-ttu-id="7ed97-235">A cadeia de caracteres é convertida em um pincel e aplicada para o <xref:System.Windows.Shapes.Ellipse> que fornece o círculo interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="7ed97-235">The string is then converted to a brush and applied to the <xref:System.Windows.Shapes.Ellipse> that provides the Circle's UI.</span></span> <span data-ttu-id="7ed97-236">Se os dados são arrastados para fora do círculo sem queda original <xref:System.Windows.Shapes.Shape.Fill%2A> valor novamente é aplicado ao círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-236">If the data is dragged out of the Circle without being dropped, the original <xref:System.Windows.Shapes.Shape.Fill%2A> value is re-applied to the Circle.</span></span>  
  
### <a name="to-preview-the-effects-of-the-drag-and-drop-operation"></a><span data-ttu-id="7ed97-237">Para visualizar os efeitos da operação do tipo “arrastar e soltar”</span><span class="sxs-lookup"><span data-stu-id="7ed97-237">To preview the effects of the drag-and-drop operation</span></span>  
  
1.  <span data-ttu-id="7ed97-238">Abra Circle.xaml.cs ou Circle.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-238">Open Circle.xaml.cs or Circle.xaml.vb.</span></span>  
  
2.  <span data-ttu-id="7ed97-239">Na classe do círculo, declarar uma particular <xref:System.Windows.Media.Brush> variável chamada `_previousFill` e inicializá-lo para `null`.</span><span class="sxs-lookup"><span data-stu-id="7ed97-239">In the Circle class, declare a private <xref:System.Windows.Media.Brush> variable named `_previousFill` and initialize it to `null`.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#Brush](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]  
  
3.  <span data-ttu-id="7ed97-240">Adicione o seguinte <xref:System.Windows.UIElement.OnDragEnter%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragEnter> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-240">Add the following <xref:System.Windows.UIElement.OnDragEnter%2A> override to provide class handling for the <xref:System.Windows.UIElement.DragEnter> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]  
  
     <span data-ttu-id="7ed97-241">Isso <xref:System.Windows.UIElement.OnDragEnter%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-241">This <xref:System.Windows.UIElement.OnDragEnter%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-242">Salva o <xref:System.Windows.Shapes.Shape.Fill%2A> propriedade o <xref:System.Windows.Shapes.Ellipse> no `_previousFill` variável.</span><span class="sxs-lookup"><span data-stu-id="7ed97-242">Saves the <xref:System.Windows.Shapes.Shape.Fill%2A> property of the <xref:System.Windows.Shapes.Ellipse> in the `_previousFill` variable.</span></span>  
  
    -   <span data-ttu-id="7ed97-243">Executa as mesmas verificações são executadas no <xref:System.Windows.UIElement.OnDrop%2A> método para determinar se os dados podem ser convertidos em um <xref:System.Windows.Media.Brush>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-243">Performs the same checks that are performed in the <xref:System.Windows.UIElement.OnDrop%2A> method to determine whether the data can be converted to a <xref:System.Windows.Media.Brush>.</span></span>  
  
    -   <span data-ttu-id="7ed97-244">Se os dados são convertidos para um válida <xref:System.Windows.Media.Brush>, aplica-se para o <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-244">If the data is converted to a valid <xref:System.Windows.Media.Brush>, applies it to the <xref:System.Windows.Shapes.Shape.Fill%2A> of the <xref:System.Windows.Shapes.Ellipse>.</span></span>  
  
4.  <span data-ttu-id="7ed97-245">Adicione o seguinte <xref:System.Windows.UIElement.OnDragLeave%2A> substituição para fornecer manipulação de classe para o <xref:System.Windows.UIElement.DragLeave> evento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-245">Add the following <xref:System.Windows.UIElement.OnDragLeave%2A> override to provide class handling for the <xref:System.Windows.UIElement.DragLeave> event.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]  
  
     <span data-ttu-id="7ed97-246">Isso <xref:System.Windows.UIElement.OnDragLeave%2A> substituição executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-246">This <xref:System.Windows.UIElement.OnDragLeave%2A> override performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-247">Aplica-se a <xref:System.Windows.Media.Brush> salvo no `_previousFill` variável para o <xref:System.Windows.Shapes.Shape.Fill%2A> do <xref:System.Windows.Shapes.Ellipse> que fornece a interface do usuário do controle de usuário do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-247">Applies the <xref:System.Windows.Media.Brush> saved in the `_previousFill` variable to the <xref:System.Windows.Shapes.Shape.Fill%2A> of the <xref:System.Windows.Shapes.Ellipse> that provides the UI of the Circle user control.</span></span>  
  
5.  <span data-ttu-id="7ed97-248">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-248">Press F5 to build and run the application.</span></span>  
  
6.  <span data-ttu-id="7ed97-249">Selecione o texto `green` no <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-249">Select the text `green` in the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
7.  <span data-ttu-id="7ed97-250">Arraste o texto sobre um controle do círculo sem soltá-lo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-250">Drag the text over a Circle control without dropping it.</span></span> <span data-ttu-id="7ed97-251">O círculo muda de azul para verde.</span><span class="sxs-lookup"><span data-stu-id="7ed97-251">The Circle changes from blue to green.</span></span>  
  
     <span data-ttu-id="7ed97-252">![Visualize os efeitos de uma operação do tipo “arrastar&#45;e&#45;soltar”](../../../../docs/framework/wpf/advanced/media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")</span><span class="sxs-lookup"><span data-stu-id="7ed97-252">![Preview the effects of a drag&#45;and&#45;drop operation](../../../../docs/framework/wpf/advanced/media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")</span></span>  
  
8.  <span data-ttu-id="7ed97-253">Arraste o texto para fora do controle do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-253">Drag the text away from the Circle control.</span></span> <span data-ttu-id="7ed97-254">O círculo volta de verde para azul.</span><span class="sxs-lookup"><span data-stu-id="7ed97-254">The Circle changes from green back to blue.</span></span>  
  
## <a name="enabling-a-panel-to-receive-dropped-data"></a><span data-ttu-id="7ed97-255">Permitindo que um painel receba dados que foram soltos</span><span class="sxs-lookup"><span data-stu-id="7ed97-255">Enabling a Panel to Receive Dropped Data</span></span>  
 <span data-ttu-id="7ed97-256">Nesta seção, você permitirá que os painéis que hospedam os controles de usuário do círculo funcionem como destinos de soltar para os dados arrastados do círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-256">In this section, you will enable the panels that host the Circle user controls to act as drop targets for dragged Circle data.</span></span> <span data-ttu-id="7ed97-257">Você implementará o código que permite mover um círculo de um painel para outro ou fazer uma cópia de um controle do círculo, mantendo a tecla CTRL pressionada enquanto arrasta e solta em um círculo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-257">You will implement code that enables you to move a Circle from one panel to another, or to make a copy of a Circle control by holding down the CTRL key while dragging and dropping a Circle.</span></span>  
  
### <a name="to-enable-the-panel-to-be-a-drop-target"></a><span data-ttu-id="7ed97-258">Para permitir que o painel seja um destino de soltar</span><span class="sxs-lookup"><span data-stu-id="7ed97-258">To enable the panel to be a drop target</span></span>  
  
1.  <span data-ttu-id="7ed97-259">Abra MainWindow.xaml.</span><span class="sxs-lookup"><span data-stu-id="7ed97-259">Open MainWindow.xaml.</span></span>  
  
2.  <span data-ttu-id="7ed97-260">Como mostra o XAML a seguir, em cada uma da <xref:System.Windows.Controls.StackPanel> controles, adicionar manipuladores para o <xref:System.Windows.UIElement.DragOver> e <xref:System.Windows.UIElement.Drop> eventos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-260">As shown in the following XAML, in each of the <xref:System.Windows.Controls.StackPanel> controls, add handlers for the <xref:System.Windows.UIElement.DragOver> and <xref:System.Windows.UIElement.Drop> events.</span></span> <span data-ttu-id="7ed97-261">Nome do <xref:System.Windows.UIElement.DragOver> manipulador de eventos, `panel_DragOver`e nomeie o <xref:System.Windows.UIElement.Drop> manipulador de eventos, `panel_Drop`.</span><span class="sxs-lookup"><span data-stu-id="7ed97-261">Name the <xref:System.Windows.UIElement.DragOver> event handler, `panel_DragOver`, and name the <xref:System.Windows.UIElement.Drop> event handler, `panel_Drop`.</span></span>  
  
     [!code-xaml[DragDropWalkthrough#PanelsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]  
  
3.  <span data-ttu-id="7ed97-262">Abra MainWindows.xaml.cs ou MainWindow.xaml.vb.</span><span class="sxs-lookup"><span data-stu-id="7ed97-262">Open MainWindows.xaml.cs or MainWindow.xaml.vb.</span></span>  
  
4.  <span data-ttu-id="7ed97-263">Adicione o seguinte código para o <xref:System.Windows.UIElement.DragOver> manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-263">Add the following code for the <xref:System.Windows.UIElement.DragOver> event handler.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]  
  
     <span data-ttu-id="7ed97-264">Isso <xref:System.Windows.UIElement.DragOver> manipulador de eventos executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-264">This <xref:System.Windows.UIElement.DragOver> event handler performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-265">Verifica se os dados arrastados contém os dados de "Objeto" que foi empacotados no <xref:System.Windows.DataObject> pelo controle de usuário círculo e passado na chamada para <xref:System.Windows.DragDrop.DoDragDrop%2A>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-265">Checks that the dragged data contains the "Object" data that was packaged in the <xref:System.Windows.DataObject> by the Circle user control and passed in the call to <xref:System.Windows.DragDrop.DoDragDrop%2A>.</span></span>  
  
    -   <span data-ttu-id="7ed97-266">Se os dados do “objeto” estiverem presentes, verifica se a tecla CTRL está pressionada.</span><span class="sxs-lookup"><span data-stu-id="7ed97-266">If the "Object" data is present, checks whether the CTRL key is pressed.</span></span>  
  
    -   <span data-ttu-id="7ed97-267">Se for pressionada a tecla CTRL, define o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Copy>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-267">If the CTRL key is pressed, sets the <xref:System.Windows.DragEventArgs.Effects%2A> property to <xref:System.Windows.DragDropEffects.Copy>.</span></span> <span data-ttu-id="7ed97-268">Caso contrário, defina o <xref:System.Windows.DragEventArgs.Effects%2A> propriedade <xref:System.Windows.DragDropEffects.Move>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-268">Otherwise, set the <xref:System.Windows.DragEventArgs.Effects%2A> property to <xref:System.Windows.DragDropEffects.Move>.</span></span>  
  
5.  <span data-ttu-id="7ed97-269">Adicione o seguinte código para o <xref:System.Windows.UIElement.Drop> manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="7ed97-269">Add the following code for the <xref:System.Windows.UIElement.Drop> event handler.</span></span>  
  
     [!code-csharp[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]  
  
     <span data-ttu-id="7ed97-270">Isso <xref:System.Windows.UIElement.Drop> manipulador de eventos executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="7ed97-270">This <xref:System.Windows.UIElement.Drop> event handler performs the following tasks:</span></span>  
  
    -   <span data-ttu-id="7ed97-271">Verifica se o <xref:System.Windows.UIElement.Drop> evento já foi tratado.</span><span class="sxs-lookup"><span data-stu-id="7ed97-271">Checks whether the <xref:System.Windows.UIElement.Drop> event has already been handled.</span></span> <span data-ttu-id="7ed97-272">Por exemplo, se um círculo é solto em outro círculo que identificadores o <xref:System.Windows.UIElement.Drop> evento, você não quiser que o painel que contém o círculo para manipulá-lo também.</span><span class="sxs-lookup"><span data-stu-id="7ed97-272">For instance, if a Circle is dropped on another Circle which handles the <xref:System.Windows.UIElement.Drop> event, you do not want the panel that contains the Circle to also handle it.</span></span>  
  
    -   <span data-ttu-id="7ed97-273">Se o <xref:System.Windows.UIElement.Drop> evento não é tratado, verifica se a tecla CTRL pressionada.</span><span class="sxs-lookup"><span data-stu-id="7ed97-273">If the <xref:System.Windows.UIElement.Drop> event is not handled, checks whether the CTRL key is pressed.</span></span>  
  
    -   <span data-ttu-id="7ed97-274">Se a tecla CTRL foi pressionada quando o <xref:System.Windows.UIElement.Drop> acontece, faz uma cópia do círculo controla e adicioná-lo para o <xref:System.Windows.Controls.Panel.Children%2A> coleção do <xref:System.Windows.Controls.StackPanel>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-274">If the CTRL key is pressed when the <xref:System.Windows.UIElement.Drop> happens, makes a copy of the Circle control and add it to the <xref:System.Windows.Controls.Panel.Children%2A> collection of the <xref:System.Windows.Controls.StackPanel>.</span></span>  
  
    -   <span data-ttu-id="7ed97-275">Se não for pressionada a tecla CTRL, move o círculo do <xref:System.Windows.Controls.Panel.Children%2A> coleção de seu painel pai para o <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel que ele foi removido.</span><span class="sxs-lookup"><span data-stu-id="7ed97-275">If the CTRL key is not pressed, moves the Circle from the <xref:System.Windows.Controls.Panel.Children%2A> collection of its parent panel to the <xref:System.Windows.Controls.Panel.Children%2A> collection of the panel that it was dropped on.</span></span>  
  
    -   <span data-ttu-id="7ed97-276">Conjuntos de <xref:System.Windows.DragEventArgs.Effects%2A> propriedade para notificar o <xref:System.Windows.DragDrop.DoDragDrop%2A> método se uma operação de mover ou copiar foi executada.</span><span class="sxs-lookup"><span data-stu-id="7ed97-276">Sets the <xref:System.Windows.DragEventArgs.Effects%2A> property to notify the <xref:System.Windows.DragDrop.DoDragDrop%2A> method whether a move or copy operation was performed.</span></span>  
  
6.  <span data-ttu-id="7ed97-277">Pressione F5 para compilar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7ed97-277">Press F5 to build and run the application.</span></span>  
  
7.  <span data-ttu-id="7ed97-278">Selecione o texto `green` do <xref:System.Windows.Controls.TextBox>.</span><span class="sxs-lookup"><span data-stu-id="7ed97-278">Select the text `green` from the <xref:System.Windows.Controls.TextBox>.</span></span>  
  
8.  <span data-ttu-id="7ed97-279">Arraste o texto sobre um controle do círculo e solte-o.</span><span class="sxs-lookup"><span data-stu-id="7ed97-279">Drag the text over a Circle control and drop it.</span></span>  
  
9. <span data-ttu-id="7ed97-280">Arraste um controle do círculo do painel esquerdo para o painel direito e solte-o.</span><span class="sxs-lookup"><span data-stu-id="7ed97-280">Drag a Circle control from the left panel to the right panel and drop it.</span></span> <span data-ttu-id="7ed97-281">O círculo é removido do <xref:System.Windows.Controls.Panel.Children%2A> coleção do painel esquerdo e adicionado à coleção de filhos do painel à direita.</span><span class="sxs-lookup"><span data-stu-id="7ed97-281">The Circle is removed from the <xref:System.Windows.Controls.Panel.Children%2A> collection of the left panel and added to the Children collection of the right panel.</span></span>  
  
10. <span data-ttu-id="7ed97-282">Arraste um controle do círculo do painel em que está para o outro painel e solte-o enquanto pressiona a tecla CTRL.</span><span class="sxs-lookup"><span data-stu-id="7ed97-282">Drag a Circle control from the panel it is in to the other panel and drop it while pressing the CTRL key.</span></span> <span data-ttu-id="7ed97-283">Círculo é copiado e a cópia é adicionada para o <xref:System.Windows.Controls.Panel.Children%2A> conjunto do painel de recebimento.</span><span class="sxs-lookup"><span data-stu-id="7ed97-283">The Circle is copied and the copy is added to the <xref:System.Windows.Controls.Panel.Children%2A> collection of the receiving panel.</span></span>  
  
     <span data-ttu-id="7ed97-284">![Arrastando um círculo enquanto pressiona a tecla CTRL](../../../../docs/framework/wpf/advanced/media/dragdrop-paneldrop.png "DragDrop_PanelDrop")</span><span class="sxs-lookup"><span data-stu-id="7ed97-284">![Dragging a Circle while pressing the CTRL key](../../../../docs/framework/wpf/advanced/media/dragdrop-paneldrop.png "DragDrop_PanelDrop")</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7ed97-285">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7ed97-285">See Also</span></span>  
 [<span data-ttu-id="7ed97-286">Visão geral de arrastar e soltar</span><span class="sxs-lookup"><span data-stu-id="7ed97-286">Drag and Drop Overview</span></span>](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)