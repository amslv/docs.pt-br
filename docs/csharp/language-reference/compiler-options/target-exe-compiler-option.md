---
title: -target:exe (opções do compilador C#)
ms.date: 07/20/2015
f1_keywords:
- /exe
helpviewer_keywords:
- target compiler options [C#], /target:exe
- /target compiler options [C#], /target:exe
- -target compiler options [C#], /target:exe
ms.assetid: bda5717d-1b91-4848-956b-fcf85c30e432
ms.openlocfilehash: 4a2d3ea2bda56caf6a16f52877ad36b3947357e8
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43518153"
---
# <a name="-targetexe-c-compiler-options"></a>-target:exe (opções do compilador C#)
A opção **-target:exe** faz com que o compilador crie um aplicativo de console executável (EXE).  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-target:exe  
```  
  
## <a name="remarks"></a>Comentários  
 A opção **-target:exe** está em vigor por padrão. O arquivo executável será criado com a extensão .exe.  
  
 Use [-target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) para criar um executável de programa do Windows.  
  
 A menos que seja especificado de outra forma com a opção [-out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), o nome do arquivo de saída usará o nome do arquivo de entrada que contém o método [Main](../../../csharp/programming-guide/main-and-command-args/index.md).  
  
 Quando especificado na linha de comando, todos os arquivos até a próxima opção **-out** ou **-target:module** serão usados para criar o arquivo .exe  
  
 Somente um método **Main** é necessário nos arquivos de código-fonte que são compilados em um arquivo .exe. A opção do compilador [-main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) permite especificar qual classe contém o método **Main**, nos casos em que o código tem mais de uma classe com um método **Main**.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Para definir esta opção do compilador no ambiente de desenvolvimento do Visual Studio  
  
1.  Abra a página **Propriedades** do projeto.  
  
2.  Clique na página de propriedades do **Aplicativo**.  
  
3.  Modifique a propriedade **Tipo de saída**.  
  
 Para saber mais sobre como definir essa opção do compilador programaticamente, veja <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Exemplo  
 Cada uma das seguintes linhas de comando compilará `in.cs`, criando `in.exe`:  
  
```console  
csc -target:exe in.cs  
csc in.cs  
```  
  
## <a name="see-also"></a>Consulte também  

- [-target (opções do compilador do C#)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)  
- [Opções do compilador de C#](../../../csharp/language-reference/compiler-options/index.md)
