---
title: Como criar chaves de acesso com controles de rótulo dos Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [Windows Forms], access keys
- dialog box controls [Windows Forms], mnemonics
- access keys [Windows Forms], creating for controls
- Label control [Windows Forms], creating access keys
- mnemonics [Windows Forms], adding to dialog box controls
- mnemonics
- Windows Forms controls, access keys
- UseMnemonic property [Windows Forms], Label control
- keyboard shortcuts [Windows Forms], creating for controls
- access keys [Windows Forms], Windows Forms
ms.assetid: 5ee8f823-80be-4a4f-96a4-412671e2e306
ms.openlocfilehash: fc9592981f3d926b2b5b85b6869da13dc644e7a0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33530797"
---
# <a name="how-to-create-access-keys-with-windows-forms-label-controls"></a>Como criar chaves de acesso com controles de rótulo dos Windows Forms
Windows Forms <xref:System.Windows.Forms.Label> controles podem ser usados para definir as chaves de acesso para outros controles. Ao definir uma tecla de acesso em um controle de rótulo, o usuário pode pressionar a tecla ALT mais o caractere designado para mover o foco para o controle seguinte na ordem de tabulação. Como os rótulos não podem receber o foco, este é movido automaticamente para o próximo controle na ordem de tabulação. Use essa técnica para atribuir teclas de acesso a caixas de texto, caixas de combinação, caixas de listagem e grades de dados.  
  
### <a name="to-assign-an-access-key-to-a-control-with-a-label"></a>Atribuir uma tecla de acesso a um controle com um rótulo  
  
1.  Desenhe o rótulo primeiro e, em seguida, desenhe o outro controle.  
  
     -ou-  
  
     Desenhar controles em qualquer ordem e defina o <xref:System.Windows.Forms.Control.TabIndex%2A> propriedade do rótulo, a menos que outro controle.  
  
2.  Defina o rótulo <xref:System.Windows.Forms.Label.UseMnemonic%2A> propriedade `true`.  
  
3.  Usar um e comercial (&) no rótulo do <xref:System.Windows.Forms.Label.Text%2A> propriedade para atribuir a chave de acesso para o rótulo. Para obter mais informações, consulte [Criando teclas de acesso para controles dos Windows Forms](../../../../docs/framework/winforms/controls/how-to-create-access-keys-for-windows-forms-controls.md).  
  
    > [!NOTE]
    >  Pode ser útil exibir o E comercial em um controle de rótulo, em vez de usá-lo para criar teclas de acesso. Isso poderá ocorrer se você associar um controle de rótulo a um campo em um conjunto de registros em que os dados incluem o E comercial. Para exibir o e comercial em um controle de rótulo, defina o <xref:System.Windows.Forms.Label.UseMnemonic%2A> propriedade `false`. Se você quiser exibir "e" comercial e também tem uma chave de acesso, defina o <xref:System.Windows.Forms.Label.UseMnemonic%2A> propriedade `true` e indicam a chave de acesso com um e comercial (&) e o e comercial para exibir com duas vezes.  
  
    ```vb  
    Label1.UseMnemonic = True  
    Label1.Text = "&Print"  
    Label2.UseMnemonic = True  
    Label2.Text = "&Copy && Paste"  
    ```  
  
    ```csharp  
    label1.UseMnemonic = true;  
    label1.Text = "&Print";  
    label2.UseMnemonic = true;  
    label2.Text = "&Copy && Paste";  
    ```  
  
    ```cpp  
    label1->UseMnemonic = true;  
    label1->Text = "&Print";  
    label2->UseMnemonic = true;  
    label2->Text = "&Copy && Paste";  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Como dimensionar um controle de rótulo dos Windows Forms para ajustar-se ao seu conteúdo](../../../../docs/framework/winforms/controls/how-to-size-a-windows-forms-label-control-to-fit-its-contents.md)  
 [Visão geral do controle Label](../../../../docs/framework/winforms/controls/label-control-overview-windows-forms.md)  
 [Controle de rótulo](../../../../docs/framework/winforms/controls/label-control-windows-forms.md)
