
Entretanto, ao chamar o método **String.Format**, não é necessário se concentrar na sobrecarga específica que você deseja chamar. Em vez disso, é possível chamar o método com uma [cadeia de caracteres de formato composto](~/docs/standard/base-types/composite-formatting.md) que inclui um ou mais itens de formato. Você atribui a cada item de formato um índice numérico. O primeiro índice começa em 0. Além da cadeia de caracteres inicial, sua chamada de método deve ter tantos argumentos adicionais quantos valores de índice. Por exemplo, uma cadeia de caracteres cujos itens de formato têm índices 0 e 1 deve ter 2 argumentos; uma com índices de 0 a 5 deve ter 6 argumentos. O compilador de linguagem, então, resolverá a chamada de método para uma sobrecarga específica do método **String.Format**.   
 
Para obter uma documentação mais detalhada sobre como usar o método **String.Format**, consulte o [Guia de Introdução ao método String.Format](#Starting) e [Qual método chamar?](#FTaskList).    