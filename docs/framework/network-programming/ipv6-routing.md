---
title: Roteamento IPv6
ms.date: 03/30/2017
ms.assetid: c98731b4-b542-46a2-9947-1cea63c186b2
author: mcleblanc
ms.author: markl
ms.openlocfilehash: 4ff5f131cfd9fac48e653b98e05d5e46dcfb0bec
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2018
ms.locfileid: "47399015"
---
# <a name="ipv6-routing"></a>Roteamento IPv6
Um mecanismo de roteamento flexível é uma vantagem do IPv6. Devido à maneira que as IDs de rede IPv4 foram e são alocadas, grandes tabelas de roteamento precisam ser mantidas pelos roteadores que estão nos backbones da Internet. Esses roteadores devem saber todas as rotas para encaminhar pacotes que são potencialmente direcionados para qualquer nó na Internet. Com sua capacidade de agregar endereços, o IPv6 permite endereçamento flexível e reduz consideravelmente o tamanho das tabelas de roteamento. Nessa nova arquitetura de endereçamento, os roteadores intermediários devem controlar apenas a parte local de sua rede para encaminhar as mensagens corretamente.  
  
## <a name="neighbor-discovery"></a>Descoberta de vizinhos  
 Estes são alguns dos recursos fornecidos pela descoberta de vizinhos:  
  
-   Descoberta de roteador. Isso permite que os hosts identifiquem os roteadores locais.  
  
-   Resolução de endereço. Isso permite que os nós resolvam um endereço de camada de link para um endereço de próximo salto correspondente (uma substituição para o protocolo de resolução de endereço [ARP]).  
  
-   Configuração automática de endereço. Isso permite que os hosts configurem automaticamente os endereços locais e globais de sites.  
  
 A descoberta de vizinho usa protocolo ICMP para mensagens IPv6 (ICMPv6) que incluem:  
  
-   Anúncio de roteador. Enviado por um roteador psudoperiodicamente ou em resposta a uma solicitação de roteador. Os roteadores IPv6 usam anúncios de roteador para anunciar a própria disponibilidade, prefixos de endereço e outros parâmetros.  
  
-   Solicitação de roteador. Enviada por um host para solicitar que os roteadores no link enviem um anúncio de roteador imediatamente.  
  
-   Solicitação de vizinho. Enviado por nós para resolução de endereço, para detecção de endereço duplicado ou para verificar se um vizinho ainda pode ser acessado.  
  
-   Anúncio de vizinho. Enviado por nós para responder a uma solicitação de vizinho ou para notificar vizinhos de uma alteração no endereço de camada de link.  
  
-   Redirecionamento. Enviado por roteadores a fim de indicar um melhor endereço de próximo salto para um destino específico para um nó de envio.  
  
## <a name="see-also"></a>Consulte também  
 [Protocolo IP versão 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)  
 [Soquetes](../../../docs/framework/network-programming/sockets.md)
