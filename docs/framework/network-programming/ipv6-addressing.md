---
title: "Endereçamento IPv6"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Internet Protocol version 6, addresses in
- Neighbor Discovery
- IPv6, enabling
- IPv6, mobility and
- Internet Protocol version 6, anycast addresses
- IPv6, Neighbor Discovery
- Internet Protocol version 6, auto-configuring
- Internet Protocol version 6, enabling
- IPv6, unicast addresses
- IPv6, auto-configuring
- Internet Protocol version 6, routing
- IPv6, RFC documents
- IPv6, routing
- Internet Protocol version 6, disabling
- Internet Protocol version 6, unicast addresses
- IPv6, multicast addresses
- Internet Protocol version 6, mobility and
- Internet Protocol version 6, RFC documents
- Internet Protocol version 6, Neighbor Discovery
- IPv6, anycast addresses
- Internet Protocol version 6, multicast addresses
- IPv6, addresses in
- IPv6, disabling
ms.assetid: 20a104ae-1649-4649-a005-531a5cf74c93
caps.latest.revision: 10
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6d810d9fdf6f0e464147e639d9a3acf2ebc148d9
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="ipv6-addressing"></a><span data-ttu-id="61681-102">Endereçamento IPv6</span><span class="sxs-lookup"><span data-stu-id="61681-102">IPv6 Addressing</span></span>
<span data-ttu-id="61681-103">No protocolo IP versão 6 (IPv6), os endereços têm tamanho de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="61681-103">In the Internet Protocol version 6 (IPv6), addresses are 128 bits long.</span></span> <span data-ttu-id="61681-104">Um motivo para um espaço de endereço tão grande é subdividir os endereços disponíveis em uma hierarquia de domínios de roteamento que reflitam a topologia da Internet.</span><span class="sxs-lookup"><span data-stu-id="61681-104">One reason for such a large address space is to subdivide the available addresses into a hierarchy of routing domains that reflect the Internet's topology.</span></span> <span data-ttu-id="61681-105">Outro motivo é mapear os endereços de adaptadores de rede (ou interfaces) que conectam dispositivos à rede.</span><span class="sxs-lookup"><span data-stu-id="61681-105">Another reason is to map the addresses of network adapters (or interfaces) that connect devices to the network.</span></span> <span data-ttu-id="61681-106">O IPv6 tem uma capacidade inerente de resolver endereços no nível mais baixo deles, que é o nível de adaptador de rede e também tem capacidades de configuração automática.</span><span class="sxs-lookup"><span data-stu-id="61681-106">IPv6 features an inherent capability to resolve addresses at their lowest level, which is at the network interface level, and also has auto-configuration capabilities.</span></span>  
  
## <a name="text-representation"></a><span data-ttu-id="61681-107">Representação de texto</span><span class="sxs-lookup"><span data-stu-id="61681-107">Text Representation</span></span>  
 <span data-ttu-id="61681-108">A seguir estão as três formas convencionais usadas para representar os endereços IPv6 como cadeias de caracteres de texto:</span><span class="sxs-lookup"><span data-stu-id="61681-108">The following are the three conventional forms used to represent the IPv6 addresses as text strings:</span></span>  
  
-   <span data-ttu-id="61681-109">**Forma hexadecimal com dois-pontos**.</span><span class="sxs-lookup"><span data-stu-id="61681-109">**Colon-hexadecimal form**.</span></span> <span data-ttu-id="61681-110">Esta é a forma preferencial: n:n:n:n:n:n:n:n.</span><span class="sxs-lookup"><span data-stu-id="61681-110">This is the preferred form n:n:n:n:n:n:n:n.</span></span> <span data-ttu-id="61681-111">Cada n representa o valor hexadecimal de um dos oito elementos de 16 bits do endereço.</span><span class="sxs-lookup"><span data-stu-id="61681-111">Each n represents the hexadecimal value of one of the eight 16-bit elements of the address.</span></span> <span data-ttu-id="61681-112">Por exemplo: `3FFE:FFFF:7654:FEDA:1245:BA98:3210:4562`.</span><span class="sxs-lookup"><span data-stu-id="61681-112">For example: `3FFE:FFFF:7654:FEDA:1245:BA98:3210:4562`.</span></span>  
  
