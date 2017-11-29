---
title: "Como adicionar um ToolStripContainer a um formulário"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toolbars [Windows Forms], built-in rafting
- ToolStrip control [Windows Forms], built-in rafting
- ToolStripContainer control [Windows Forms], adding to Windows Forms
ms.assetid: d0f55095-a833-453e-be5a-644906d75d54
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 5a4089bc6f8ded2c2856318d11b8277811d118c3
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-add-a-toolstripcontainer-to-a-form"></a><span data-ttu-id="c31a0-102">Como adicionar um ToolStripContainer a um formulário</span><span class="sxs-lookup"><span data-stu-id="c31a0-102">How to: Add a ToolStripContainer to a Form</span></span>
<span data-ttu-id="c31a0-103">Você pode adicionar programaticamente um <xref:System.Windows.Forms.ToolStripContainer> a um formulário do Windows e preenchê-lo com controles.</span><span class="sxs-lookup"><span data-stu-id="c31a0-103">You can programmatically add a <xref:System.Windows.Forms.ToolStripContainer> to a Windows Form and populate it with controls.</span></span>  
  
## <a name="example"></a><span data-ttu-id="c31a0-104">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c31a0-104">Example</span></span>  
 <span data-ttu-id="c31a0-105">O exemplo de código a seguir demonstra como adicionar um <xref:System.Windows.Forms.ToolStripContainer> e um <xref:System.Windows.Forms.ToolStrip> para formulários do Windows, como adicionar itens para o <xref:System.Windows.Forms.ToolStrip>e como adicionar o <xref:System.Windows.Forms.ToolStrip> para o <xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanel%2A> do <xref:System.Windows.Forms.ToolStripContainer>.</span><span class="sxs-lookup"><span data-stu-id="c31a0-105">The following code example demonstrates how to add a <xref:System.Windows.Forms.ToolStripContainer> and a <xref:System.Windows.Forms.ToolStrip> to a Windows Forms, how to add items to the <xref:System.Windows.Forms.ToolStrip>, and how to add the <xref:System.Windows.Forms.ToolStrip> to the <xref:System.Windows.Forms.ToolStripContainer.TopToolStripPanel%2A> of the <xref:System.Windows.Forms.ToolStripContainer>.</span></span>  
  
 [!code-csharp[System.Windows.Forms.ToolStripContainer2#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/system.windows.forms.toolstripcontainer2/cs/form1.cs#1)]
 [!code-vb[System.Windows.Forms.ToolStripContainer2#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/system.windows.forms.toolstripcontainer2/vb/form1.vb#1)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="c31a0-106">Compilando o código</span><span class="sxs-lookup"><span data-stu-id="c31a0-106">Compiling the Code</span></span>  
 <span data-ttu-id="c31a0-107">Este exemplo de código requer:</span><span class="sxs-lookup"><span data-stu-id="c31a0-107">This code example requires:</span></span>  
  
-   <span data-ttu-id="c31a0-108">Referências aos assemblies System. Drawing, System. Text e System.</span><span class="sxs-lookup"><span data-stu-id="c31a0-108">References to the System.Drawing, System.Text, and System.Windows.Forms assemblies.</span></span>  
  
 <span data-ttu-id="c31a0-109">Para obter informações sobre como criar este exemplo da linha de comando para [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], consulte [Building from the Command Line](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) (Compilação da linha de comando) ou [Command-line Building With csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md) (Compilação da linha de comando com csc.exe).</span><span class="sxs-lookup"><span data-stu-id="c31a0-109">For information about building this example from the command line for [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] or [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)], see [Building from the Command Line](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) or [Command-line Building With csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).</span></span> <span data-ttu-id="c31a0-110">Também é possível compilar este exemplo em [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] colando o código em um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="c31a0-110">You can also build this example in [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] by pasting the code into a new project.</span></span>  <span data-ttu-id="c31a0-111">Consulte também [como: compilar e executar um exemplo de código completa do Windows Forms usando o Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)) ou [caixa de diálogo de tarefas ToolStripContainer](http://msdn.microsoft.com/library/ms233647\(v=vs.110\)).</span><span class="sxs-lookup"><span data-stu-id="c31a0-111">See also [How to: Compile and Run a Complete Windows Forms Code Example Using Visual Studio](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\)) or [ToolStripContainer Tasks Dialog Box](http://msdn.microsoft.com/library/ms233647\(v=vs.110\)).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c31a0-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c31a0-112">See Also</span></span>  
 <xref:System.Windows.Forms.ToolStripContainer>  
 [<span data-ttu-id="c31a0-113">Controle ToolStripContainer</span><span class="sxs-lookup"><span data-stu-id="c31a0-113">ToolStripContainer Control</span></span>](../../../../docs/framework/winforms/controls/toolstripcontainer-control.md)  
 [<span data-ttu-id="c31a0-114">Controle ToolStrip</span><span class="sxs-lookup"><span data-stu-id="c31a0-114">ToolStrip Control</span></span>](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)