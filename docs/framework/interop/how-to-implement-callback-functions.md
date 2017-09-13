---
title: "Como implementar funções de retorno de chamada"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- callback function, implementing
ms.assetid: e55b3712-b9ea-4453-bd9a-ad5cfa2f6bfa
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d4382c956bf3d56426be485897cdda75453b4910
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-implement-callback-functions"></a><span data-ttu-id="1dee4-102">Como implementar funções de retorno de chamada</span><span class="sxs-lookup"><span data-stu-id="1dee4-102">How to: Implement Callback Functions</span></span>
<span data-ttu-id="1dee4-103">O procedimento e o exemplo a seguir demonstram como um aplicativo gerenciado, usando invocação de plataforma, pode imprimir o valor do identificador para cada janela no computador local.</span><span class="sxs-lookup"><span data-stu-id="1dee4-103">The following procedure and example demonstrate how a managed application, using platform invoke, can print the handle value for each window on the local computer.</span></span> <span data-ttu-id="1dee4-104">Especificamente, o procedimento e o exemplo usam a função **EnumWindows** para percorrer a lista de janelas e uma função de retorno de chamada gerenciada (chamada CallBack) para imprimir o valor do identificador da janela.</span><span class="sxs-lookup"><span data-stu-id="1dee4-104">Specifically, the procedure and example use the **EnumWindows** function to step through the list of windows and a managed callback function (named CallBack) to print the value of the window handle.</span></span>  
  
### <a name="to-implement-a-callback-function"></a><span data-ttu-id="1dee4-105">Para implementar uma função de retorno de chamada</span><span class="sxs-lookup"><span data-stu-id="1dee4-105">To implement a callback function</span></span>  
  
1.  <span data-ttu-id="1dee4-106">Examine a assinatura para a função **EnumWindows** antes de continuar com a implementação.</span><span class="sxs-lookup"><span data-stu-id="1dee4-106">Look at the signature for the **EnumWindows** function before going further with the implementation.</span></span> <span data-ttu-id="1dee4-107">**EnumWindows** tem a seguinte assinatura:</span><span class="sxs-lookup"><span data-stu-id="1dee4-107">**EnumWindows** has the following signature:</span></span>  
  
    ```  
    BOOL EnumWindows(WNDENUMPROC lpEnumFunc, LPARAM lParam)  
    ```  
  
     <span data-ttu-id="1dee4-108">Uma indicação de que essa função requer um retorno de chamada é a presença do argumento **lpEnumFunc**.</span><span class="sxs-lookup"><span data-stu-id="1dee4-108">One clue that this function requires a callback is the presence of the **lpEnumFunc** argument.</span></span> <span data-ttu-id="1dee4-109">É comum ver o prefixo **lp** (ponteiro longo) combinado com o sufixo **Func** no nome de argumentos que levam um ponteiro para uma função de retorno de chamada.</span><span class="sxs-lookup"><span data-stu-id="1dee4-109">It is common to see the **lp** (long pointer) prefix combined with the **Func** suffix in the name of arguments that take a pointer to a callback function.</span></span> <span data-ttu-id="1dee4-110">Para obter a documentação sobre funções do Win32, consulte o SDK da Plataforma Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1dee4-110">For documentation about Win32 functions, see the Microsoft Platform SDK.</span></span>  
  
2.  <span data-ttu-id="1dee4-111">Crie a função de retorno de chamada gerenciada.</span><span class="sxs-lookup"><span data-stu-id="1dee4-111">Create the managed callback function.</span></span> <span data-ttu-id="1dee4-112">O exemplo declara um tipo de delegado chamado `CallBack` que leva dois argumentos (**hwnd** e **lparam**).</span><span class="sxs-lookup"><span data-stu-id="1dee4-112">The example declares a delegate type, called `CallBack`, which takes two arguments (**hwnd** and **lparam**).</span></span> <span data-ttu-id="1dee4-113">O primeiro argumento é um identificador para a janela, enquanto o segundo argumento é definido pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1dee4-113">The first argument is a handle to the window; the second argument is application-defined.</span></span> <span data-ttu-id="1dee4-114">Nesta versão, ambos os argumentos devem ser números inteiros.</span><span class="sxs-lookup"><span data-stu-id="1dee4-114">In this release, both arguments must be integers.</span></span>  
  
     <span data-ttu-id="1dee4-115">Funções de retorno de chamada normalmente retornam valores diferentes de zero para indicar êxito e zero para indicar falha.</span><span class="sxs-lookup"><span data-stu-id="1dee4-115">Callback functions generally return nonzero values to indicate success and zero to indicate failure.</span></span> <span data-ttu-id="1dee4-116">Este exemplo define explicitamente o valor retornado para **true** para continuar a enumeração.</span><span class="sxs-lookup"><span data-stu-id="1dee4-116">This example explicitly sets the return value to **true** to continue the enumeration.</span></span>  
  
3.  <span data-ttu-id="1dee4-117">Crie um delegado e passe-o como um argumento para a função **EnumWindows**.</span><span class="sxs-lookup"><span data-stu-id="1dee4-117">Create a delegate and pass it as an argument to the **EnumWindows** function.</span></span> <span data-ttu-id="1dee4-118">A invocação de plataforma converte o delegado em um formato de retorno de chamada familiar automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1dee4-118">Platform invoke converts the delegate to a familiar callback format automatically.</span></span>  
  