-   <span data-ttu-id="61681-113">**Forma compactada**.</span><span class="sxs-lookup"><span data-stu-id="61681-113">**Compressed form**.</span></span> <span data-ttu-id="61681-114">Devido ao tamanho de endereço, é comum ter endereços que contêm uma cadeia de caracteres longa de zeros.</span><span class="sxs-lookup"><span data-stu-id="61681-114">Due to the address length, it is common to have addresses containing a long string of zeros.</span></span> <span data-ttu-id="61681-115">Para simplificar a gravar esses endereços, use o formato compactado, em que uma única sequência contígua de blocos de 0 é representada por um símbolo de dois-pontos duplos (::).</span><span class="sxs-lookup"><span data-stu-id="61681-115">To simplify writing these addresses, use the compressed form, in which a single contiguous sequence of 0 blocks are represented by a double-colon symbol (::).</span></span> <span data-ttu-id="61681-116">Este símbolo pode aparecer apenas uma vez em um endereço.</span><span class="sxs-lookup"><span data-stu-id="61681-116">This symbol can appear only once in an address.</span></span> <span data-ttu-id="61681-117">Por exemplo, o endereço multicast `FFED:0:0:0:0:BA98:3210:4562` torna-se `FFED::BA98:3210:4562` no formato compactado.</span><span class="sxs-lookup"><span data-stu-id="61681-117">For example, the multicast address `FFED:0:0:0:0:BA98:3210:4562` in compressed form is `FFED::BA98:3210:4562`.</span></span> <span data-ttu-id="61681-118">O endereço unicast `3FFE:FFFF:0:0:8:800:20C4:0` em formato compactado é `3FFE:FFFF::8:800:20C4:0`.</span><span class="sxs-lookup"><span data-stu-id="61681-118">The unicast address `3FFE:FFFF:0:0:8:800:20C4:0` in compressed form is `3FFE:FFFF::8:800:20C4:0`.</span></span> <span data-ttu-id="61681-119">O endereço de loopback `0:0:0:0:0:0:0:1` em formato compactado é `::`1.</span><span class="sxs-lookup"><span data-stu-id="61681-119">The loopback address `0:0:0:0:0:0:0:1` in compressed form is `::`1.</span></span> <span data-ttu-id="61681-120">O endereço não especificado `0:0:0:0:0:0:0:0` em formato compactado é `::`.</span><span class="sxs-lookup"><span data-stu-id="61681-120">The unspecified address `0:0:0:0:0:0:0:0` in compressed form is `::`.</span></span>  
  
-   <span data-ttu-id="61681-121">**Formato misto**.</span><span class="sxs-lookup"><span data-stu-id="61681-121">**Mixed form**.</span></span> <span data-ttu-id="61681-122">Esse formato combina os endereços IPv4 e IPv6.</span><span class="sxs-lookup"><span data-stu-id="61681-122">This form combines IPv4 and IPv6 addresses.</span></span> <span data-ttu-id="61681-123">Nesse caso, o formato de endereço é n:n:n:n:n:n:d.d.d.d, em que cada n representa os valores hexadecimais dos seis elementos do endereço de 16 bits superiores de IPv6 e cada d representa o valor decimal de um endereço IPv4.</span><span class="sxs-lookup"><span data-stu-id="61681-123">In this case, the address format is n:n:n:n:n:n:d.d.d.d, where each n represents the hexadecimal values of the six IPv6 high-order 16-bit address elements, and each d represents the decimal value of an IPv4 address.</span></span>  
  
## <a name="address-types"></a><span data-ttu-id="61681-124">Tipos de endereço</span><span class="sxs-lookup"><span data-stu-id="61681-124">Address Types</span></span>  
 <span data-ttu-id="61681-125">Os bits à esquerda do endereço definem o tipo específico de endereço IPv6.</span><span class="sxs-lookup"><span data-stu-id="61681-125">The leading bits in the address define the specific IPv6 address type.</span></span> <span data-ttu-id="61681-126">O campo de comprimento variável que contém esses bits à esquerda é chamado de um FP (prefixo de formato).</span><span class="sxs-lookup"><span data-stu-id="61681-126">The variable-length field containing these leading bits is called a Format Prefix (FP).</span></span>  
  
 <span data-ttu-id="61681-127">Um endereço unicast IPv6 é dividido em duas partes.</span><span class="sxs-lookup"><span data-stu-id="61681-127">An IPv6 unicast address is divided into two parts.</span></span> <span data-ttu-id="61681-128">A primeira parte contém o prefixo de endereço e a segunda parte contém o identificador de interface.</span><span class="sxs-lookup"><span data-stu-id="61681-128">The first part contains the address prefix, and the second part contains the interface identifier.</span></span> <span data-ttu-id="61681-129">Uma maneira concisa de expressar uma combinação de endereço IPv6/prefixo é a seguinte: endereço ipv6/comprimento do prefixo.</span><span class="sxs-lookup"><span data-stu-id="61681-129">A concise way to express an IPv6 address/prefix combination is as follows: ipv6-address/prefix-length.</span></span>  
  
 <span data-ttu-id="61681-130">A seguir, um exemplo de um endereço com um prefixo de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="61681-130">The following is an example of an address with a 64-bit prefix.</span></span>  
  
 <span data-ttu-id="61681-131">`3FFE:FFFF:0:CD30:0:0:0:0/64`.</span><span class="sxs-lookup"><span data-stu-id="61681-131">`3FFE:FFFF:0:CD30:0:0:0:0/64`.</span></span>  
  
 <span data-ttu-id="61681-132">O prefixo neste exemplo é `3FFE:FFFF:0:CD30`.</span><span class="sxs-lookup"><span data-stu-id="61681-132">The prefix in this example is `3FFE:FFFF:0:CD30`.</span></span> <span data-ttu-id="61681-133">O endereço também pode ser gravado em um formato compactado, como `3FFE:FFFF:0:CD30::/64`.</span><span class="sxs-lookup"><span data-stu-id="61681-133">The address can also be written in a compressed form, as `3FFE:FFFF:0:CD30::/64`.</span></span>  
  
 <span data-ttu-id="61681-134">O IPv6 define os seguintes tipos de endereço:</span><span class="sxs-lookup"><span data-stu-id="61681-134">IPv6 defines the following address types:</span></span>  
  
