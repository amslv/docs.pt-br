---
title: Como abrir um arquivo solto em um controle RichTextBox
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
- drag-and-drop [WPF], RichTextBox
- RichTextBox [WPF], drag-and-drop
- drag-and-drop [WPF], open a dropped file
ms.assetid: 6bb8bb54-f576-41db-a9a7-24102ddeb490
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: f65ecaf9c6ef34176967e1ebf9134ceee195036b
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-open-a-file-that-is-dropped-on-a-richtextbox-control"></a><span data-ttu-id="42d1c-102">Como abrir um arquivo solto em um controle RichTextBox</span><span class="sxs-lookup"><span data-stu-id="42d1c-102">How to: Open a File That is Dropped on a RichTextBox Control</span></span>
<span data-ttu-id="42d1c-103">Em [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], o <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox>, e <xref:System.Windows.Documents.FlowDocument> todos os controles têm a funcionalidade de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="42d1c-103">In [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)], the <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox>, and <xref:System.Windows.Documents.FlowDocument> controls all have built-in drag-and-drop functionality.</span></span> <span data-ttu-id="42d1c-104">A funcionalidade interna permite arrastar e soltar o texto dentro e entre os controles.</span><span class="sxs-lookup"><span data-stu-id="42d1c-104">The built-in functionality enables drag-and-drop of text within and between the controls.</span></span> <span data-ttu-id="42d1c-105">No entanto, ela não habilita a abertura de um arquivo soltando-o no controle.</span><span class="sxs-lookup"><span data-stu-id="42d1c-105">However, it does not enable opening a file by dropping the file on the control.</span></span> <span data-ttu-id="42d1c-106">Esses controles também marcam os eventos do tipo "arrastar e soltar" como manipulados.</span><span class="sxs-lookup"><span data-stu-id="42d1c-106">These controls also mark the drag-and-drop events as handled.</span></span> <span data-ttu-id="42d1c-107">Como resultado, por padrão, não é possível adicionar seus próprios manipuladores de eventos para fornecer funcionalidade para abrir os arquivos soltos.</span><span class="sxs-lookup"><span data-stu-id="42d1c-107">As a result, by default, you cannot add your own event handlers to provide functionality to open dropped files.</span></span>  
  
 <span data-ttu-id="42d1c-108">Para adicionar um tratamento adicional para eventos de arrastar e soltar nesses controles, use o <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> método para adicionar os manipuladores de eventos para os eventos de arrastar e soltar.</span><span class="sxs-lookup"><span data-stu-id="42d1c-108">To add additional handling for drag-and-drop events in these controls, use the <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> method to add your event handlers for the drag-and-drop events.</span></span> <span data-ttu-id="42d1c-109">Defina o parâmetro `handledEventsToo` para `true` para que o manipulador especificado seja invocado para um evento roteados que já tenham sido marcado como manipulados por outro elemento na rota de evento.</span><span class="sxs-lookup"><span data-stu-id="42d1c-109">Set the `handledEventsToo` parameter to `true` to have the specified handler be invoked for a routed event that has already been marked as handled by another element along the event route.</span></span>  
  
> [!TIP]
>  <span data-ttu-id="42d1c-110">Você pode substituir a funcionalidade de arrastar e soltar interna de <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox>, e <xref:System.Windows.Documents.FlowDocument> tratando as versões de visualização dos eventos de arrastar e soltar e marcar os eventos como tratado.</span><span class="sxs-lookup"><span data-stu-id="42d1c-110">You can replace the built-in drag-and-drop functionality of <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox>, and <xref:System.Windows.Documents.FlowDocument> by handling the preview versions of the drag-and-drop events and marking the preview events as handled.</span></span> <span data-ttu-id="42d1c-111">No entanto, isso desabilitará a funcionalidade interna do tipo "arrastar e soltar", o que não é recomendado.</span><span class="sxs-lookup"><span data-stu-id="42d1c-111">However, this will disable the built-in drag-and-drop functionality, and is not recommended.</span></span>  
  
## <a name="example"></a><span data-ttu-id="42d1c-112">Exemplo</span><span class="sxs-lookup"><span data-stu-id="42d1c-112">Example</span></span>  
 <span data-ttu-id="42d1c-113">O exemplo a seguir demonstra como adicionar manipuladores para o <xref:System.Windows.DragDrop.DragOver> e <xref:System.Windows.DragDrop.Drop> eventos em um <xref:System.Windows.Controls.RichTextBox>.</span><span class="sxs-lookup"><span data-stu-id="42d1c-113">The following example demonstrates how to add handlers for the <xref:System.Windows.DragDrop.DragOver> and <xref:System.Windows.DragDrop.Drop> events on a <xref:System.Windows.Controls.RichTextBox>.</span></span> <span data-ttu-id="42d1c-114">Este exemplo usa o <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> método e conjuntos de `handledEventsToo` parâmetro para `true` para que os manipuladores de eventos serão invocados, embora o <xref:System.Windows.Controls.RichTextBox> marca esses eventos tratados.</span><span class="sxs-lookup"><span data-stu-id="42d1c-114">This example uses the <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> method and sets the `handledEventsToo` parameter to `true` so that the events handlers will be invoked even though the <xref:System.Windows.Controls.RichTextBox> marks these events as handled.</span></span> <span data-ttu-id="42d1c-115">O código nos manipuladores de eventos adiciona a funcionalidade para abrir um arquivo de texto que é arrastado para o <xref:System.Windows.Controls.RichTextBox>.</span><span class="sxs-lookup"><span data-stu-id="42d1c-115">The code in the event handlers adds functionality to open a text file that is dropped on the <xref:System.Windows.Controls.RichTextBox>.</span></span>  
  
 <span data-ttu-id="42d1c-116">Para testar este exemplo, arraste um arquivo de texto ou um arquivo do rich text format (RTF) do Windows Explorer para o <xref:System.Windows.Controls.RichTextBox>.</span><span class="sxs-lookup"><span data-stu-id="42d1c-116">To test this example, drag a text file or a rich text format (RTF) file from Windows Explorer to the <xref:System.Windows.Controls.RichTextBox>.</span></span> <span data-ttu-id="42d1c-117">O arquivo será aberto no <xref:System.Windows.Controls.RichTextBox>.</span><span class="sxs-lookup"><span data-stu-id="42d1c-117">The file will be opened in the <xref:System.Windows.Controls.RichTextBox>.</span></span> <span data-ttu-id="42d1c-118">Se você pressionar a tecla SHIFT antes de soltar o arquivo, ele será aberto como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="42d1c-118">If you press the SHIFT key before the dropping the file, the file will be opened as plain text.</span></span>  
  
 [!code-xaml[DragDropSnippets#RtbXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#rtbxaml)]  
  
 [!code-csharp[DragDropSnippets#RtbHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#rtbhandlers)]
 [!code-vb[DragDropSnippets#RtbHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#rtbhandlers)]