---
title: "Gramática XamlName"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DottedXamlName grammar [XAML Services]
- grammar [XAML Services], DottedXamlName
- grammar [XAML Services], XamlName
- names in XAML [XAML Services]
- XamlName grammar [XAML Services]
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
caps.latest.revision: "13"
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.openlocfilehash: 92327c8ff6232e64bf8b6b2a9d78e4a9eb30f3e1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="xamlname-grammar"></a><span data-ttu-id="d8379-102">Gramática XamlName</span><span class="sxs-lookup"><span data-stu-id="d8379-102">XamlName Grammar</span></span>
<span data-ttu-id="d8379-103">Gramática XamlName é uma gramática específica que está definida na especificação de linguagem XAML [MS-XAML], que é reproduzida aqui por conveniência.</span><span class="sxs-lookup"><span data-stu-id="d8379-103">XamlName Grammar is a specific grammar that is defined in the XAML language specification [MS-XAML], which is reproduced here for convenience.</span></span>  
  
## <a name="from-the-xaml-specification"></a><span data-ttu-id="d8379-104">Da especificação XAML.</span><span class="sxs-lookup"><span data-stu-id="d8379-104">From the XAML Specification</span></span>  
 <span data-ttu-id="d8379-105">A especificação de [MS-XAML] define a gramática XamlName para identificar o conjunto de identificadores simbólicos legais utilizados para tipos e propriedades.</span><span class="sxs-lookup"><span data-stu-id="d8379-105">The [MS-XAML] specification defines the grammar XamlName to identify the set of legal symbolic identifiers used for types and properties.</span></span>  
  
 <span data-ttu-id="d8379-106">Cadeia de caracteres valores que são do tipo XamlName deve estar de acordo com a gramática a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8379-106">String values that are of type XamlName must conform to the following grammar:</span></span>  
  
```  
XamlName ::= NameStartChar ( NameChar )*   
NameStartChar ::= LetterCharacter | '_'   
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter   
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl   
DecimalDigit ::= UnicodeNd   
CombiningCharacter ::= UnicodeMn | UnicodeMc  
```  
  
 <span data-ttu-id="d8379-107">Que assume os seguintes valores de categoria geral, conforme definido no banco de dados de caractere Unicode</span><span class="sxs-lookup"><span data-stu-id="d8379-107">Which assumes the following general category values as defined in the Unicode Character Database</span></span>  
  
```  
Lu  
Letter, Uppercase  
Ll  
Letter, Lowercase  
Lt  
Letter, Titlecase  
Lm  
Letter, Modifier  
Lo  
Letter, Other  
Mn  
Mark, Non-Spacing  
Mc  
Mark, Spacing Combining  
Nd  
Number, Decimal  
Nl  
Number, Letter  
```  
  
 <span data-ttu-id="d8379-108">XAML define uma segunda gramática, DottedXamlName, que é usado para a propriedade e evento referências qualificadas e também membros anexos.</span><span class="sxs-lookup"><span data-stu-id="d8379-108">XAML defines a second grammar, DottedXamlName, that is used for property and event qualified references, and also for attached members.</span></span> <span data-ttu-id="d8379-109">Para obter mais informações, consulte <xref:System.Windows.DependencyProperty> e [visão geral de XAML (WPF)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).</span><span class="sxs-lookup"><span data-stu-id="d8379-109">For more information, see <xref:System.Windows.DependencyProperty> and [XAML Overview (WPF)](../../../docs/framework/wpf/advanced/xaml-overview-wpf.md).</span></span>  
  
 <span data-ttu-id="d8379-110">Cadeia de caracteres valores que são do tipo XamlName deve estar de acordo com a gramática a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8379-110">String values that are of type DottedXamlName must conform to the following grammar:</span></span>  
  
```  
DottedXamlName ::= XamlName '.' XamlName  
```  
  
## <a name="remarks"></a><span data-ttu-id="d8379-111">Comentários</span><span class="sxs-lookup"><span data-stu-id="d8379-111">Remarks</span></span>  
 <span data-ttu-id="d8379-112">Para a especificação completa, consulte [ \[XAML MS\]](http://go.microsoft.com/fwlink/?LinkId=114525).</span><span class="sxs-lookup"><span data-stu-id="d8379-112">For the complete specification, see [\[MS-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525).</span></span>