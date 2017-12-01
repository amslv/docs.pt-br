---
title: Membros protegidos
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- members [.NET Framework], protected
- protected members
- classes [.NET Framework], unsealed
- classes [.NET Framework], protected members
- unsealed classes
- customizing class behavior
ms.assetid: aa0b58ee-3956-494d-ab48-471ae5db8740
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 7c3aacd0f08641c01200f0b1791a78413a306590
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="protected-members"></a><span data-ttu-id="cb060-102">Membros protegidos</span><span class="sxs-lookup"><span data-stu-id="cb060-102">Protected Members</span></span>
<span data-ttu-id="cb060-103">Membros protegidos por si só não fornecem nenhuma extensibilidade, mas eles podem tornar a extensibilidade por meio de subclassificação mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="cb060-103">Protected members by themselves do not provide any extensibility, but they can make extensibility through subclassing more powerful.</span></span> <span data-ttu-id="cb060-104">Eles podem ser usados para expor as opções avançadas de personalização sem desnecessariamente complicar a principal interface pública.</span><span class="sxs-lookup"><span data-stu-id="cb060-104">They can be used to expose advanced customization options without unnecessarily complicating the main public interface.</span></span>  
  
 <span data-ttu-id="cb060-105">Designers de Framework precisam ter cuidado com membros protegidos, porque o nome "protegido" pode dar uma falsa sensação de segurança.</span><span class="sxs-lookup"><span data-stu-id="cb060-105">Framework designers need to be careful with protected members because the name "protected" can give a false sense of security.</span></span> <span data-ttu-id="cb060-106">Qualquer pessoa que é capaz de subclasse de uma classe não lacrada e membros de acesso protegido e então as mesmas as práticas de codificação usadas para membros públicos se aplica a membros protegidos.</span><span class="sxs-lookup"><span data-stu-id="cb060-106">Anyone is able to subclass an unsealed class and access protected members, and so all the same defensive coding practices used for public members apply to protected members.</span></span>  
  
 <span data-ttu-id="cb060-107">**✓ CONSIDERE** usando membros para a personalização avançada protegidos.</span><span class="sxs-lookup"><span data-stu-id="cb060-107">**✓ CONSIDER** using protected members for advanced customization.</span></span>  
  
 <span data-ttu-id="cb060-108">**FAZER ✓** tratar membros protegidos em classes não lacradas como public para fins de análise de segurança, documentação e compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="cb060-108">**✓ DO** treat protected members in unsealed classes as public for the purpose of security, documentation, and compatibility analysis.</span></span>  
  
 <span data-ttu-id="cb060-109">Qualquer pessoa pode herdar de uma classe e acessar os membros protegidos.</span><span class="sxs-lookup"><span data-stu-id="cb060-109">Anyone can inherit from a class and access the protected members.</span></span>  
  
 <span data-ttu-id="cb060-110">*Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*</span><span class="sxs-lookup"><span data-stu-id="cb060-110">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>  
  
 <span data-ttu-id="cb060-111">*Reimpressas pela permissão de Pearson educação, Inc. de [diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008, Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*</span><span class="sxs-lookup"><span data-stu-id="cb060-111">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cb060-112">Consulte também</span><span class="sxs-lookup"><span data-stu-id="cb060-112">See Also</span></span>  
 [<span data-ttu-id="cb060-113">Diretrizes de design do Framework</span><span class="sxs-lookup"><span data-stu-id="cb060-113">Framework Design Guidelines</span></span>](../../../docs/standard/design-guidelines/index.md)  
 [<span data-ttu-id="cb060-114">Criação de extensibilidade</span><span class="sxs-lookup"><span data-stu-id="cb060-114">Designing for Extensibility</span></span>](../../../docs/standard/design-guidelines/designing-for-extensibility.md)