-   <span data-ttu-id="61681-135">**Endereço unicast**.</span><span class="sxs-lookup"><span data-stu-id="61681-135">**Unicast address**.</span></span> <span data-ttu-id="61681-136">Um identificador para uma única interface.</span><span class="sxs-lookup"><span data-stu-id="61681-136">An identifier for a single interface.</span></span> <span data-ttu-id="61681-137">Um pacote enviado para esse endereço é entregue para a interface identificada.</span><span class="sxs-lookup"><span data-stu-id="61681-137">A packet sent to this address is delivered to the identified interface.</span></span> <span data-ttu-id="61681-138">Os endereços unicast são diferenciados dos endereços multicast pelo valor do octeto superior.</span><span class="sxs-lookup"><span data-stu-id="61681-138">The unicast addresses are distinguished from the multicast addresses by the value of the high-order octet.</span></span> <span data-ttu-id="61681-139">O octeto superior dos endereços multicast tem o valor hexadecimal FF.</span><span class="sxs-lookup"><span data-stu-id="61681-139">The multicast addresses' high-order octet has the hexadecimal value of FF.</span></span> <span data-ttu-id="61681-140">Qualquer outro valor para esse octeto identifica um endereço unicast.</span><span class="sxs-lookup"><span data-stu-id="61681-140">Any other value for this octet identifies a unicast address.</span></span> <span data-ttu-id="61681-141">Estes são os diferentes tipos de endereço unicast:</span><span class="sxs-lookup"><span data-stu-id="61681-141">The following are different types of unicast addresses:</span></span>  
  
    -   <span data-ttu-id="61681-142">**Endereços de link local**.</span><span class="sxs-lookup"><span data-stu-id="61681-142">**Link-local addresses**.</span></span> <span data-ttu-id="61681-143">Esses endereços são usados em um único link e têm o seguinte formato: FE80::*InterfaceID*.</span><span class="sxs-lookup"><span data-stu-id="61681-143">These addresses are used on a single link and have the following format: FE80::*InterfaceID*.</span></span> <span data-ttu-id="61681-144">Endereços de conexões locais são usados entre os nós em um link para a configuração automática de endereços, descoberta de vizinhos ou ainda quando nenhum dos roteadores está presente.</span><span class="sxs-lookup"><span data-stu-id="61681-144">Link-local addresses are used between nodes on a link for auto-address configuration, neighbor discovery, or when no routers are present.</span></span> <span data-ttu-id="61681-145">Um endereço de link local é usado principalmente na inicialização e quando o sistema ainda não adquiriu endereços de escopo mais amplo.</span><span class="sxs-lookup"><span data-stu-id="61681-145">A link-local address is used primarily at startup and when the system has not yet acquired addresses of larger scope.</span></span>  
  
    -   <span data-ttu-id="61681-146">**Endereços de site local**.</span><span class="sxs-lookup"><span data-stu-id="61681-146">**Site-local addresses**.</span></span> <span data-ttu-id="61681-147">Esses endereços são usados em um único site e têm o seguinte formato: FEC0::*SubnetID*:*InterfaceID*.</span><span class="sxs-lookup"><span data-stu-id="61681-147">These addresses are used on a single site and have the following format: FEC0::*SubnetID*:*InterfaceID*.</span></span> <span data-ttu-id="61681-148">Os endereços de sites locais são usados para endereçamento dentro de um site sem a necessidade de um prefixo global.</span><span class="sxs-lookup"><span data-stu-id="61681-148">The site-local addresses are used for addressing inside a site without the need for a global prefix.</span></span>  
  
    -   <span data-ttu-id="61681-149">**Endereços unicast IPv6 globais**.</span><span class="sxs-lookup"><span data-stu-id="61681-149">**Global IPv6 unicast addresses**.</span></span> <span data-ttu-id="61681-150">Esses endereços podem ser usados pela Internet e têm o seguinte formato: 010(FP, 3 bits) ID de TLA (13 bits) Reserved (8 bits) ID de NLA (24 bits) ID de SLA (16 bits) *InterfaceID* (64 bits).</span><span class="sxs-lookup"><span data-stu-id="61681-150">These addresses can be used across the Internet and have the following format: 010(FP, 3 bits) TLA ID (13 bits) Reserved (8 bits) NLA ID (24 bits) SLA ID (16 bits) *InterfaceID* (64 bits).</span></span>  
  
