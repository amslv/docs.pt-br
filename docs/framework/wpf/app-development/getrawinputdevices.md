---
title: GetRawInputDevices
ms.date: 03/30/2017
helpviewer_keywords:
- raw input [WPF]
ms.assetid: c4d37ecd-065a-4d1c-9e6c-26804ae968ca
ms.openlocfilehash: 0cb1184ddc3e8051a68dfed12367dea65a06b623
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50034477"
---
# <a name="getrawinputdevices"></a>GetRawInputDevices
Permite ao PresentationHost.exe descobrir e registrar os dispositivos de dados brutos (dispositivos de interface humana) no qual o aplicativo host está interessado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetRawInputDevices( [out] IEnumRAWINPUTDEVICE **ppEnum );  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppEnum`  
  
 [out] Um ponteiro para um [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md) para enumerar os dispositivos de entrada brutos.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 HRESULT:  
  
 S_OK – [IEnumRAWINPUTDEVICE](../../../../docs/framework/wpf/app-development/ienumrawinputdevice.md) só será usado pelo PresentationHost.exe se S_OK será retornado.  
  
 E_NOTIMPL  
  
## <a name="remarks"></a>Comentários  
 Dispositivos de dados brutos são o conjunto de dispositivos de entrada que inclui os teclados, mouses e dispositivos menos tradicionais como controles remotos.  
  
 Depois que a lista de dispositivos brutos de entrada tiver sido recuperada, PresentationHost.exe registra nos dispositivos para receber mensagens de notificação de WM_INPUT.  
  
## <a name="see-also"></a>Consulte também  
 [GetRawInputDeviceList](/windows/desktop/api/winuser/nf-winuser-getrawinputdevicelist)  
 [FilterInputMessage](../../../../docs/framework/wpf/app-development/filterinputmessage.md)
