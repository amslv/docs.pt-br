---
title: "Como animar um objeto ao longo de um caminho (animação de ponto)"
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
- animation [WPF], objects along paths (point animation)
- point animation [WPF]
ms.assetid: 1fa3f817-35bc-41a1-b366-f5a20b70da0c
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 47cafab505bcbab7008385393bbacf093e264cd9
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-animate-an-object-along-a-path-point-animation"></a><span data-ttu-id="69c0e-102">Como animar um objeto ao longo de um caminho (animação de ponto)</span><span class="sxs-lookup"><span data-stu-id="69c0e-102">How to: Animate an Object Along a Path (Point Animation)</span></span>
<span data-ttu-id="69c0e-103">Este exemplo mostra como usar um <xref:System.Windows.Media.Animation.PointAnimationUsingPath> objeto animar uma <xref:System.Windows.Point> ao longo de um caminho curvo.</span><span class="sxs-lookup"><span data-stu-id="69c0e-103">This example shows how to use a <xref:System.Windows.Media.Animation.PointAnimationUsingPath> object to animate a <xref:System.Windows.Point> along a curved path.</span></span>  
  
## <a name="example"></a><span data-ttu-id="69c0e-104">Exemplo</span><span class="sxs-lookup"><span data-stu-id="69c0e-104">Example</span></span>  
 <span data-ttu-id="69c0e-105">O exemplo a seguir move um <xref:System.Windows.Media.EllipseGeometry> ao longo de um caminho definido por uma <xref:System.Windows.Media.PathGeometry>.</span><span class="sxs-lookup"><span data-stu-id="69c0e-105">The following example moves an <xref:System.Windows.Media.EllipseGeometry> along a path defined by a <xref:System.Windows.Media.PathGeometry>.</span></span> <span data-ttu-id="69c0e-106">A geometria de elipse <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriedade, que usa um <xref:System.Windows.Point> valor, especifica sua posição; para mover a geometria da elipse, você animar seu <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="69c0e-106">The ellipse geometry's <xref:System.Windows.Media.EllipseGeometry.Center%2A> property, which takes a <xref:System.Windows.Point> value, specifies its position; to move the ellipse geometry, you animate its <xref:System.Windows.Media.EllipseGeometry.Center%2A> property.</span></span> <span data-ttu-id="69c0e-107">O exemplo usa um <xref:System.Windows.Media.Animation.PointAnimationUsingPath> para animar a <xref:System.Windows.Media.EllipseGeometry> do objeto <xref:System.Windows.Media.EllipseGeometry.Center%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="69c0e-107">The example uses a <xref:System.Windows.Media.Animation.PointAnimationUsingPath> to animate the <xref:System.Windows.Media.EllipseGeometry> object's <xref:System.Windows.Media.EllipseGeometry.Center%2A> property.</span></span>  
  
 [!code-xaml[PathAnimationGallery_snippet#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_snippet/CS/pointanimationusingpathexample.xaml#pointanimationusingpathwholepage)]  
  
 [!code-csharp[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/CSharp/PointAnimationUsingPathExample.cs#pointanimationusingpathwholepage)]
 [!code-vb[PathAnimationGallery_procedural_snip#PointAnimationUsingPathWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PathAnimationGallery_procedural_snip/VisualBasic/PointAnimationUsingPathExample.vb#pointanimationusingpathwholepage)]  
  
 <span data-ttu-id="69c0e-108">Para o exemplo completo, consulte [exemplo de animação de caminho](http://go.microsoft.com/fwlink/?LinkID=160028).</span><span class="sxs-lookup"><span data-stu-id="69c0e-108">For the complete sample, see [Path Animation Sample](http://go.microsoft.com/fwlink/?LinkID=160028).</span></span>  
  
 <span data-ttu-id="69c0e-109">A versão do código do exemplo anterior usada um <xref:System.Windows.Media.Animation.Storyboard> para animar a <xref:System.Windows.Media.EllipseGeometry>, mesmo que apenas uma animação foi aplicada.</span><span class="sxs-lookup"><span data-stu-id="69c0e-109">The code version of the preceding sample used a <xref:System.Windows.Media.Animation.Storyboard> to animate the <xref:System.Windows.Media.EllipseGeometry>, even though only one animation was applied.</span></span> <span data-ttu-id="69c0e-110">Um <xref:System.Windows.Media.Animation.Storyboard> geralmente é a maneira mais fácil para aplicar várias animações pois essas animações podem ser controladas pelo mesmo <xref:System.Windows.Media.Animation.Storyboard>.</span><span class="sxs-lookup"><span data-stu-id="69c0e-110">A <xref:System.Windows.Media.Animation.Storyboard> is often the easiest way to apply multiple animations because these animations can be controlled by the same <xref:System.Windows.Media.Animation.Storyboard>.</span></span> <span data-ttu-id="69c0e-111">No entanto, uma maneira fácil de aplicar uma única animação a uma propriedade em código é usar o <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> método.</span><span class="sxs-lookup"><span data-stu-id="69c0e-111">However, an easier way to apply a single animation to a property when using code is to use the <xref:System.Windows.Media.Animation.Animatable.BeginAnimation%2A> method.</span></span> <span data-ttu-id="69c0e-112">Para obter um exemplo, consulte [Animar uma propriedade sem usar um storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).</span><span class="sxs-lookup"><span data-stu-id="69c0e-112">For an example, see [Animate a Property Without Using a Storyboard](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-without-using-a-storyboard.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="69c0e-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="69c0e-113">See Also</span></span>  
 [<span data-ttu-id="69c0e-114">Exemplo de animação de caminho</span><span class="sxs-lookup"><span data-stu-id="69c0e-114">Path Animation Sample</span></span>](http://go.microsoft.com/fwlink/?LinkID=160028)  
 [<span data-ttu-id="69c0e-115">Visão geral da animação</span><span class="sxs-lookup"><span data-stu-id="69c0e-115">Animation Overview</span></span>](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)  
 [<span data-ttu-id="69c0e-116">Tópicos explicativos de animação do caminho</span><span class="sxs-lookup"><span data-stu-id="69c0e-116">Path Animation How-to Topics</span></span>](../../../../docs/framework/wpf/graphics-multimedia/path-animation-how-to-topics.md)