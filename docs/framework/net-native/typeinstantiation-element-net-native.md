---
title: Elemento &lt;TypeInstantiation&gt; (.NET Nativo)
ms.date: 03/30/2017
ms.assetid: a5eada64-075b-4162-9655-ded84e4681f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5277b056c11de4c3e32d33c72bafc8f64ee17d05
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50033858"
---
# <a name="lttypeinstantiationgt-element-net-native"></a>Elemento &lt;TypeInstantiation&gt; (.NET Nativo)
Aplica a política de reflexão de tempo de execução a um tipo genérico construído.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<TypeInstantiation Name="type_name"  
                   Arguments="type_arguments"  
                   Activate="policy_type"  
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
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Tipo de atributo|Descrição|  
|---------------|--------------------|-----------------|  
|`Name`|Geral|Atributo obrigatório. Especifica o nome do tipo.|  
|`Arguments`|Geral|Atributo obrigatório. Especifica os argumentos de tipo genérico. Se houver vários parâmetros, eles são separados por vírgulas.|  
|`Activate`|Reflexão|Atributo opcional. Controla o acesso de tempo de execução a construtores para habilitar a ativação de instâncias.|  
|`Browse`|Reflexão|Atributo opcional. Controla a consulta para obter informações sobre elementos do programa, mas não permite qualquer acesso de tempo de execução.|  
|`Dynamic`|Reflexão|Atributo opcional. Controla o acesso a todos os tipos de membro ao tempo de execução, incluindo construtores, métodos, campos, propriedades e eventos, habilitando a programação dinâmica.|  
|`Serialize`|Serialização|Atributo opcional. Controla o acesso ao tempo de execução para construtores, campos e propriedades para habilitar a serialização e desserialização das instâncias por bibliotecas como o serializador Newtonsoft JSON.|  
|`DataContractSerializer`|Serialização|Atributo opcional. Controla a política de serialização que usa a classe <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType>.|  
|`DataContractJsonSerializer`|Serialização|Atributo opcional. Controla a política de serialização JSON que usa a classe <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=nameWithType>.|  
|`XmlSerializer`|Serialização|Atributo opcional. Controla a política de serialização XML que usa a classe <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>.|  
|`MarshalObject`|Interoperabilidade|Atributo opcional. Política de controles de marshaling de tipos de referência para o Tempo de Execução do Windows e COM.|  
|`MarshalDelegate`|Interoperabilidade|Atributo opcional. Controla a diretiva de marshaling de tipos delegados como ponteiros de função para código nativo.|  
|`MarshalStructure`|Interoperabilidade|Atributo opcional. Controla a política de estruturas de marshaling para código nativo.|  
  
## <a name="name-attribute"></a>Atributo de nome  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*type_name*|O nome do tipo. Se este elemento `<TypeInstantiation>` for o filho de um elemento [\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md), de um elemento [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) ou de outro elemento `<TypeInstantiation>`, o *type_name* poderá incluir o nome do tipo sem seu namespace. Caso contrário, o *type_name* deverá incluir o nome do tipo totalmente qualificado. O nome do tipo não decorado. Por exemplo, para um objeto <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>, o elemento `<TypeInstantiation>` poderá aparecer da seguinte maneira:<br /><br /> `\<TypeInstantiation Name=System.Collections.Generic.List Dynamic="Required Public" />`|  
  
## <a name="arguments-attribute"></a>Atributo de argumentos  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*type_argument*|Especifica os argumentos de tipo genérico. Se houver vários parâmetros, eles são separados por vírgulas. Cada argumento deve conter o nome do tipo totalmente qualificado.|  
  
