---
title: Binding2
ms.date: 03/30/2017
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
ms.openlocfilehash: 84e304f3dedcbd785d6238e6cb5eb142c288b995
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50033827"
---
# <a name="binding"></a>Associação
WMI de associação  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>Métodos  
 A classe de associação não define quaisquer métodos.  
  
## <a name="properties"></a>Propriedades  
 A classe Binding tem as seguintes propriedades.  
  
### <a name="bindingelements"></a>BindingElements  
 Tipo de dados: matriz BindingElement  
  
 Tipo de acesso: somente leitura  
  
 A coleção de elementos implementados pela associação de associação.  
  
### <a name="closetimeout"></a>closeTimeout  
 Tipo de dados: datetime  
  
 Tipo de acesso: somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação close.  
  
### <a name="name"></a>Nome  
 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: somente leitura  
  
 O nome da associação.  
  
### <a name="namespace"></a>Namespace  
 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: somente leitura  
  
 O namespace XML da associação.  
  
### <a name="opentimeout"></a>openTimeout  
 Tipo de dados: datetime  
  
 Tipo de acesso: somente leitura  
  
 O intervalo de tempo fornecido para a conclusão de uma operação open.  
  
### <a name="receivetimeout"></a>receiveTimeout  
 Tipo de dados: datetime  
  
 Tipo de acesso: somente leitura  
  
 O intervalo de tempo fornecido para uma operação de recebimento ser concluída.  
  
### <a name="scheme"></a>Esquema  
 Tipo de dados: cadeia de caracteres  
  
 Tipo de acesso: somente leitura  
  
 O esquema de transporte URI que é usado pelas fábricas de canal e de ouvinte que são criadas pela associação.  
  
### <a name="sendtimeout"></a>sendTimeout  
 Tipo de dados: datetime  
  
 Tipo de acesso: somente leitura  
  
 O intervalo de tempo fornecido para uma operação de envio ser concluída.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em Servicemodel.mof.|  
|---------|-----------------------------------|  
|Namespace|Definido no root\ServiceModel|  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Channels.Binding>
