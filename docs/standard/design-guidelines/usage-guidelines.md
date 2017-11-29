---
title: Diretrizes de uso
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: class library design guidelines [.NET Framework], usage guidelines
ms.assetid: 42215ffa-a099-4a26-b14e-fb2bdb6f95b7
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: df0d1c5f8bff9d4cb546378f281a44c696246553
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="usage-guidelines"></a><span data-ttu-id="346db-102">Diretrizes de uso</span><span class="sxs-lookup"><span data-stu-id="346db-102">Usage Guidelines</span></span>
<span data-ttu-id="346db-103">Esta seção contém diretrizes para usar tipos comuns nas APIs publicamente acessível.</span><span class="sxs-lookup"><span data-stu-id="346db-103">This section contains guidelines for using common types in publicly accessible APIs.</span></span> <span data-ttu-id="346db-104">Ele lida com o uso direto de tipos de estrutura (por exemplo, atributos de serialização) internas e operadores comuns de sobrecarga.</span><span class="sxs-lookup"><span data-stu-id="346db-104">It deals with direct usage of built-in Framework types (e.g., serialization attributes) and overloading common operators.</span></span>  
  
 <span data-ttu-id="346db-105">O <xref:System.IDisposable?displayProperty=nameWithType> interface não é abordada nesta seção, mas é abordada no [padrão Dispose](../../../docs/standard/design-guidelines/dispose-pattern.md) seção.</span><span class="sxs-lookup"><span data-stu-id="346db-105">The <xref:System.IDisposable?displayProperty=nameWithType> interface is not covered in this section, but is discussed in the [Dispose Pattern](../../../docs/standard/design-guidelines/dispose-pattern.md) section.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="346db-106">Para obter instruções e informações adicionais sobre outros comum, tipos internos do .NET Framework, consulte os tópicos de referência para o seguinte: <xref:System.DateTime?displayProperty=nameWithType>, <xref:System.DateTimeOffset?displayProperty=nameWithType>, <xref:System.ICloneable?displayProperty=nameWithType>, <xref:System.IComparable%601?displayProperty=nameWithType>, <xref:System.IEquatable%601?displayProperty=nameWithType>, <xref:System.Nullable%601?displayProperty=nameWithType>, <xref:System.Object?displayProperty=nameWithType> , <xref:System.Uri?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="346db-106">For guidelines and additional information about about other common, built-in .NET Framework types, see the reference topics for the following: <xref:System.DateTime?displayProperty=nameWithType>, <xref:System.DateTimeOffset?displayProperty=nameWithType>, <xref:System.ICloneable?displayProperty=nameWithType>, <xref:System.IComparable%601?displayProperty=nameWithType>, <xref:System.IEquatable%601?displayProperty=nameWithType>, <xref:System.Nullable%601?displayProperty=nameWithType>, <xref:System.Object?displayProperty=nameWithType>, <xref:System.Uri?displayProperty=nameWithType>.</span></span>  
  
## <a name="in-this-section"></a><span data-ttu-id="346db-107">Nesta seção</span><span class="sxs-lookup"><span data-stu-id="346db-107">In This Section</span></span>  
 [<span data-ttu-id="346db-108">Matrizes</span><span class="sxs-lookup"><span data-stu-id="346db-108">Arrays</span></span>](../../../docs/standard/design-guidelines/arrays.md)  
 [<span data-ttu-id="346db-109">Atributos</span><span class="sxs-lookup"><span data-stu-id="346db-109">Attributes</span></span>](../../../docs/standard/design-guidelines/attributes.md)  
 [<span data-ttu-id="346db-110">Coleções</span><span class="sxs-lookup"><span data-stu-id="346db-110">Collections</span></span>](/cpp/mfc/collections)  
 [<span data-ttu-id="346db-111">Serialização</span><span class="sxs-lookup"><span data-stu-id="346db-111">Serialization</span></span>](../../../docs/standard/design-guidelines/serialization.md)  
 [<span data-ttu-id="346db-112">Uso de System. XML</span><span class="sxs-lookup"><span data-stu-id="346db-112">System.Xml Usage</span></span>](../../../docs/standard/design-guidelines/system-xml-usage.md)  
 [<span data-ttu-id="346db-113">Operadores de igualdade</span><span class="sxs-lookup"><span data-stu-id="346db-113">Equality Operators</span></span>](../../../docs/standard/design-guidelines/equality-operators.md)  
 <span data-ttu-id="346db-114">*Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*</span><span class="sxs-lookup"><span data-stu-id="346db-114">*Portions © 2005, 2009 Microsoft Corporation. All rights reserved.*</span></span>  
  
 <span data-ttu-id="346db-115">*Reimpressas pela permissão de Pearson educação, Inc. de [diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicados 22 de outubro de 2008, Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*</span><span class="sxs-lookup"><span data-stu-id="346db-115">*Reprinted by permission of Pearson Education, Inc. from [Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) by Krzysztof Cwalina and Brad Abrams, published Oct 22, 2008 by Addison-Wesley Professional as part of the Microsoft Windows Development Series.*</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="346db-116">Consulte também</span><span class="sxs-lookup"><span data-stu-id="346db-116">See Also</span></span>  
 [<span data-ttu-id="346db-117">Diretrizes de design do Framework</span><span class="sxs-lookup"><span data-stu-id="346db-117">Framework Design Guidelines</span></span>](../../../docs/standard/design-guidelines/index.md)