-   <span data-ttu-id="61681-151">**Endereço multicast**.</span><span class="sxs-lookup"><span data-stu-id="61681-151">**Multicast address**.</span></span> <span data-ttu-id="61681-152">Um identificador para um conjunto de interfaces (normalmente pertencentes a nós diferentes).</span><span class="sxs-lookup"><span data-stu-id="61681-152">An identifier for a set of interfaces (typically belonging to different nodes).</span></span> <span data-ttu-id="61681-153">Um pacote enviado para esse endereço será enviado para todas as interfaces identificadas pelo endereço.</span><span class="sxs-lookup"><span data-stu-id="61681-153">A packet sent to this address is delivered to all the interfaces identified by the address.</span></span> <span data-ttu-id="61681-154">Os tipos de endereço multicast substituem os endereços difundidos por IPv4.</span><span class="sxs-lookup"><span data-stu-id="61681-154">The multicast address types supersede the IPv4 broadcast addresses.</span></span>  
  
-   <span data-ttu-id="61681-155">**Endereço anycast**.</span><span class="sxs-lookup"><span data-stu-id="61681-155">**Anycast address**.</span></span> <span data-ttu-id="61681-156">Um identificador para um conjunto de interfaces (normalmente pertencentes a nós diferentes).</span><span class="sxs-lookup"><span data-stu-id="61681-156">An identifier for a set of interfaces (typically belonging to different nodes).</span></span> <span data-ttu-id="61681-157">Um pacote enviado para esse endereço será enviado para apenas uma interface identificada pelo endereço.</span><span class="sxs-lookup"><span data-stu-id="61681-157">A packet sent to this address is delivered to only one interface identified by the address.</span></span> <span data-ttu-id="61681-158">Essa é a interface mais próxima conforme identificado pela métrica de roteamento.</span><span class="sxs-lookup"><span data-stu-id="61681-158">This is the nearest interface as identified by routing metrics.</span></span> <span data-ttu-id="61681-159">Endereços anycast são obtidos do espaço de endereço unicast e não é possível diferenciá-los sintaticamente.</span><span class="sxs-lookup"><span data-stu-id="61681-159">Anycast addresses are taken from the unicast address space and are not syntactically distinguishable.</span></span> <span data-ttu-id="61681-160">A interface endereçada faz a distinção entre endereços unicast e anycast como uma função de sua configuração.</span><span class="sxs-lookup"><span data-stu-id="61681-160">The addressed interface performs the distinction between unicast and anycast addresses as a function of its configuration.</span></span>  
  
 <span data-ttu-id="61681-161">Em geral, um nó sempre tem um endereço de link local.</span><span class="sxs-lookup"><span data-stu-id="61681-161">In general, a node always has a link-local address.</span></span> <span data-ttu-id="61681-162">Ele pode ter um endereço de site local e um ou mais endereços globais.</span><span class="sxs-lookup"><span data-stu-id="61681-162">It might have a site-local address and one or more global addresses.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="61681-163">Consulte também</span><span class="sxs-lookup"><span data-stu-id="61681-163">See Also</span></span>  
 <span data-ttu-id="61681-164">[Protocolo IP versão 6](../../../docs/framework/network-programming/internet-protocol-version-6.md) </span><span class="sxs-lookup"><span data-stu-id="61681-164">[Internet Protocol Version 6](../../../docs/framework/network-programming/internet-protocol-version-6.md) </span></span>  
 [<span data-ttu-id="61681-165">Soquetes</span><span class="sxs-lookup"><span data-stu-id="61681-165">Sockets</span></span>](../../../docs/framework/network-programming/sockets.md)
