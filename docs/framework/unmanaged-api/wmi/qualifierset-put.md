---
title: Função QualifierSet_Put (referência de API não gerenciada)
description: A função QualifierSet_Put grava qualificador nomeado e seu valor.
ms.date: 11/06/2017
api_name:
- QualifierSet_Put
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Put
helpviewer_keywords:
- QualifierSet_Put function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7b2e1b08d1091e482c6b02fe015a58219ff80768
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43517555"
---
# <a name="qualifiersetput-function"></a>Função QualifierSet_Put
Grava o qualificador nomeado e o valor. O novo qualificador substitui o valor anterior do mesmo nome. Se o qualificador não existir, ele é criado. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT QualifierSet_Put (
   [in] int                  vFunc, 
   [in] IWbemQualifierSet*   ptr, 
   [in] LPCWSTR              wszName,
   [in] VARIANT*             pVal,
   [in] LONG                 lFlavor
); 
```  

## <a name="parameters"></a>Parâmetros

`vFunc`   
[in] Esse parâmetro é usado.

`ptr`   
[in] Um ponteiro para um [IWbemQualifierSet](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemqualifierset) instância.

`wszName`   
[in] O nome do qualificador de escrever.

`pVal` [in] Um ponteiro para um válido `VARIANT` que contém o qualificador de escrever. O parâmetro não pode ser `null`.

`lFlavor` [in] Uma das seguintes constantes que define os tipos de qualificador desejado para esse qualificador. O valor padrão é `WBEM_FLAVOR_OVERRIDABLE` (0).

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_FLAVOR_OVERRIDABLE` | 0 | O qualificador pode ser substituído em uma classe derivada ou instância. **Esse é o valor padrão.** |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_INSTANCE` | 1 | O qualificador é propagado para instâncias. |
| `WBEM_FLAVOR_GLAG_PROPAGATE_TO_DERIVED_CLASS` | 2 | O qualificador é propagado para classes derivadas. |
| ' WBEM_FLAVOR_NOT_OVERRIDABLE | 0x10 | O qualificador não pode ser substituído em uma instância ou classe derivada. |
| ' WBEM_FLAVOR_AMENDED | 0x80 | O qualificador é localizado. |

## <a name="return-value"></a>Valor retornado

Os seguintes valores retornados por essa função são definidos na *WbemCli.h* arquivo de cabeçalho, ou você pode defini-los como constantes em seu código:

|Constante  |Valor  |Descrição  |
|---------|---------|---------|
| `WBEM_E_CANNOT_BE_KEY` | 0x8004101f | Houve uma tentativa inválida de especificar o **chave** qualificador em uma propriedade que não pode ser uma chave. As chaves são especificadas om o c; a definição de ass para um objeto e não podem ser alterados em uma base por instância. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Um parâmetro não é válido. |
| `WBEM_E_INVALID_QUALIFIER_TYPE` | 0x80041029 | O `pVal` parâmetro não é de um tipo de Qualificador legal. |
| `WBEM_E_OVERRIDE_NOT_ALLOWED` | 0x8004101a | Não é possível chamar o `QualifierSet_Put` no qualificador porque o objeto proprietário não permite substituições de método. |
| `WBEM_S_NO_ERROR` | 0 | A chamada de função foi bem-sucedida.  |
  
## <a name="remarks"></a>Comentários

Essa função encapsula uma chamada para o [IWbemQualifierSet::Put](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemqualifierset-put) método.

## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** WMINet_Utils.idl  
  
 **Versões do .NET Framework:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Consulte também  
[WMI e contadores de desempenho (referência de API não gerenciada)](index.md)