4.  <span data-ttu-id="1dee4-119">Verifique se o coletor de lixo não recupera o delegado antes da função de retorno de chamada terminar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="1dee4-119">Ensure that the garbage collector does not reclaim the delegate before the callback function completes its work.</span></span> <span data-ttu-id="1dee4-120">Quando você passa um delegado como um parâmetro ou passa um delegado contido como um campo em uma estrutura, ele permanece não coletado pela a duração da chamada.</span><span class="sxs-lookup"><span data-stu-id="1dee4-120">When you pass a delegate as a parameter, or pass a delegate contained as a field in a structure, it remains uncollected for the duration of the call.</span></span> <span data-ttu-id="1dee4-121">Portanto, como é o caso no exemplo de enumeração a seguir, a função de retorno de chamada termina o trabalho antes da chamada retornar e não requer nenhuma ação adicional pelo chamador gerenciado.</span><span class="sxs-lookup"><span data-stu-id="1dee4-121">So, as is the case in the following enumeration example, the callback function completes its work before the call returns and requires no additional action by the managed caller.</span></span>  
  
     <span data-ttu-id="1dee4-122">Se, no entanto, a função de retorno de chamada puder ser chamada depois que a chamada retornar, o chamador gerenciado deverá tomar medidas para garantir que o delegado permaneça não coletado até que a função de retorno de chamada seja concluída.</span><span class="sxs-lookup"><span data-stu-id="1dee4-122">If, however, the callback function can be invoked after the call returns, the managed caller must take steps to ensure that the delegate remains uncollected until the callback function finishes.</span></span> <span data-ttu-id="1dee4-123">Para obter informações detalhadas sobre como evitar a coleta de lixo, consulte [Marshaling de interoperabilidade](../../../docs/framework/interop/interop-marshaling.md) com invocação de plataforma.</span><span class="sxs-lookup"><span data-stu-id="1dee4-123">For detailed information about preventing garbage collection, see [Interop Marshaling](../../../docs/framework/interop/interop-marshaling.md) with Platform Invoke.</span></span>  
  
## <a name="example"></a><span data-ttu-id="1dee4-124">Exemplo</span><span class="sxs-lookup"><span data-stu-id="1dee4-124">Example</span></span>  
  
```vb  
Imports System  
Imports System.Runtime.InteropServices  
  
Public Delegate Function CallBack( _  
hwnd As Integer, lParam As Integer) As Boolean  
  
Public Class EnumReportApp  
  
    Declare Function EnumWindows Lib "user32" ( _  
       x As CallBack, y As Integer) As Integer  
  
    Public Shared Sub Main()  
        EnumWindows(AddressOf EnumReportApp.Report, 0)  
    End Sub 'Main  
  
    Public Shared Function Report(hwnd As Integer, lParam As Integer) _  
    As Boolean  
        Console.Write("Window handle is ")  
        Console.WriteLine(hwnd)  
        Return True  
    End Function 'Report  
End Class 'EnumReportApp  
```  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
  
public delegate bool CallBack(int hwnd, int lParam);  
  
public class EnumReportApp  
{  
    [DllImport("user32")]  
    public static extern int EnumWindows(CallBack x, int y);   
  
    public static void Main()   
    {  
        CallBack myCallBack = new CallBack(EnumReportApp.Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    public static bool Report(int hwnd, int lParam)  
    {   
        Console.Write("Window handle is ");  
        Console.WriteLine(hwnd);  
        return true;  
    }  
}  
```  
  
```cpp  
using namespace System;  
using namespace System::Runtime::InteropServices;  
  
// A delegate type.  
delegate bool CallBack(int hwnd, int lParam);  
  
// Managed type with the method to call.  
ref class EnumReport  
{  
// Report the window handle.  
public:  
    [DllImport("user32")]  
    static int EnumWindows(CallBack^ x, int y);  
  
    static void Main()  
    {  
        EnumReport^ er = gcnew EnumReport;  
        CallBack^ myCallBack = gcnew CallBack(&EnumReport::Report);  
        EnumWindows(myCallBack, 0);  
    }  
  
    static bool Report(int hwnd, int lParam)  
    {  
       Console::Write(L"Window handle is ");  
       Console::WriteLine(hwnd);  
       return true;  
    }  
};  
  
int main()  
{  
    EnumReport::Main();  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="1dee4-125">Consulte também</span><span class="sxs-lookup"><span data-stu-id="1dee4-125">See Also</span></span>  
 <span data-ttu-id="1dee4-126">[Funções de retorno de chamada](../../../docs/framework/interop/callback-functions.md) </span><span class="sxs-lookup"><span data-stu-id="1dee4-126">[Callback Functions](../../../docs/framework/interop/callback-functions.md) </span></span>  
 [<span data-ttu-id="1dee4-127">Chamando uma função de DLL</span><span class="sxs-lookup"><span data-stu-id="1dee4-127">Calling a DLL Function</span></span>](../../../docs/framework/interop/calling-a-dll-function.md)
