---
title: volatile (Referência de C#)
ms.date: 07/20/2015
f1_keywords:
- volatile_CSharpKeyword
- volatile
helpviewer_keywords:
- volatile keyword [C#]
ms.assetid: 78089bc7-7b38-4cfd-9e49-87ac036af009
ms.openlocfilehash: be7e081b18702710c00b5b86a9bc152800f0cf3d
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43526213"
---
# <a name="volatile-c-reference"></a>volatile (Referência de C#)
A palavra-chave `volatile` indica que um campo pode ser modificado por vários threads que estão em execução ao mesmo tempo. Os campos que são declarados `volatile` não estão sujeitos a otimizações do compilador que assumem o acesso por um único thread. Essas restrições garantem que todos os threads observem as gravações voláteis executadas por qualquer outro thread na ordem em que elas foram realizadas. Não há nenhuma garantia de uma única ordenação total de gravações voláteis como visto em todos os threads de execução.  
  
 O modificador `volatile` geralmente é usado para um campo que é acessado por vários threads sem usar a instrução [block](../../../csharp/language-reference/keywords/lock-statement.md) para serializar o acesso.  
  
 A palavra-chave `volatile` pode ser aplicada a campos desses tipos:  
  
-   Tipos de referência.  
  
-   Tipos de ponteiro (em um contexto sem segurança). Observe que embora o ponteiro em si possa ser volátil, o objeto para o qual ele aponta não pode. Em outras palavras, você não pode declarar um "ponteiro como volátil".  
  
-   Tipos como sbyte, byte, short, ushort, int, uint, char, float e bool.  
  
-   Um tipo de enumeração com um dos seguintes tipos de base: byte, sbyte, short, ushort, int ou uint.  
  
-   Parâmetros de tipo genérico conhecidos por serem tipos de referência.  
  
-   <xref:System.IntPtr> e <xref:System.UIntPtr>.  
  
 A palavra-chave volatile pode ser aplicada apenas a campos de uma classe ou struct. As variáveis locais não podem ser declaradas como `volatile`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como declarar uma variável de campo público como `volatile`.  
  
 [!code-csharp[csrefKeywordsModifiers#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_1.cs)]  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir demonstra como um thread de trabalho ou auxiliar pode ser criado e usado para executar o processamento em paralelo com o do thread primário. Para obter informações detalhadas sobre multithreading, confira [Threading gerenciado](../../../standard/threading/index.md) e [Threading (C#)](../../programming-guide/concepts/threading/index.md).  
  
 [!code-csharp[csProgGuideThreading#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/volatile_2.cs)]  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de C#](../../../csharp/language-reference/index.md)  
- [Guia de Programação em C#](../../../csharp/programming-guide/index.md)  
- [Palavras-chave do C#](../../../csharp/language-reference/keywords/index.md)  
- [Modificadores](../../../csharp/language-reference/keywords/modifiers.md)
