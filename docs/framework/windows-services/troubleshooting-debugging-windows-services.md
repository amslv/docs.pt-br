---
title: 'Solucionando problemas: depurando Serviços Windows'
ms.date: 03/30/2017
helpviewer_keywords:
- debugging Windows Service applications
- debugging [Visual Studio], Windows services
- troubleshooting service applications
- services, troubleshooting
- troubleshooting debugging, Windows Services
- Windows Service applications, debugging
- services, debugging
- Windows Service applications, troubleshooting
ms.assetid: cf859d4c-f04c-4cb7-81e3-bc7de8bea190
author: ghogen
ms.openlocfilehash: 0dbbebd14ce0ff5f69a12c256238c7e0a02494cb
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2018
ms.locfileid: "47199938"
---
# <a name="troubleshooting-debugging-windows-services"></a>Solucionando problemas: depurando Serviços Windows
Quando você depurar um aplicativo de serviço Windows, o serviço e o **Windows Service Manager** interagirão. O **Service Manager** inicia o serviço chamando o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e, em seguida, espera 30 segundos para que o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> retorne. Se o método não retornar nesse período, o gerenciador mostra um erro indicando que o serviço não pode ser iniciado.  
  
 Ao depurar o método <xref:System.ServiceProcess.ServiceBase.OnStart%2A>, conforme é descrito em [Como depurar aplicativos de Serviço Windows](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md), você precisará estar ciente desse período de 30 segundos. Se você colocar um ponto de interrupção no método <xref:System.ServiceProcess.ServiceBase.OnStart%2A> e não entrar nele em até 30 segundos, o gerente não iniciará o serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Como depurar aplicativos de Serviço Windows](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)  
 [Introdução aos Aplicativos de Serviço Windows](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)
