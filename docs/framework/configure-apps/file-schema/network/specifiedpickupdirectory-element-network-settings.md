---
title: '&lt;specifiedPickupDirectory&gt; (configurações de rede)'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#specifiedPickupDirectory
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/specifiedPickupDirectory
helpviewer_keywords:
- specifiedPickupDirectory element
- <specifiedPickupDirectory> element
ms.assetid: 0121f49d-bff2-4bc6-af06-f1628dcd61f1
ms.openlocfilehash: d39fdf910aaec1d0a53d68fa7c6715ec344e734d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50194625"
---
# <a name="ltspecifiedpickupdirectorygt-element-network-settings"></a>&lt;specifiedPickupDirectory&gt; (configurações de rede)
Configura o diretório local para um servidor de transporte protocolo SMTP (Simple Mail).  
  
 \<configuration>  
\<system.net>  
\<mailSettings>  
\<smtp>  
\<specifiedPickupDirectory >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<specifiedPickupDirectory  
  pickupDirectoryLocation="directory"   
/>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`pickupDirectoryLocation`|O diretório em que os aplicativos salvam email para processamento posterior pelo servidor SMTP.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<SMTP > (configurações de rede)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Configura as opções de envio de mensagens de transporte protocolo SMTP (Simple Mail).|  
  
## <a name="remarks"></a>Comentários  
 O `specifiedPickupDirectory` atributo define o diretório em que os aplicativos salvam as mensagens de email a ser processada pelo servidor SMTP.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir especifica c:\maildrop como o diretório de recebimento de email.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="SpecifiedPickupDirectory">  
        <specifiedPickupDirectory  
          pickupDirectoryLocation="c:\maildrop"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também  
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>  
- <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>  
- <xref:System.Net.Configuration.SmtpSpecifiedPickupDirectoryElement?displayProperty=nameWithType>  
- [Esquema de configurações de rede](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
