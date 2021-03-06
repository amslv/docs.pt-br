---
title: Como criar botões de alternância em controles ToolStrip
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- toggle buttons [Windows Forms], creating
- examples [Windows Forms], toolbars
- ToolStrip control [Windows Forms], creating toggle buttons
ms.assetid: d9c197df-4c65-43f2-beee-b68b52b2befc
ms.openlocfilehash: a04d531433273328c2d8eb0c5ef614f08c33952a
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33530374"
---
# <a name="how-to-create-toggle-buttons-in-toolstrip-controls"></a>Como criar botões de alternância em controles ToolStrip
Quando um usuário clica em um botão de alternância, ele aparece em baixo relevo e mantém a aparência de baixo relevo até que o usuário clica no botão novamente.  
  
### <a name="to-create-a-toggling-toolstripbutton"></a>Para criar uma alternância ToolStripButton  
  
-   Use o código como o exemplo de código a seguir. Esse código supõe que o formulário contém um <xref:System.Windows.Forms.ToolStrip> controle e que seu <xref:System.Windows.Forms.ToolStrip.Items%2A> coleção contém um <xref:System.Windows.Forms.ToolStripButton> chamado `toolStripButton1`. Ele também pressupõe que você tenha um manipulador de eventos chamado `toolStripButton1_CheckedChanged`.  
  
    ```vb  
    toolStripButton1.CheckOnClick = True  
    toolStripButton1.CheckedChanged AddressOf _  
    EventHandler(toolStripButton1_CheckedChanged);  
    ```  
  
    ```csharp  
    toolStripButton1.CheckOnClick = true;  
    toolStripButton1.CheckedChanged += new _  
    EventHandler(toolStripButton1_CheckedChanged);  
    ```  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Forms.ToolStripButton>  
 [Visão geral do controle ToolStrip](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)
