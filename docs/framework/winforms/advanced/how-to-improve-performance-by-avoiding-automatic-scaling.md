---
title: "Como melhorar o desempenho evitando o dimensionamento automático"
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
- automatic scaling
- images [Windows Forms], improving performance
- images [Windows Forms], using without automatic scaling
- performance [Windows Forms], improving image
ms.assetid: 5fe2c95d-8653-4d55-bf0d-e5afa28f223b
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: 0130e0745dfca20da5dc723bb7cc84748bb0b148
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-improve-performance-by-avoiding-automatic-scaling"></a><span data-ttu-id="4b526-102">Como melhorar o desempenho evitando o dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="4b526-102">How to: Improve Performance by Avoiding Automatic Scaling</span></span>
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]<span data-ttu-id="4b526-103"> pode ajustar a escala automaticamente de uma imagem à medida que você a desenha, o que poderia diminuir o desempenho.</span><span class="sxs-lookup"><span data-stu-id="4b526-103"> may automatically scale an image as you draw it, which would decrease performance.</span></span> <span data-ttu-id="4b526-104">Como alternativa, você pode controlar o dimensionamento da imagem, passando as dimensões do retângulo de destino para o <xref:System.Drawing.Graphics.DrawImage%2A> método.</span><span class="sxs-lookup"><span data-stu-id="4b526-104">Alternatively, you can control the scaling of the image by passing the dimensions of the destination rectangle to the <xref:System.Drawing.Graphics.DrawImage%2A> method.</span></span>  
  
 <span data-ttu-id="4b526-105">Por exemplo, a seguinte chamada para o <xref:System.Drawing.Graphics.DrawImage%2A> método Especifica um canto superior esquerdo do (50, 30), mas não especifica um retângulo de destino.</span><span class="sxs-lookup"><span data-stu-id="4b526-105">For example, the following call to the <xref:System.Drawing.Graphics.DrawImage%2A> method specifies an upper-left corner of (50, 30) but does not specify a destination rectangle.</span></span>  
  
 [!code-csharp[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.WorkingWithImages#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#31)]  
  
 <span data-ttu-id="4b526-106">Embora essa é a versão mais fácil do <xref:System.Drawing.Graphics.DrawImage%2A> método em termos de número de argumentos necessários, não é necessariamente o mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="4b526-106">Although this is the easiest version of the <xref:System.Drawing.Graphics.DrawImage%2A> method in terms of the number of required arguments, it is not necessarily the most efficient.</span></span> <span data-ttu-id="4b526-107">Se a resolução usada pelo [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] (geralmente 96 pontos por polegada) é diferente do que a resolução armazenada na <xref:System.Drawing.Image> objeto, em seguida, o <xref:System.Drawing.Graphics.DrawImage%2A> método dimensionará a imagem.</span><span class="sxs-lookup"><span data-stu-id="4b526-107">If the resolution used by [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] (usually 96 dots per inch) is different from the resolution stored in the <xref:System.Drawing.Image> object, then the <xref:System.Drawing.Graphics.DrawImage%2A> method will scale the image.</span></span> <span data-ttu-id="4b526-108">Por exemplo, suponha que um <xref:System.Drawing.Image> objeto tem uma largura de 216 pixels e um valor armazenado resolução horizontal de 72 pontos por polegada.</span><span class="sxs-lookup"><span data-stu-id="4b526-108">For example, suppose an <xref:System.Drawing.Image> object has a width of 216 pixels and a stored horizontal resolution value of 72 dots per inch.</span></span> <span data-ttu-id="4b526-109">Como 216/72 é 3, <xref:System.Drawing.Graphics.DrawImage%2A> dimensionará a imagem para que ele tenha uma largura de 3 polegadas em uma resolução de 96 pontos por polegada.</span><span class="sxs-lookup"><span data-stu-id="4b526-109">Because 216/72 is 3, <xref:System.Drawing.Graphics.DrawImage%2A> will scale the image so that it has a width of 3 inches at a resolution of 96 dots per inch.</span></span> <span data-ttu-id="4b526-110">Ou seja, <xref:System.Drawing.Graphics.DrawImage%2A> exibirá uma imagem que tem uma largura de 96 x 3 = 288 pixels.</span><span class="sxs-lookup"><span data-stu-id="4b526-110">That is, <xref:System.Drawing.Graphics.DrawImage%2A> will display an image that has a width of 96x3 = 288 pixels.</span></span>  
  
 <span data-ttu-id="4b526-111">Mesmo se a resolução da tela for diferente de 96 pontos por polegada, [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] provavelmente ajustará a escala da imagem como se a resolução de tela fosse de 96 pontos por polegada.</span><span class="sxs-lookup"><span data-stu-id="4b526-111">Even if your screen resolution is different from 96 dots per inch, [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] will probably scale the image as if the screen resolution were 96 dots per inch.</span></span> <span data-ttu-id="4b526-112">Isso ocorre porque um [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> objeto está associado um contexto de dispositivo e quando [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] consultas o contexto de dispositivo para a resolução da tela, o resultado geralmente é 96, independentemente da resolução da tela real.</span><span class="sxs-lookup"><span data-stu-id="4b526-112">That is because a [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> object is associated with a device context, and when [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] queries the device context for the screen resolution, the result is usually 96, regardless of the actual screen resolution.</span></span> <span data-ttu-id="4b526-113">Você pode evitar o dimensionamento automático, especificando o retângulo de destino no <xref:System.Drawing.Graphics.DrawImage%2A> método.</span><span class="sxs-lookup"><span data-stu-id="4b526-113">You can avoid automatic scaling by specifying the destination rectangle in the <xref:System.Drawing.Graphics.DrawImage%2A> method.</span></span>  
  
## <a name="example"></a><span data-ttu-id="4b526-114">Exemplo</span><span class="sxs-lookup"><span data-stu-id="4b526-114">Example</span></span>  
 <span data-ttu-id="4b526-115">O exemplo a seguir desenha a mesma imagem duas vezes.</span><span class="sxs-lookup"><span data-stu-id="4b526-115">The following example draws the same image twice.</span></span> <span data-ttu-id="4b526-116">No primeiro caso, a largura e altura do retângulo de destino não são especificados, e a escala da imagem é ajustada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4b526-116">In the first case, the width and height of the destination rectangle are not specified, and the image is automatically scaled.</span></span> <span data-ttu-id="4b526-117">No segundo caso, a largura e altura (medidas em pixels) do retângulo de destino são especificadas como iguais à largura e altura da imagem original.</span><span class="sxs-lookup"><span data-stu-id="4b526-117">In the second case, the width and height (measured in pixels) of the destination rectangle are specified to be the same as the width and height of the original image.</span></span> <span data-ttu-id="4b526-118">A ilustração a seguir mostra a imagem renderizada duas vezes.</span><span class="sxs-lookup"><span data-stu-id="4b526-118">The following illustration shows the image rendered twice.</span></span>  
  
 <span data-ttu-id="4b526-119">![Textura em escala](../../../../docs/framework/winforms/advanced/media/csscaledtexture1.png "csscaledtexture1")</span><span class="sxs-lookup"><span data-stu-id="4b526-119">![Scaled Texture](../../../../docs/framework/winforms/advanced/media/csscaledtexture1.png "csscaledtexture1")</span></span>  
  
 [!code-csharp[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/CS/Class1.cs#32)]
 [!code-vb[System.Drawing.WorkingWithImages#32](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.WorkingWithImages/VB/Class1.vb#32)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="4b526-120">Compilando o código</span><span class="sxs-lookup"><span data-stu-id="4b526-120">Compiling the Code</span></span>  
 <span data-ttu-id="4b526-121">O exemplo anterior é projetado para uso com o Windows Forms e requer <xref:System.Windows.Forms.PaintEventArgs> `e`, que é um parâmetro do <xref:System.Windows.Forms.Control.Paint> manipulador de eventos.</span><span class="sxs-lookup"><span data-stu-id="4b526-121">The preceding example is designed for use with Windows Forms, and it requires <xref:System.Windows.Forms.PaintEventArgs> `e`, which is a parameter of the <xref:System.Windows.Forms.Control.Paint> event handler.</span></span> <span data-ttu-id="4b526-122">Substitua Texture.jpg por um nome e caminho de imagem válidos no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="4b526-122">Replace Texture.jpg with an image name and path that are valid on your system.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4b526-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4b526-123">See Also</span></span>  
 [<span data-ttu-id="4b526-124">Imagens, bitmaps e metarquivos</span><span class="sxs-lookup"><span data-stu-id="4b526-124">Images, Bitmaps, and Metafiles</span></span>](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)  
 [<span data-ttu-id="4b526-125">Trabalhando com Imagens, Bitmaps, Ícones e Metarquivos</span><span class="sxs-lookup"><span data-stu-id="4b526-125">Working with Images, Bitmaps, Icons, and Metafiles</span></span>](../../../../docs/framework/winforms/advanced/working-with-images-bitmaps-icons-and-metafiles.md)