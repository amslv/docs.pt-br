---
title: "Exemplo de soquete de cliente síncrono"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- sockets, code examples
- synchronous client sockets
- sockets, synchronous client sockets
ms.assetid: 2c7d5be7-2221-467c-a839-5744ec4d576d
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 759585d1029742f6f45e9f7253282af05accc82e
ms.contentlocale: pt-br
ms.lasthandoff: 08/21/2017

---
# <a name="synchronous-client-socket-example"></a><span data-ttu-id="f2861-102">Exemplo de soquete de cliente síncrono</span><span class="sxs-lookup"><span data-stu-id="f2861-102">Synchronous Client Socket Example</span></span>
<span data-ttu-id="f2861-103">O programa de exemplo a seguir cria um cliente que se conecta a um servidor.</span><span class="sxs-lookup"><span data-stu-id="f2861-103">The following example program creates a client that connects to a server.</span></span> <span data-ttu-id="f2861-104">O cliente é criado com um soquete síncrono e, portanto, a execução do aplicativo cliente é suspensa até que o servidor retorne uma resposta.</span><span class="sxs-lookup"><span data-stu-id="f2861-104">The client is built with a synchronous socket, so execution of the client application is suspended until the server returns a response.</span></span> <span data-ttu-id="f2861-105">O aplicativo envia uma cadeia de caracteres ao servidor e, em seguida, exibe a cadeia de caracteres retornada pelo servidor no console.</span><span class="sxs-lookup"><span data-stu-id="f2861-105">The application sends a string to the server and then displays the string returned by the server on the console.</span></span>  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class SynchronousSocketClient  
  
    Public Shared Sub Main()  
        ' Data buffer for incoming data.  
        Dim bytes(1024) As Byte  
  
        ' Connect to a remote device.  
  
        ' Establish the remote endpoint for the socket.  
        ' This example uses port 11000 on the local computer.  
        Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
        Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
        Dim remoteEP As New IPEndPoint(ipAddress, 11000)  
  
        ' Create a TCP/IP socket.  
        Dim sender As New Socket(AddressFamily.InterNetwork, _  
            SocketType.Stream, ProtocolType.Tcp)  
  
        ' Connect the socket to the remote endpoint.  
        sender.Connect(remoteEP)  
  
        Console.WriteLine("Socket connected to {0}", _  
            sender.RemoteEndPoint.ToString())  
  
        ' Encode the data string into a byte array.  
        Dim msg As Byte() = _  
            Encoding.ASCII.GetBytes("This is a test<EOF>")  
  
        ' Send the data through the socket.  
        Dim bytesSent As Integer = sender.Send(msg)  
  
        ' Receive the response from the remote device.  
        Dim bytesRec As Integer = sender.Receive(bytes)  
        Console.WriteLine("Echoed test = {0}", _  
            Encoding.ASCII.GetString(bytes, 0, bytesRec))  
  
        ' Release the socket.  
        sender.Shutdown(SocketShutdown.Both)  
        sender.Close()  
    End Sub  
  
End Class 'SynchronousSocketClient  
```  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Sockets;  
using System.Text;  
  
public class SynchronousSocketClient {  
  
    public static void StartClient() {  
        // Data buffer for incoming data.  
        byte[] bytes = new byte[1024];  
  
        // Connect to a remote device.  
        try {  
            // Establish the remote endpoint for the socket.  
            // This example uses port 11000 on the local computer.  
            IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
            IPAddress ipAddress = ipHostInfo.AddressList[0];  
            IPEndPoint remoteEP = new IPEndPoint(ipAddress,11000);  
  
            // Create a TCP/IP  socket.  
            Socket sender = new Socket(AddressFamily.InterNetwork,   
                SocketType.Stream, ProtocolType.Tcp );  
  
            // Connect the socket to the remote endpoint. Catch any errors.  
            try {  
                sender.Connect(remoteEP);  
  
                Console.WriteLine("Socket connected to {0}",  
                    sender.RemoteEndPoint.ToString());  
  
                // Encode the data string into a byte array.  
                byte[] msg = Encoding.ASCII.GetBytes("This is a test<EOF>");  
  
                // Send the data through the socket.  
                int bytesSent = sender.Send(msg);  
  
                // Receive the response from the remote device.  
                int bytesRec = sender.Receive(bytes);  
                Console.WriteLine("Echoed test = {0}",  
                    Encoding.ASCII.GetString(bytes,0,bytesRec));  
  
                // Release the socket.  
                sender.Shutdown(SocketShutdown.Both);  
                sender.Close();  
  
            } catch (ArgumentNullException ane) {  
                Console.WriteLine("ArgumentNullException : {0}",ane.ToString());  
            } catch (SocketException se) {  
                Console.WriteLine("SocketException : {0}",se.ToString());  
            } catch (Exception e) {  
                Console.WriteLine("Unexpected exception : {0}", e.ToString());  
            }  
  
        } catch (Exception e) {  
            Console.WriteLine( e.ToString());  
        }  
    }  
  
    public static int Main(String[] args) {  
        StartClient();  
        return 0;  
    }  
}  
```  
  
## <a name="see-also"></a><span data-ttu-id="f2861-106">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f2861-106">See Also</span></span>  
 <span data-ttu-id="f2861-107">[Exemplo de soquete de servidor síncrono](../../../docs/framework/network-programming/synchronous-server-socket-example.md) </span><span class="sxs-lookup"><span data-stu-id="f2861-107">[Synchronous Server Socket Example](../../../docs/framework/network-programming/synchronous-server-socket-example.md) </span></span>  
 <span data-ttu-id="f2861-108">[Usando um soquete de cliente síncrono](../../../docs/framework/network-programming/using-a-synchronous-client-socket.md) </span><span class="sxs-lookup"><span data-stu-id="f2861-108">[Using a Synchronous Client Socket](../../../docs/framework/network-programming/using-a-synchronous-client-socket.md) </span></span>  
 [<span data-ttu-id="f2861-109">Exemplos de código de soquete</span><span class="sxs-lookup"><span data-stu-id="f2861-109">Socket Code Examples</span></span>](../../../docs/framework/network-programming/socket-code-examples.md)
