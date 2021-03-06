---
title: Dos atributos1
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- attributes [.NET Framework], about
- class library design guidelines [.NET Framework], attributes
ms.assetid: ee0038ef-b247-4747-a650-3c5c5cd58d8b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 51aa91b1acbae9f1a15ac12441090dd4c1c2dcb1
ms.sourcegitcommit: 4b6490b2529707627ad77c3a43fbe64120397175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44259475"
---
# <a name="attributes"></a>Atributos
<xref:System.Attribute?displayProperty=nameWithType> uma classe base é usada para definir atributos personalizados.  
  
 Os atributos são anotações que podem ser adicionadas aos elementos de programação, como assemblies, tipos, membros e parâmetros. Eles são armazenados nos metadados do assembly e podem ser acessados no tempo de execução usando as APIs de reflexão. Por exemplo, o Framework define o <xref:System.ObsoleteAttribute>, que pode ser aplicada a um tipo ou membro para indicar que o tipo ou membro foi preterido.  
  
 Atributos podem ter uma ou mais propriedades que contêm dados adicionais relacionados ao atributo. Por exemplo, `ObsoleteAttribute` poderia conter informações adicionais sobre a versão em que um tipo ou membro foi preterido e a descrição das novas APIs, substituindo a API obsoleta.  
  
 Algumas propriedades de um atributo devem ser especificadas quando o atributo é aplicado. Eles são chamados das propriedades necessárias ou os argumentos necessários, porque eles são representados como parâmetros posicionais de construtor. Por exemplo, o <xref:System.Diagnostics.ConditionalAttribute.ConditionString%2A> propriedade do <xref:System.Diagnostics.ConditionalAttribute> é uma propriedade necessária.  
  
 As propriedades que não necessariamente precisam ser especificado quando o atributo é aplicado são chamadas propriedades opcionais (ou argumentos opcionais). Eles são representados por propriedades configuráveis. Compiladores fornecem uma sintaxe especial para definir essas propriedades quando um atributo é aplicado. Por exemplo, o <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> propriedade representa um argumento opcional.  
  
 **✓ DO** nome classes de atributos personalizados com o sufixo "Atributo".  
  
 **✓ DO** se aplicam a <xref:System.AttributeUsageAttribute> para os atributos personalizados.  
  
 **✓ DO** fornecem propriedades configuráveis para argumentos opcionais.  
  
 **✓ DO** fornecem propriedades somente obtenção para os argumentos necessários.  
  
 **✓ DO** fornecer parâmetros de construtor para inicializar propriedades correspondentes para os argumentos necessários. Cada parâmetro deve ter o mesmo nome (embora com maiusculas e minúsculas diferentes) como a propriedade correspondente.  
  
 **X AVOID** fornecendo os parâmetros do construtor para inicializar propriedades correspondentes para os argumentos opcionais.  
  
 Em outras palavras, não têm propriedades que podem ser definidas com um construtor e um setter. Essa diretriz torna bastante explícito quais argumentos são opcionais e que são necessário e evita a necessidade de duas maneiras de fazer a mesma coisa.  
  
 **X AVOID** sobrecarga construtores de atributo personalizado.  
  
 Ter apenas um construtor claramente comunica-se para o usuário quais argumentos são necessários e opcionais.  
  
 **✓ DO** lacrar classes de atributo personalizado, se possível. Isso torna a pesquisa para o atributo mais rápida.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*  
  
 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*  
  
## <a name="see-also"></a>Consulte também

- [Diretrizes de design do Framework](../../../docs/standard/design-guidelines/index.md)  
- [Diretrizes de uso](../../../docs/standard/design-guidelines/usage-guidelines.md)
