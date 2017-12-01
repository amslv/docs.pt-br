---
title: "Comparação de objeto usando XmlNameTable"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 8d94e041-d340-4ddf-9a2c-d7319e3f4f86
caps.latest.revision: "4"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 0cd1a3bad69499b4804299adecabad3a43b5eab1
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="object-comparison-using-xmlnametable"></a><span data-ttu-id="f920e-102">Comparação de objeto usando XmlNameTable</span><span class="sxs-lookup"><span data-stu-id="f920e-102">Object Comparison Using XmlNameTable</span></span>
<span data-ttu-id="f920e-103">**XmlDocument**, quando criado, tem uma tabela de nome criada especificamente para esse documento.</span><span class="sxs-lookup"><span data-stu-id="f920e-103">**XmlDocuments**, when created, have a name table created specifically for that document.</span></span> <span data-ttu-id="f920e-104">Quando o XML é carregado no documento ou novos elementos ou atributos são criados, os nomes de atributo e elemento são colocados no **XmlNameTable**.</span><span class="sxs-lookup"><span data-stu-id="f920e-104">When XML is loaded into the document, or new elements or attributes are created, the attribute and element names are put into the **XmlNameTable**.</span></span> <span data-ttu-id="f920e-105">Você também pode criar um **XmlDocument** usando uma existente **NameTable** de outro documento.</span><span class="sxs-lookup"><span data-stu-id="f920e-105">You can also create an **XmlDocument** using an existing **NameTable** from another document.</span></span> <span data-ttu-id="f920e-106">Quando **XmlDocument** são criados com o construtor que assume um **XmlNameTable** parâmetro, o documento tem acesso aos nomes de nó, namespaces e prefixos já armazenados na  **XmlNameTable**.</span><span class="sxs-lookup"><span data-stu-id="f920e-106">When **XmlDocuments** are created with the constructor that takes an **XmlNameTable** parameter, the document has access to the node names, namespaces, and prefixes already stored in the **XmlNameTable**.</span></span> <span data-ttu-id="f920e-107">Independentemente de como a tabela de nome é carregada com nomes, uma vez que os nomes são armazenados na tabela, os nomes podem ser comparados rapidamente usando a comparação de objeto em vez de comparação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f920e-107">Regardless of how the name table is loaded with names, once the names are stored in the table, names can be compared quickly using object comparison instead of string comparison.</span></span> <span data-ttu-id="f920e-108">Cadeias de caracteres também podem ser adicionadas para a tabela de nome usando o <xref:System.Xml.NameTable.Add%2A>.</span><span class="sxs-lookup"><span data-stu-id="f920e-108">Strings can also be added to the name table using the <xref:System.Xml.NameTable.Add%2A>.</span></span> <span data-ttu-id="f920e-109">O exemplo de código a seguir mostra uma tabela de nome que está sendo criado e a cadeia de caracteres **MyString** que está sendo adicionado à tabela.</span><span class="sxs-lookup"><span data-stu-id="f920e-109">The following code sample shows a name table being created and the string **MyString** being added to the table.</span></span> <span data-ttu-id="f920e-110">Depois disso, um **XmlDocument** é criado usando essa tabela e os nomes de elemento e atributo no **Myfile.xml** são adicionadas à tabela de nome existente.</span><span class="sxs-lookup"><span data-stu-id="f920e-110">After that, an **XmlDocument** is created using that table, and the element and attribute names in **Myfile.xml** are added to the existing name table.</span></span>  
  
```vb  
Dim nt As New NameTable()  
nt.Add("MyString")  
Dim doc As New XmlDocument(nt)  
doc.Load("Myfile.xml")  
```  
  
```csharp  
NameTable nt = new NameTable();  
nt.Add("MyString");  
XmlDocument doc = new XmlDocument(nt);  
doc.Load("Myfile.xml");  
```  
  
 <span data-ttu-id="f920e-111">O exemplo de código a seguir mostra a criação de um documento, dois novos elementos que estão sendo adicionados ao documento, que também os adiciona à tabela do nome do documento, e a comparação de objeto em nomes.</span><span class="sxs-lookup"><span data-stu-id="f920e-111">The following code example shows the creation of a document, two new elements being added to the document, which also adds them to the document name table, and the object comparison on the names.</span></span>  
  
```vb  
Dim doc1 As XmlDocument = imp.CreateDocument()  
Dim node1 As XmlElement = doc.CreateElement("node1")  
Dim doc2 As XmlDocument = imp.CreateDocument()  
Dim node2 As XmlElement = doc.CreateElement("node2")  
if (CType(node1.Name, object) = CType(node2.Name, object))  
```  
  
```csharp  
XmlDocument doc1 = imp.CreateDocument();  
node1 = doc1.CreateElement ("node1");  
XmlDocument doc2 = imp.CreateDocument();  
node2 = doc2.CreateElement ("node1");  
if (((object)node1.Name) == ((object)node2.Name))  
{ ...  
```  
  
 <span data-ttu-id="f920e-112">A situação acima de uma tabela de nome transmitida entre dois documentos é típico quando o mesmo tipo de documento está sendo processado repetidamente, como documentos de ordem em um site de comércio eletrônico, que atendem a um esquema de linguagem de definição de esquema XML (XSD) ou Document type definition (DTD) e as mesmas cadeias de caracteres são repetidas.</span><span class="sxs-lookup"><span data-stu-id="f920e-112">The above scenario of a name table passed between two documents is typical when the same type of document is being processed repeatedly, such as order documents at an ecommerce site, which conform to an XML Schema definition language (XSD) schema or document type definition (DTD) and the same strings are repeated.</span></span> <span data-ttu-id="f920e-113">Usar a mesma tabela de nome fornece uma melhoria de desempenho, porque o mesmo nome de elemento ocorre em vários documentos.</span><span class="sxs-lookup"><span data-stu-id="f920e-113">Using the same name table gives a performance improvement, as the same element name occurs in multiple documents.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f920e-114">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f920e-114">See Also</span></span>  
 [<span data-ttu-id="f920e-115">XML Document Object Model (DOM)</span><span class="sxs-lookup"><span data-stu-id="f920e-115">XML Document Object Model (DOM)</span></span>](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)