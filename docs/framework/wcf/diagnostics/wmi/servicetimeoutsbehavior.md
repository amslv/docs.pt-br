---
title: ServiceTimeoutsBehavior
ms.date: 03/30/2017
ms.assetid: 4412525d-a3cc-4eae-b3e8-a50ce766d09d
ms.openlocfilehash: 1a5284915de739e95325234318842a4d1ab607be
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50135235"
---
# <a name="servicetimeoutsbehavior"></a>ServiceTimeoutsBehavior
ServiceTimeoutsBehavior  
  
## <a name="syntax"></a>Sintaxe  
  
```csharp
class ServiceTimeoutsBehavior : Behavior  
{  
  datetime TransactionTimeout;  
};  
```  
  
## <a name="methods"></a>Métodos  
 A classe ServiceTimeoutsBehavior não define quaisquer métodos.  
  
## <a name="properties"></a>Propriedades  
 A classe ServiceTimeoutsBehavior tem a seguinte propriedade:  
  
### <a name="transactiontimeout"></a>TransactionTimeout  
 Tipo de dados: datetime  
  
 Tipo de acesso: somente leitura  
  
 O período dentro do qual uma transação deve ser concluída.  
  
## <a name="requirements"></a>Requisitos  
  
|MOF|Declarado em Servicemodel.mof.|  
|---------|-----------------------------------|  
|Namespace|Definido no root\ServiceModel|  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.Configuration.ServiceTimeoutsElement>
