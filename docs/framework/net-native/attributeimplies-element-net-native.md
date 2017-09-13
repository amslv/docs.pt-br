---
title: Elemento &lt;AttributeImplies&gt; (.NET Nativo)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 82db7193-a860-418b-84fc-fff2fdf2e025
caps.latest.revision: 7
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2fcb3f476a00f00e00eeea90db75699c2c4cdf76
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="ltattributeimpliesgt-element-net-native"></a><span data-ttu-id="ce10d-102">Elemento &lt;AttributeImplies&gt; (.NET Nativo)</span><span class="sxs-lookup"><span data-stu-id="ce10d-102">&lt;AttributeImplies&gt; Element (.NET Native)</span></span>
<span data-ttu-id="ce10d-103">Define a política para os elementos de código ao qual o atributo recipiente é aplicado.</span><span class="sxs-lookup"><span data-stu-id="ce10d-103">Defines policy for code elements the containing attribute is applied to.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ce10d-104">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="ce10d-104">Syntax</span></span>  
  
```xml  
<AttributeImplies Activate="policy_type"  
                  Browse="policy_type"  
                  Dynamic="policy_type"  
                  Serialize="policy_type"   
                  DataContractSerializer="policy_setting"  
                  DataContractJsonSerializer="policy_setting"  
                  XmlSerializer="policy_setting"  
                  MarshalObject="policy_setting"  
                  MarshalDelegate="policy_setting"  
                  MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a><span data-ttu-id="ce10d-105">Atributos e elementos</span><span class="sxs-lookup"><span data-stu-id="ce10d-105">Attributes and Elements</span></span>  
 <span data-ttu-id="ce10d-106">As seções a seguir descrevem atributos, elementos filho e elementos pai.</span><span class="sxs-lookup"><span data-stu-id="ce10d-106">The following sections describe attributes, child elements, and parent elements.</span></span>  
  
### <a name="attributes"></a><span data-ttu-id="ce10d-107">Atributos</span><span class="sxs-lookup"><span data-stu-id="ce10d-107">Attributes</span></span>  
  
|<span data-ttu-id="ce10d-108">Atributo</span><span class="sxs-lookup"><span data-stu-id="ce10d-108">Attribute</span></span>|<span data-ttu-id="ce10d-109">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="ce10d-109">Attribute type</span></span>|<span data-ttu-id="ce10d-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="ce10d-110">Description</span></span>|  
|---------------|--------------------|-----------------|  
|`Activate`|<span data-ttu-id="ce10d-111">Reflexão</span><span class="sxs-lookup"><span data-stu-id="ce10d-111">Reflection</span></span>|<span data-ttu-id="ce10d-112">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-112">Optional attribute.</span></span> <span data-ttu-id="ce10d-113">Controla o acesso de tempo de execução a construtores para habilitar a ativação de instâncias.</span><span class="sxs-lookup"><span data-stu-id="ce10d-113">Controls runtime access to constructors to enable activation of instances.</span></span>|  
|`Browse`|<span data-ttu-id="ce10d-114">Reflexão</span><span class="sxs-lookup"><span data-stu-id="ce10d-114">Reflection</span></span>|<span data-ttu-id="ce10d-115">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-115">Optional attribute.</span></span> <span data-ttu-id="ce10d-116">Controla a consulta para obter informações sobre elementos do programa, mas não permite qualquer acesso de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ce10d-116">Controls querying for information about program elements, but does not enable any runtime access.</span></span>|  
|`Dynamic`|<span data-ttu-id="ce10d-117">Reflexão</span><span class="sxs-lookup"><span data-stu-id="ce10d-117">Reflection</span></span>|<span data-ttu-id="ce10d-118">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-118">Optional attribute.</span></span> <span data-ttu-id="ce10d-119">Controla o acesso a todos os tipos de membro ao tempo de execução, incluindo construtores, métodos, campos, propriedades e eventos, habilitando a programação dinâmica.</span><span class="sxs-lookup"><span data-stu-id="ce10d-119">Controls runtime access to all type members, including constructors, methods, fields, properties, and events, to enable dynamic programming.</span></span>|  
|`Serialize`|<span data-ttu-id="ce10d-120">Serialização</span><span class="sxs-lookup"><span data-stu-id="ce10d-120">Serialization</span></span>|<span data-ttu-id="ce10d-121">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-121">Optional attribute.</span></span> <span data-ttu-id="ce10d-122">Controla o acesso ao tempo de execução para construtores, campos e propriedades para habilitar a serialização e desserialização das instâncias por bibliotecas como o serializador Newtonsoft JSON.</span><span class="sxs-lookup"><span data-stu-id="ce10d-122">Controls runtime access to constructors, fields, and properties, to enable type instances to be serialized and deserialized by libraries such as the Newtonsoft JSON serializer.</span></span>|  
|`DataContractSerializer`|<span data-ttu-id="ce10d-123">Serialização</span><span class="sxs-lookup"><span data-stu-id="ce10d-123">Serialization</span></span>|<span data-ttu-id="ce10d-124">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-124">Optional attribute.</span></span> <span data-ttu-id="ce10d-125">Controla a política de serialização que usa a classe <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="ce10d-125">Controls policy for serialization that uses the <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> class.</span></span>|  
|`DataContractJsonSerializer`|<span data-ttu-id="ce10d-126">Serialização</span><span class="sxs-lookup"><span data-stu-id="ce10d-126">Serialization</span></span>|<span data-ttu-id="ce10d-127">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-127">Optional attribute.</span></span> <span data-ttu-id="ce10d-128">Controla a política de serialização JSON que usa a classe <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="ce10d-128">Controls policy for JSON serialization that uses the <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> class.</span></span>|  
|`XmlSerializer`|<span data-ttu-id="ce10d-129">Serialização</span><span class="sxs-lookup"><span data-stu-id="ce10d-129">Serialization</span></span>|<span data-ttu-id="ce10d-130">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-130">Optional attribute.</span></span> <span data-ttu-id="ce10d-131">Controla a política de serialização XML que usa a classe <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="ce10d-131">Controls policy for XML serialization that uses the <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> class.</span></span>|  
|`MarshalObject`|<span data-ttu-id="ce10d-132">Interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="ce10d-132">Interop</span></span>|<span data-ttu-id="ce10d-133">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-133">Optional attribute.</span></span> <span data-ttu-id="ce10d-134">Política de controles de marshaling de tipos de referência para o Tempo de Execução do Windows e COM.</span><span class="sxs-lookup"><span data-stu-id="ce10d-134">Controls policy for marshaling reference types to Windows Runtime and COM.</span></span>|  
|`MarshalDelegate`|<span data-ttu-id="ce10d-135">Interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="ce10d-135">Interop</span></span>|<span data-ttu-id="ce10d-136">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-136">Optional attribute.</span></span> <span data-ttu-id="ce10d-137">Controla a diretiva de marshaling de tipos delegados como ponteiros de função para código nativo.</span><span class="sxs-lookup"><span data-stu-id="ce10d-137">Controls policy for marshaling delegate types as function pointers to native code.</span></span>|  
|`MarshalStructure`|<span data-ttu-id="ce10d-138">Interoperabilidade</span><span class="sxs-lookup"><span data-stu-id="ce10d-138">Interop</span></span>|<span data-ttu-id="ce10d-139">Atributo opcional.</span><span class="sxs-lookup"><span data-stu-id="ce10d-139">Optional attribute.</span></span> <span data-ttu-id="ce10d-140">Controla a política de marshaling de tipos de valor para código nativo.</span><span class="sxs-lookup"><span data-stu-id="ce10d-140">Controls policy for marshaling value types to native code.</span></span>|  
  
## <a name="all-attributes"></a><span data-ttu-id="ce10d-141">Todos os atributos</span><span class="sxs-lookup"><span data-stu-id="ce10d-141">All attributes</span></span>  
  
|<span data-ttu-id="ce10d-142">Valor</span><span class="sxs-lookup"><span data-stu-id="ce10d-142">Value</span></span>|<span data-ttu-id="ce10d-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="ce10d-143">Description</span></span>|  
|-----------|-----------------|  
|<span data-ttu-id="ce10d-144">*policy_setting*</span><span class="sxs-lookup"><span data-stu-id="ce10d-144">*policy_setting*</span></span>|<span data-ttu-id="ce10d-145">A configuração a ser aplicada a este tipo de política.</span><span class="sxs-lookup"><span data-stu-id="ce10d-145">The setting to apply to this policy type.</span></span> <span data-ttu-id="ce10d-146">Os valores possíveis são `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`.</span><span class="sxs-lookup"><span data-stu-id="ce10d-146">Possible values are `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal`, and `Required All`.</span></span> <span data-ttu-id="ce10d-147">Para obter mais informações, consulte [Configurações da política da diretiva de tempo de execução](../../../docs/framework/net-native/runtime-directive-policy-settings.md).</span><span class="sxs-lookup"><span data-stu-id="ce10d-147">For more information, see [Runtime Directive Policy Settings](../../../docs/framework/net-native/runtime-directive-policy-settings.md).</span></span>|  
  
### <a name="child-elements"></a><span data-ttu-id="ce10d-148">Elementos filho</span><span class="sxs-lookup"><span data-stu-id="ce10d-148">Child Elements</span></span>  
 <span data-ttu-id="ce10d-149">nenhuma.</span><span class="sxs-lookup"><span data-stu-id="ce10d-149">None.</span></span>  
  
### <a name="parent-elements"></a><span data-ttu-id="ce10d-150">Elementos pai</span><span class="sxs-lookup"><span data-stu-id="ce10d-150">Parent Elements</span></span>  
  
|<span data-ttu-id="ce10d-151">Elemento</span><span class="sxs-lookup"><span data-stu-id="ce10d-151">Element</span></span>|<span data-ttu-id="ce10d-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="ce10d-152">Description</span></span>|  
|-------------|-----------------|  
|[<span data-ttu-id="ce10d-153">\<Type></span><span class="sxs-lookup"><span data-stu-id="ce10d-153">\<Type></span></span>](../../../docs/framework/net-native/type-element-net-native.md)|<span data-ttu-id="ce10d-154">Aplica a política de reflexão a um tipo e todos os seus membros.</span><span class="sxs-lookup"><span data-stu-id="ce10d-154">Applies reflection policy to a type and all its members.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ce10d-155">Comentários</span><span class="sxs-lookup"><span data-stu-id="ce10d-155">Remarks</span></span>  
 <span data-ttu-id="ce10d-156">O elemento `<AttributeImplies>` é usado se o seu tipo recipiente for um atributo (isto é, uma classe derivada de <xref:System.Attribute?displayProperty=fullName>).</span><span class="sxs-lookup"><span data-stu-id="ce10d-156">The `<AttributeImplies>` element is used if its containing type is an attribute (that is, a class derived from <xref:System.Attribute?displayProperty=fullName>).</span></span> <span data-ttu-id="ce10d-157">Se o atributo for aplicado a um elemento de programa específico, a política definida pelo elemento `<AttributeImplies>` aplica-se a esse elemento de programa.</span><span class="sxs-lookup"><span data-stu-id="ce10d-157">If the attribute is applied to a particular program element, the policy defined by the `<AttributeImplies>` element applies to that program element.</span></span>  
  
 <span data-ttu-id="ce10d-158">Os atributos de reflexão, serialização e interoperabilidade são todos opcionais, embora pelo menos um deve estar presente.</span><span class="sxs-lookup"><span data-stu-id="ce10d-158">The reflection, serialization, and interop attributes are all optional, although at least one should be present.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ce10d-159">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ce10d-159">See Also</span></span>  
 <span data-ttu-id="ce10d-160">[\<Elemento Type>](../../../docs/framework/net-native/type-element-net-native.md) </span><span class="sxs-lookup"><span data-stu-id="ce10d-160">[\<Type> Element](../../../docs/framework/net-native/type-element-net-native.md) </span></span>  
 <span data-ttu-id="ce10d-161">[Referência do arquivo de configuração das diretivas de tempo de execução (rd.xml)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md) </span><span class="sxs-lookup"><span data-stu-id="ce10d-161">[Runtime Directives (rd.xml) Configuration File Reference](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md) </span></span>  
 <span data-ttu-id="ce10d-162">[Elementos da diretiva de tempo de execução](../../../docs/framework/net-native/runtime-directive-elements.md) </span><span class="sxs-lookup"><span data-stu-id="ce10d-162">[Runtime Directive Elements](../../../docs/framework/net-native/runtime-directive-elements.md) </span></span>  
 [<span data-ttu-id="ce10d-163">Configurações da política da diretiva de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="ce10d-163">Runtime Directive Policy Settings</span></span>](../../../docs/framework/net-native/runtime-directive-policy-settings.md)
