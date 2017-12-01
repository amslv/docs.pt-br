---
title: Usando o Document Object Model HTML gerenciado
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: managed HTML DOM
ms.assetid: a017dd5c-cd7b-47e4-952c-f4f54cb48409
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: ff1004248e709b4b4913b90eb81f0726ab390c54
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="using-the-managed-html-document-object-model"></a><span data-ttu-id="8ea24-102">Usando o Document Object Model HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-102">Using the Managed HTML Document Object Model</span></span>
<span data-ttu-id="8ea24-103">O Modelo de Objeto do Documento (DOM) HTML gerenciado fornece um wrapper com base no [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] para as classes HTML expostas pelo Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="8ea24-103">The managed HTML document object model (DOM) provides a wrapper based on the [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] for the HTML classes exposed by Internet Explorer.</span></span> <span data-ttu-id="8ea24-104">Use essas classes para manipular páginas HTML hospedadas no <xref:System.Windows.Forms.WebBrowser> controle, ou para criar novas páginas desde o início.</span><span class="sxs-lookup"><span data-stu-id="8ea24-104">Use these classes to manipulate HTML pages hosted in the <xref:System.Windows.Forms.WebBrowser> control, or to build new pages from the beginning.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="8ea24-105">Nesta seção</span><span class="sxs-lookup"><span data-stu-id="8ea24-105">In This Section</span></span>  
 [<span data-ttu-id="8ea24-106">Como acessar o Modelo de Objeto do Documento HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-106">How to: Access the Managed HTML Document Object Model</span></span>](../../../../docs/framework/winforms/controls/how-to-access-the-managed-html-document-object-model.md)  
 <span data-ttu-id="8ea24-107">Descreve como obter uma instância válida do <xref:System.Windows.Forms.HtmlDocument> em um aplicativo de formulários do Windows ou um <xref:System.Windows.Forms.UserControl> hospedado no Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="8ea24-107">Describes how to obtain a valid instance of <xref:System.Windows.Forms.HtmlDocument> from either a Windows Forms application or a <xref:System.Windows.Forms.UserControl> hosted in Internet Explorer.</span></span>  
  
 [<span data-ttu-id="8ea24-108">Como acessar a fonte HTML no Modelo de Objeto do Documento HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-108">How to: Access the HTML Source in the Managed HTML Document Object Model</span></span>](../../../../docs/framework/winforms/controls/how-to-access-the-html-source-in-the-managed-html-document-object-model.md)  
 <span data-ttu-id="8ea24-109">Descreve como obter o a fonte HTML original, sem modificações e como obter a fonte "ativa" que reflete o estado atual do DOM.</span><span class="sxs-lookup"><span data-stu-id="8ea24-109">Describes how to obtain the original, unmodified HTML source, and how to obtain the "live" source that reflects the current state of the DOM.</span></span>  
  
 [<span data-ttu-id="8ea24-110">Como alterar estilos em um elemento no Modelo de Objeto do Documento HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-110">How to: Change Styles on an Element in the Managed HTML Document Object Model</span></span>](../../../../docs/framework/winforms/controls/how-to-change-styles-on-an-element-in-the-managed-html-document-object-model.md)  
 <span data-ttu-id="8ea24-111">Descreve como manipular estilos que são usados para controlar a exibição visual de elementos.</span><span class="sxs-lookup"><span data-stu-id="8ea24-111">Describes how to manipulate styles, which are used to control the visual display of elements.</span></span>  
  
 [<span data-ttu-id="8ea24-112">Acessando quadros no Modelo de Objeto do Documento HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-112">Accessing Frames in the Managed HTML Document Object Model</span></span>](../../../../docs/framework/winforms/controls/accessing-frames-in-the-managed-html-document-object-model.md)  
 <span data-ttu-id="8ea24-113">Descreve quais são os quadros e conjuntos de quadros e como acessar o DOM de um quadro.</span><span class="sxs-lookup"><span data-stu-id="8ea24-113">Describes what frames and framesets are, and how to access the DOM of a frame.</span></span>  
  
 [<span data-ttu-id="8ea24-114">Acessando membros não expostos no Modelo de Objeto do Documento HTML gerenciado</span><span class="sxs-lookup"><span data-stu-id="8ea24-114">Accessing Unexposed Members on the Managed HTML Document Object Model</span></span>](../../../../docs/framework/winforms/controls/accessing-unexposed-members-on-the-managed-html-document-object-model.md)  
 <span data-ttu-id="8ea24-115">Descreve como acessar membros do DOM subjacente que não tenham um equivalente gerenciado.</span><span class="sxs-lookup"><span data-stu-id="8ea24-115">Describes how to access members of the underlying DOM that do not have a managed equivalent.</span></span>  
  
## <a name="reference"></a><span data-ttu-id="8ea24-116">Referência</span><span class="sxs-lookup"><span data-stu-id="8ea24-116">Reference</span></span>  
 <xref:System.Windows.Forms.HtmlDocument>  
  
 <xref:System.Windows.Forms.HtmlElement>  
  
 <xref:System.Windows.Forms.HtmlWindow>  
  
## <a name="related-sections"></a><span data-ttu-id="8ea24-117">Seções relacionadas</span><span class="sxs-lookup"><span data-stu-id="8ea24-117">Related Sections</span></span>  
 [<span data-ttu-id="8ea24-118">Controle WebBrowser</span><span class="sxs-lookup"><span data-stu-id="8ea24-118">WebBrowser Control</span></span>](../../../../docs/framework/winforms/controls/webbrowser-control-windows-forms.md)  
  
## <a name="see-also"></a><span data-ttu-id="8ea24-119">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8ea24-119">See Also</span></span>  
 [<span data-ttu-id="8ea24-120">Sobre o modelo de objeto DHTML</span><span class="sxs-lookup"><span data-stu-id="8ea24-120">About the DHTML Object Model</span></span>](http://msdn.microsoft.com/library/default.asp?url=/workshop/author/om/doc_object.asp)