---
title: Como criar um contrato de resposta/solicitação
ms.date: 03/30/2017
ms.assetid: 801d90da-3d45-4284-9c9f-56c8aadb4060
ms.openlocfilehash: 0d41973d04fc75f70011505a3361e71e89a05276
ms.sourcegitcommit: f6343b070f3c66877338a05c8bfb0be9985255e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39220978"
---
# <a name="how-to-create-a-request-reply-contract"></a>Como criar um contrato de resposta/solicitação
Um contrato de solicitação-resposta especifica um método que retorna uma resposta. A resposta deve ser enviada e correlacionada à solicitação de acordo com os termos deste contrato. Mesmo que o método retorna sem resposta (`void` em c#, ou um `Sub` no Visual Basic), a infraestrutura cria e envia uma mensagem vazia ao chamador. Para evitar o envio de uma mensagem de resposta vazia, use um contrato unidirecional para a operação.  
  
### <a name="to-create-a-request-reply-contract"></a>Para criar um contrato de solicitação-resposta  
  
1.  Crie uma interface na linguagem de programação de sua escolha.  
  
2.  Aplicar o <xref:System.ServiceModel.ServiceContractAttribute> à interface de atributo.  
  
3.  Aplicar o <xref:System.ServiceModel.OperationContractAttribute> de atributo para cada método que os clientes podem invocar.  
  
4.  Opcional. Defina o valor da <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> propriedade para `true` para impedir o envio de uma mensagem de resposta vazia. Por padrão, todas as operações são contratos de solicitação-resposta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir define um contrato para um serviço de calculadora fornece `Add` e `Subtract` métodos. O `Multiply` método não é parte do contrato, porque ele não está marcado pelo <xref:System.ServiceModel.OperationContractAttribute> de classe e não está acessível aos clientes.  
  
```csharp
using System.ServiceModel;

[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    // It would be equivalent to write explicitly:
    // [OperationContract(IsOneWay=false)]
    int Add(int a, int b);
    
    [OperationContract]
    int Subtract(int a, int b);
    
    int Multiply(int a, int b)
}
```
  
-   Para obter mais informações sobre como especificar contratos de operação, consulte o <xref:System.ServiceModel.OperationContractAttribute> classe e o <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> propriedade.  
  
-   Aplicando o <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute> atributos faz com que a geração automática de definições de contrato de serviço em um documento de descrição linguagem WSDL (Web Services) quando o serviço é implantado. O documento é baixado por meio do acréscimo `?wsdl` endereço para o serviço de base para o HTTP. Por exemplo, `http://microsoft/CalculatorService?wsdl`  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.ServiceModel.OperationContractAttribute>  
 [Criando contratos de serviço](../../../../docs/framework/wcf/designing-service-contracts.md)  
 [Como criar um contrato duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)
