---
title: "Como pintar uma área com uma imagem"
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
- images [WPF], painting with
- painting [WPF], with images
- brushes [WPF], painting with images
ms.assetid: 3432c533-1fc7-492d-94ee-0b13d60125ae
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 3edbe30347580bb4f9677d7fb98d3b4fd8b92cff
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2017
---
# <a name="how-to-paint-an-area-with-an-image"></a><span data-ttu-id="18b44-102">Como pintar uma área com uma imagem</span><span class="sxs-lookup"><span data-stu-id="18b44-102">How to: Paint an Area with an Image</span></span>
<span data-ttu-id="18b44-103">Este exemplo mostra como usar o <xref:System.Windows.Media.ImageBrush> classe para pintar uma área com uma imagem.</span><span class="sxs-lookup"><span data-stu-id="18b44-103">This example shows how to use the <xref:System.Windows.Media.ImageBrush> class to paint an area with an image.</span></span> <span data-ttu-id="18b44-104">Um <xref:System.Windows.Media.ImageBrush> exibe uma única imagem, que é especificada pelo seu <xref:System.Windows.Media.ImageBrush.ImageSource%2A> propriedade.</span><span class="sxs-lookup"><span data-stu-id="18b44-104">An <xref:System.Windows.Media.ImageBrush> displays a single image, which is specified by its <xref:System.Windows.Media.ImageBrush.ImageSource%2A> property.</span></span>  
  
## <a name="example"></a><span data-ttu-id="18b44-105">Exemplo</span><span class="sxs-lookup"><span data-stu-id="18b44-105">Example</span></span>  
 <span data-ttu-id="18b44-106">A exemplo a seguir pinta o <xref:System.Windows.Controls.Control.Background%2A> de um botão usando um <xref:System.Windows.Media.ImageBrush>.</span><span class="sxs-lookup"><span data-stu-id="18b44-106">The following example paints the <xref:System.Windows.Controls.Control.Background%2A> of a button by using an <xref:System.Windows.Media.ImageBrush>.</span></span>  
  
 [!code-csharp[UsingImageBrush_snip#ImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/PaintingWithImagesExample.cs#imagebrushexamplewholepage)]  
  
 <span data-ttu-id="18b44-107">Por padrão, um <xref:System.Windows.Media.ImageBrush> alonga a imagem para preencher completamente a área que você estiver pintando.</span><span class="sxs-lookup"><span data-stu-id="18b44-107">By default, an <xref:System.Windows.Media.ImageBrush> stretches its image to completely fill the area that you are painting.</span></span> <span data-ttu-id="18b44-108">No exemplo anterior, a imagem é esticada para preencher o botão, possivelmente distorcendo a imagem.</span><span class="sxs-lookup"><span data-stu-id="18b44-108">In the preceding example, the image is stretched to fill the button, possibly distorting the image.</span></span> <span data-ttu-id="18b44-109">Você pode controlar esse comportamento, definindo a <xref:System.Windows.Media.TileBrush.Stretch%2A> propriedade <xref:System.Windows.Media.TileBrush> para <xref:System.Windows.Media.Stretch.Uniform> ou <xref:System.Windows.Media.Stretch.UniformToFill>, que faz com que o pincel preservar a taxa de proporção da imagem.</span><span class="sxs-lookup"><span data-stu-id="18b44-109">You can control this behavior by setting the <xref:System.Windows.Media.TileBrush.Stretch%2A> property of <xref:System.Windows.Media.TileBrush> to <xref:System.Windows.Media.Stretch.Uniform> or <xref:System.Windows.Media.Stretch.UniformToFill>, which causes the brush to preserve the aspect ratio of the image.</span></span>  
  
 <span data-ttu-id="18b44-110">Se você definir o <xref:System.Windows.Media.TileBrush.Viewport%2A> e <xref:System.Windows.Media.TileBrush.TileMode%2A> propriedades de um <xref:System.Windows.Media.ImageBrush>, você pode criar um padrão de repetição.</span><span class="sxs-lookup"><span data-stu-id="18b44-110">If you set the <xref:System.Windows.Media.TileBrush.Viewport%2A> and <xref:System.Windows.Media.TileBrush.TileMode%2A> properties of an <xref:System.Windows.Media.ImageBrush>, you can create a repeating pattern.</span></span> <span data-ttu-id="18b44-111">O exemplo a seguir pinta um botão usando um padrão que é criado por meio de uma imagem.</span><span class="sxs-lookup"><span data-stu-id="18b44-111">The following example paints a button by using a pattern that is created from an image.</span></span>  
  
 [!code-csharp[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TiledImageBrushExample.cs#tiledimagebrushexamplewholepage)]
 [!code-vb[UsingImageBrush_snip#TiledImageBrushExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UsingImageBrush_snip/VisualBasic/TiledImageBrushExample.vb#tiledimagebrushexamplewholepage)]  
  
 <span data-ttu-id="18b44-112">Para obter mais informações sobre o <xref:System.Windows.Media.ImageBrush> de classe, consulte [pintura com imagens, desenhos e visuais](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).</span><span class="sxs-lookup"><span data-stu-id="18b44-112">For more information about the <xref:System.Windows.Media.ImageBrush> class, see [Painting with Images, Drawings, and Visuals](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md).</span></span>  
  
 <span data-ttu-id="18b44-113">Este exemplo de código é parte de um exemplo maior fornecido para a <xref:System.Windows.Media.ImageBrush> classe.</span><span class="sxs-lookup"><span data-stu-id="18b44-113">This code example is part of a larger example that is provided for the <xref:System.Windows.Media.ImageBrush> class.</span></span> <span data-ttu-id="18b44-114">Para o exemplo completo, consulte [ImageBrush exemplo](http://go.microsoft.com/fwlink/?LinkID=160005).</span><span class="sxs-lookup"><span data-stu-id="18b44-114">For the complete sample, see [ImageBrush Sample](http://go.microsoft.com/fwlink/?LinkID=160005).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="18b44-115">Consulte também</span><span class="sxs-lookup"><span data-stu-id="18b44-115">See Also</span></span>  
 [<span data-ttu-id="18b44-116">Pintando com imagens, desenhos e visuais</span><span class="sxs-lookup"><span data-stu-id="18b44-116">Painting with Images, Drawings, and Visuals</span></span>](../../../../docs/framework/wpf/graphics-multimedia/painting-with-images-drawings-and-visuals.md)