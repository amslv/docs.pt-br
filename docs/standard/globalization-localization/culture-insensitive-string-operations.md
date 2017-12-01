---
title: "Operações de cadeia de caracteres que não levam em conta a cultura"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- culture, culture-insensitive string operations
- case-sensitive comparisons
- globalization [.NET Framework], culture-insensitive string operations
- strings [.NET Framework], culture-insensitive string operations
- localization [.NET Framework], culture-insensitive string operations
- world-ready applications, culture-insensitive string operations
- culture-sensitive string operations
- culture-insensitive string operations
ms.assetid: e6e2bb94-a95d-44e2-b68c-cfdd1db77784
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: dddd46dc5d825738dd9d5038ae573910122953c8
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="culture-insensitive-string-operations"></a><span data-ttu-id="48d38-102">Operações de cadeia de caracteres que não levam em conta a cultura</span><span class="sxs-lookup"><span data-stu-id="48d38-102">Culture-Insensitive String Operations</span></span>
<span data-ttu-id="48d38-103">As operações de cadeia de caracteres sensíveis à cultura podem representar uma vantagem se você estiver criando aplicativos projetados para exibir resultados a usuários de acordo com a cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-103">Culture-sensitive string operations can be an advantage if you are creating applications designed to display results to users on a per-culture basis.</span></span> <span data-ttu-id="48d38-104">Por padrão, os métodos sensíveis à cultura obtêm a cultura a ser usada da propriedade <xref:System.Globalization.CultureInfo.CurrentCulture%2A> para o thread atual.</span><span class="sxs-lookup"><span data-stu-id="48d38-104">By default, culture-sensitive methods obtain the culture to use from the <xref:System.Globalization.CultureInfo.CurrentCulture%2A> property for the current thread.</span></span>  
  
 <span data-ttu-id="48d38-105">Observe que as operações de cadeia de caracteres sensíveis à cultura nem sempre apresentam o comportamento desejado.</span><span class="sxs-lookup"><span data-stu-id="48d38-105">Note that culture-sensitive string operations are not always the desired behavior.</span></span> <span data-ttu-id="48d38-106">Usar operações sensíveis à cultura quando os resultados devem ser independentes da cultura pode fazer o código falhar em culturas com mapeamentos de casos e regras de classificação personalizados.</span><span class="sxs-lookup"><span data-stu-id="48d38-106">Using culture-sensitive operations when results should be independent of culture can cause application code to fail on cultures with custom case mappings and sorting rules.</span></span> <span data-ttu-id="48d38-107">Para obter um exemplo, consulte a seção "Cadeia de caracteres comparações que Use a cultura atual" o [práticas recomendadas para usar cadeias de caracteres](../../../docs/standard/base-types/best-practices-strings.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="48d38-107">For an example, see the "String Comparisons that Use the Current Culture" section in the [Best Practices for Using Strings](../../../docs/standard/base-types/best-practices-strings.md) article.</span></span>  
  
 <span data-ttu-id="48d38-108">A forma como o aplicativo usa os resultados determina se as operações de cadeia de caracteres devem ser sensíveis à cultura ou insensíveis à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-108">Whether string operations should be culture-sensitive or culture-insensitive depends on how your application uses the results.</span></span> <span data-ttu-id="48d38-109">Operações de cadeias de caracteres que exibem resultados para o usuário devem normalmente ser sensíveis à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-109">String operations that display results to the user should typically be culture-sensitive.</span></span> <span data-ttu-id="48d38-110">Por exemplo, se um aplicativo exibe uma lista classificada das cadeias de caracteres encontradas em uma caixa de listagem, o aplicativo deve executar uma classificação sensível à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-110">For example, if an application displays a sorted list of localized strings in a list box, the application should perform a culture-sensitive sort.</span></span>  
  
 <span data-ttu-id="48d38-111">Os resultados das operações de cadeia de caracteres usados internamente devem, de forma geral, ser insensíveis à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-111">Results of string operations that are used internally should typically be culture-insensitive.</span></span> <span data-ttu-id="48d38-112">Geralmente, se o aplicativo trabalha com nomes de arquivos, formatos de persistência ou informações simbólicas que não são exibidas para o usuário, os resultados das operações de cadeia de caracteres não devem variar de acordo com a cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-112">In general, if the application is working with file names, persistence formats, or symbolic information that is not displayed to the user, results of string operations should not vary by culture.</span></span> <span data-ttu-id="48d38-113">Por exemplo, se um aplicativo compara uma cadeia de caracteres para determinar se ela é uma marca XML reconhecida, a comparação não deve ser sensível à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-113">For example, if an application compares a string to determine whether it is a recognized XML tag, the comparison should not be culture-sensitive.</span></span> <span data-ttu-id="48d38-114">Além disso, se uma decisão de segurança é baseada no resultado de uma operação de comparação de cadeias de caracteres ou de modificação de maiúsculas/minúsculas, a operação deve ser sensível à cultura para garantir que o resultado não seja afetado pelo valor de <xref:System.Globalization.CultureInfo.CurrentCulture%2A>.</span><span class="sxs-lookup"><span data-stu-id="48d38-114">In addition, if a security decision is based on the result of a string comparison or case change operation, the operation should be culture-insensitive to ensure that the result is not affected by the value of <xref:System.Globalization.CultureInfo.CurrentCulture%2A>.</span></span>  
  
 <span data-ttu-id="48d38-115">Independentemente de estar ou não desenvolvendo um aplicativo que inclua código para tratar problemas de localização e globalização, você deve estar ciente dos métodos .NET Framework que, por padrão, recuperam resultados sensíveis à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-115">Whether or not you are developing an application that includes code to handle localization and globalization issues, you should be aware of the .NET Framework methods that retrieve culture-sensitive results by default.</span></span> <span data-ttu-id="48d38-116">A finalidade deste tópico é ilustrar a maneira correta para seus aplicativos usarem esses métodos a fim de obter resultados insensíveis à cultura.</span><span class="sxs-lookup"><span data-stu-id="48d38-116">The purpose of this topic is to illustrate the correct way for your applications to use these methods to obtain culture-insensitive results.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="48d38-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="48d38-117">See Also</span></span>  
 [<span data-ttu-id="48d38-118">Globalização e localização</span><span class="sxs-lookup"><span data-stu-id="48d38-118">Globalization and Localization</span></span>](../../../docs/standard/globalization-localization/index.md)