## <a name="all-other-attributes"></a>Todos os outros atributos  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*policy_setting*|A configuração a ser aplicada a este tipo de política para o tipo genérico construído. Os valores possíveis são `All`, `Auto`, `Excluded`, `Public`, `PublicAndInternal`, `Required Public`, `Required PublicAndInternal` e `Required All`. Para obter mais informações, consulte [Configurações da política da diretiva de tempo de execução](../../../docs/framework/net-native/runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<Event>](../../../docs/framework/net-native/event-element-net-native.md)|Aplica a política de reflexão a um evento pertencente a esse tipo.|  
|[\<Field>](../../../docs/framework/net-native/field-element-net-native.md)|Aplica a política de reflexão a um campo pertencente a esse tipo.|  
|[\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)|Aplica a política a um tipo, se esta política tiver sido aplicada ao tipo representado pelo elemento `<TypeInstantiation>` recipiente.|  
|[\<Method>](../../../docs/framework/net-native/method-element-net-native.md)|Aplica a política de reflexão a um método pertencente a esse tipo.|  
|[\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)|Aplica a política de reflexão a um método construído genérico pertencente a esse tipo.|  
|[\<Property>](../../../docs/framework/net-native/property-element-net-native.md)|Aplica a política de reflexão a uma propriedade pertencente a esse tipo.|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|Aplica a política de reflexão a um tipo aninhado.|  
|`<TypeInstantiation>`|Aplica a política de reflexão a um tipo genérico construído aninhado.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|Serve como um contêiner para os tipos amplos de aplicativos cujos metadados estão disponíveis para reflexão no tempo de execução.|  
|[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|Aplica a política de reflexão para todos os tipos em um assembly especificado.|  
|[\<Library>](../../../docs/framework/net-native/library-element-net-native.md)|Define o assembly que contém tipos e membros de tipo cujos metadados estão disponíveis para reflexão em tempo de execução.|  
|[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|Aplica a política de reflexão a todos os tipos em um namespace.|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|Aplica a política de reflexão a um tipo e todos os seus membros.|  
|`<TypeInstantiation>`|Aplica a política de reflexão a um tipo genérico construído e todos os seus membros.|  
  
## <a name="remarks"></a>Comentários  
 Os atributos de reflexão, serialização e interoperabilidade são todos opcionais. No entanto, pelo menos um deve estar presente.  
  
 Se um elemento `<TypeInstantiation>` for o filho de um elemento [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md), [\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md) ou [\<Type>](../../../docs/framework/net-native/type-element-net-native.md), ele substituirá as configurações de política definidas pelo elemento pai. Se um elemento [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) definir uma definição de tipo genérico correspondente, o elemento `<TypeInstantiation>` substituirá a política de reflexão em tempo de execução somente para instanciações do tipo genérico construído especificado.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa uma reflexão para recuperar a definição de tipo genérico de um objeto <xref:System.Collections.Generic.Dictionary%602> construído. Ele também usa reflexão para exibir informações sobre objetos <xref:System.Type> que representam tipos genéricos construídos e definições de tipo genérico. A variável `b` no exemplo é um <xref:Windows.UI.Xaml.Controls.TextBlock> controle.  
  
 [!code-csharp[ProjectN_Reflection#2](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/makegenerictype1.cs#2)]  
  
 Após a compilação com a cadeia de ferramentas [!INCLUDE[net_native](../../../includes/net-native-md.md)], o exemplo gera uma exceção [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) na linha que chama o método <xref:System.Type.GetGenericTypeDefinition%2A?displayProperty=nameWithType>. Para eliminar a exceção e fornecer os metadados necessários, adicione o seguinte elemento `<TypeInstantiation>` ao arquivo de diretivas de tempo de execução:  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
     <TypeInstantiation Name="System.Collections.Generic.Dictionary"  
                        Arguments="System.String,GenericType.Example"  
                        Dynamic="Required Public" />  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de configuração das diretivas de tempo de execução (rd.xml)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)  
 [Elementos da diretiva de tempo de execução](../../../docs/framework/net-native/runtime-directive-elements.md)  
 [Configurações da política da diretiva de tempo de execução](../../../docs/framework/net-native/runtime-directive-policy-settings.md)
