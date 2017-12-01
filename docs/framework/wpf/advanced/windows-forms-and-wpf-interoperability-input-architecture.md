---
title: Windows Forms e arquitetura de entrada da interoperabilidade do WPF
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input architecture [WPF interoperability]
- messages [WPF]
- Windows Forms [WPF], interoperability with
- Windows Forms [WPF], WPF interoperation
- interoperability [WPF], Windows Forms
- modeless forms [WPF]
- ElementHost keyboard and messages [WPF]
- keyboard interoperation [WPF]
- WindowsFormsHost keyboard and messages [WPF]
- modeless dialog boxes [WPF]
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
caps.latest.revision: "20"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.openlocfilehash: b48b5d78ce3136146f7ad17f859a489b5556a000
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="windows-forms-and-wpf-interoperability-input-architecture"></a><span data-ttu-id="a97dd-102">Windows Forms e arquitetura de entrada da interoperabilidade do WPF</span><span class="sxs-lookup"><span data-stu-id="a97dd-102">Windows Forms and WPF Interoperability Input Architecture</span></span>
<span data-ttu-id="a97dd-103">A interoperação entre o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] e o [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] requer que as duas tecnologias tenham o processamento de entrada de teclado apropriado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-103">Interoperation between the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] and [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] requires that both technologies have the appropriate keyboard input processing.</span></span> <span data-ttu-id="a97dd-104">Este tópico descreve como essas tecnologias implementam o processamento de mensagens e teclado para permitir uma interoperação suave em aplicativos híbridos.</span><span class="sxs-lookup"><span data-stu-id="a97dd-104">This topic describes how these technologies implement keyboard and message processing to enable smooth interoperation in hybrid applications.</span></span>  
  
 <span data-ttu-id="a97dd-105">Este tópico contém as seguintes subseções:</span><span class="sxs-lookup"><span data-stu-id="a97dd-105">This topic contains the following subsections:</span></span>  
  
-   <span data-ttu-id="a97dd-106">Formulários sem janela restrita e caixas de diálogo</span><span class="sxs-lookup"><span data-stu-id="a97dd-106">Modeless Forms and Dialog Boxes</span></span>  
  
-   <span data-ttu-id="a97dd-107">Processamento de mensagens e teclado de WindowsFormsHost</span><span class="sxs-lookup"><span data-stu-id="a97dd-107">WindowsFormsHost Keyboard and Message Processing</span></span>  
  
-   <span data-ttu-id="a97dd-108">Processamento de mensagens e teclado de ElementHost</span><span class="sxs-lookup"><span data-stu-id="a97dd-108">ElementHost Keyboard and Message Processing</span></span>  
  
## <a name="modeless-forms-and-dialog-boxes"></a><span data-ttu-id="a97dd-109">Formulários sem janela restrita e caixas de diálogo</span><span class="sxs-lookup"><span data-stu-id="a97dd-109">Modeless Forms and Dialog Boxes</span></span>  
 <span data-ttu-id="a97dd-110">Chamar o <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> método no <xref:System.Windows.Forms.Integration.WindowsFormsHost> elemento para abrir uma caixa de diálogo ou formulário sem janela restrita de um [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-aplicativo com base em.</span><span class="sxs-lookup"><span data-stu-id="a97dd-110">Call the <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> method on the <xref:System.Windows.Forms.Integration.WindowsFormsHost> element to open a modeless form or dialog box from a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-based application.</span></span>  
  
 <span data-ttu-id="a97dd-111">Chamar o <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> método no <xref:System.Windows.Forms.Integration.ElementHost> controle para abrir uma sem janela restrita [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] página em um [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-aplicativo baseado em.</span><span class="sxs-lookup"><span data-stu-id="a97dd-111">Call the <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> method on the <xref:System.Windows.Forms.Integration.ElementHost> control to open a modeless [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] page in a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]-based application.</span></span>  
  
## <a name="windowsformshost-keyboard-and-message-processing"></a><span data-ttu-id="a97dd-112">Processamento de mensagens e teclado de WindowsFormsHost</span><span class="sxs-lookup"><span data-stu-id="a97dd-112">WindowsFormsHost Keyboard and Message Processing</span></span>  
 <span data-ttu-id="a97dd-113">Quando hospedado por um aplicativo baseado em [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], o processamento de mensagens e teclado [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] consiste no seguinte:</span><span class="sxs-lookup"><span data-stu-id="a97dd-113">When hosted by a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]-based application, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] keyboard and message processing consists of the following:</span></span>  
  
-   <span data-ttu-id="a97dd-114">O <xref:System.Windows.Forms.Integration.WindowsFormsHost> classe adquire mensagens do [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] loop de mensagem, que é implementado pelo <xref:System.Windows.Interop.ComponentDispatcher> classe.</span><span class="sxs-lookup"><span data-stu-id="a97dd-114">The <xref:System.Windows.Forms.Integration.WindowsFormsHost> class acquires messages from the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] message loop, which is implemented by the <xref:System.Windows.Interop.ComponentDispatcher> class.</span></span>  
  
-   <span data-ttu-id="a97dd-115">O <xref:System.Windows.Forms.Integration.WindowsFormsHost> classe cria um substituto [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] loop de mensagem para garantir que comum [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ocorre o processamento do teclado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-115">The <xref:System.Windows.Forms.Integration.WindowsFormsHost> class creates a surrogate [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] message loop to ensure that ordinary [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] keyboard processing occurs.</span></span>  
  
-   <span data-ttu-id="a97dd-116">O <xref:System.Windows.Forms.Integration.WindowsFormsHost> classe implementa o <xref:System.Windows.Interop.IKeyboardInputSink> interface para coordenar o gerenciamento de foco com [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span><span class="sxs-lookup"><span data-stu-id="a97dd-116">The <xref:System.Windows.Forms.Integration.WindowsFormsHost> class implements the <xref:System.Windows.Interop.IKeyboardInputSink> interface to coordinate focus management with [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span></span>  
  
-   <span data-ttu-id="a97dd-117">O <xref:System.Windows.Forms.Integration.WindowsFormsHost> controles se registrar e iniciar seus loops de mensagens.</span><span class="sxs-lookup"><span data-stu-id="a97dd-117">The <xref:System.Windows.Forms.Integration.WindowsFormsHost> controls register themselves and start their message loops.</span></span>  
  
 <span data-ttu-id="a97dd-118">As seções a seguir descrevem essas etapas do processo em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a97dd-118">The following sections describe these parts of the process in more detail.</span></span>  
  
### <a name="acquiring-messages-from-the-wpf-message-loop"></a><span data-ttu-id="a97dd-119">Adquirindo mensagens do loop de mensagens do WPF</span><span class="sxs-lookup"><span data-stu-id="a97dd-119">Acquiring Messages from the WPF Message Loop</span></span>  
 <span data-ttu-id="a97dd-120">O <xref:System.Windows.Interop.ComponentDispatcher> classe implementa o Gerenciador de loop de mensagem para [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span><span class="sxs-lookup"><span data-stu-id="a97dd-120">The <xref:System.Windows.Interop.ComponentDispatcher> class implements the message loop manager for [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)].</span></span> <span data-ttu-id="a97dd-121">O <xref:System.Windows.Interop.ComponentDispatcher> classe fornece ganchos para permitir que clientes externos para filtrar mensagens antes de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] processá-las.</span><span class="sxs-lookup"><span data-stu-id="a97dd-121">The <xref:System.Windows.Interop.ComponentDispatcher> class provides hooks to enable external clients to filter messages before [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] processes them.</span></span>  
  
 <span data-ttu-id="a97dd-122">A implementação de interoperação trata o <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> evento, que permite [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controles para processar mensagens antes de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controles.</span><span class="sxs-lookup"><span data-stu-id="a97dd-122">The interoperation implementation handles the <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> event, which enables [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controls to process messages before [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] controls.</span></span>  
  
### <a name="surrogate-windows-forms-message-loop"></a><span data-ttu-id="a97dd-123">Loop de mensagens substituto dos Windows Forms</span><span class="sxs-lookup"><span data-stu-id="a97dd-123">Surrogate Windows Forms Message Loop</span></span>  
 <span data-ttu-id="a97dd-124">Por padrão, o <xref:System.Windows.Forms.Application?displayProperty=nameWithType> classe contém o loop de mensagens principal para [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a97dd-124">By default, the <xref:System.Windows.Forms.Application?displayProperty=nameWithType> class contains the primary message loop for [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] applications.</span></span> <span data-ttu-id="a97dd-125">Durante a interoperação, o loop de mensagens [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] não processa mensagens.</span><span class="sxs-lookup"><span data-stu-id="a97dd-125">During interoperation, the [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] message loop does not process messages.</span></span> <span data-ttu-id="a97dd-126">Portanto, essa lógica deve ser reproduzida.</span><span class="sxs-lookup"><span data-stu-id="a97dd-126">Therefore, this logic must be reproduced.</span></span> <span data-ttu-id="a97dd-127">O manipulador para o <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> evento executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a97dd-127">The handler for the <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> event performs the following steps:</span></span>  
  
1.  <span data-ttu-id="a97dd-128">Filtra a mensagem usando o <xref:System.Windows.Forms.IMessageFilter> interface.</span><span class="sxs-lookup"><span data-stu-id="a97dd-128">Filters the message using the <xref:System.Windows.Forms.IMessageFilter> interface.</span></span>  
  
2.  <span data-ttu-id="a97dd-129">Chama o <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> método.</span><span class="sxs-lookup"><span data-stu-id="a97dd-129">Calls the <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=nameWithType> method.</span></span>  
  
3.  <span data-ttu-id="a97dd-130">Converte e envia a mensagem, se necessário.</span><span class="sxs-lookup"><span data-stu-id="a97dd-130">Translates and dispatches the message, if it is required.</span></span>  
  
4.  <span data-ttu-id="a97dd-131">Passa a mensagem para o controle de host, se nenhum outro controle processar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="a97dd-131">Passes the message to the hosting control, if no other controls process the message.</span></span>  
  
### <a name="ikeyboardinputsink-implementation"></a><span data-ttu-id="a97dd-132">Implementação de IKeyboardInputSink</span><span class="sxs-lookup"><span data-stu-id="a97dd-132">IKeyboardInputSink Implementation</span></span>  
 <span data-ttu-id="a97dd-133">O loop de mensagens substituto trata do gerenciamento do teclado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-133">The surrogate message loop handles keyboard management.</span></span> <span data-ttu-id="a97dd-134">Portanto, o <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> método é o único <xref:System.Windows.Interop.IKeyboardInputSink> membro que requer uma implementação na <xref:System.Windows.Forms.Integration.WindowsFormsHost> classe.</span><span class="sxs-lookup"><span data-stu-id="a97dd-134">Therefore, the <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> method is the only <xref:System.Windows.Interop.IKeyboardInputSink> member that requires an implementation in the <xref:System.Windows.Forms.Integration.WindowsFormsHost> class.</span></span>  
  
 <span data-ttu-id="a97dd-135">Por padrão, o <xref:System.Windows.Interop.HwndHost> classe retorna `false` para sua <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> implementação.</span><span class="sxs-lookup"><span data-stu-id="a97dd-135">By default, the <xref:System.Windows.Interop.HwndHost> class returns `false` for its <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> implementation.</span></span> <span data-ttu-id="a97dd-136">Isso evita a tabulação de um controle [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] para um controle [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].</span><span class="sxs-lookup"><span data-stu-id="a97dd-136">This prevents tabbing from a [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] control to a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] control.</span></span>  
  
 <span data-ttu-id="a97dd-137">O <xref:System.Windows.Forms.Integration.WindowsFormsHost> implementação o <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> método executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="a97dd-137">The <xref:System.Windows.Forms.Integration.WindowsFormsHost> implementation of the <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=nameWithType> method performs the following steps:</span></span>  
  
1.  <span data-ttu-id="a97dd-138">Localiza o primeiro ou último [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] controle contido pelo <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle e que pode receber foco.</span><span class="sxs-lookup"><span data-stu-id="a97dd-138">Finds the first or last [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] control that is contained by the <xref:System.Windows.Forms.Integration.WindowsFormsHost> control and that can receive focus.</span></span> <span data-ttu-id="a97dd-139">A escolha do controle depende de informações de passagem.</span><span class="sxs-lookup"><span data-stu-id="a97dd-139">The control choice depends on traversal information.</span></span>  
  
2.  <span data-ttu-id="a97dd-140">Define o foco para o controle e retorna `true`.</span><span class="sxs-lookup"><span data-stu-id="a97dd-140">Sets focus to the control and returns `true`.</span></span>  
  
3.  <span data-ttu-id="a97dd-141">Se nenhum controle puder receber o foco, retorna `false`.</span><span class="sxs-lookup"><span data-stu-id="a97dd-141">If no control can receive focus, returns `false`.</span></span>  
  
### <a name="windowsformshost-registration"></a><span data-ttu-id="a97dd-142">Registro de WindowsFormsHost</span><span class="sxs-lookup"><span data-stu-id="a97dd-142">WindowsFormsHost Registration</span></span>  
 <span data-ttu-id="a97dd-143">Quando o manipulador de janela para um <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle é criado, o <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle chama um método estático interno que registra sua presença no loop de mensagens.</span><span class="sxs-lookup"><span data-stu-id="a97dd-143">When the window handle to a <xref:System.Windows.Forms.Integration.WindowsFormsHost> control is created, the <xref:System.Windows.Forms.Integration.WindowsFormsHost> control calls an internal static method that registers its presence for the message loop.</span></span>  
  
 <span data-ttu-id="a97dd-144">Durante o registro, o <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle examina o loop de mensagens.</span><span class="sxs-lookup"><span data-stu-id="a97dd-144">During registration, the <xref:System.Windows.Forms.Integration.WindowsFormsHost> control examines the message loop.</span></span> <span data-ttu-id="a97dd-145">Se o loop de mensagem não tiver sido iniciado, o <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> manipulador de eventos é criado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-145">If the message loop has not been started, the <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> event handler is created.</span></span> <span data-ttu-id="a97dd-146">O loop de mensagens é considerado para estar em execução quando o <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> manipulador de eventos está anexado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-146">The message loop is considered to be running when the <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=nameWithType> event handler is attached.</span></span>  
  
 <span data-ttu-id="a97dd-147">Quando o identificador de janela é destruído, o <xref:System.Windows.Forms.Integration.WindowsFormsHost> controle remove a próprio do registro.</span><span class="sxs-lookup"><span data-stu-id="a97dd-147">When the window handle is destroyed, the <xref:System.Windows.Forms.Integration.WindowsFormsHost> control removes itself from registration.</span></span>  
  
## <a name="elementhost-keyboard-and-message-processing"></a><span data-ttu-id="a97dd-148">Processamento de mensagens e teclado de ElementHost</span><span class="sxs-lookup"><span data-stu-id="a97dd-148">ElementHost Keyboard and Message Processing</span></span>  
 <span data-ttu-id="a97dd-149">Quando hospedado por um aplicativo [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], o processamento de mensagens e teclado [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] consiste no seguinte:</span><span class="sxs-lookup"><span data-stu-id="a97dd-149">When hosted by a [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] application, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] keyboard and message processing consists of the following:</span></span>  
  
-   <span data-ttu-id="a97dd-150"><xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.IKeyboardInputSink>, e <xref:System.Windows.Interop.IKeyboardInputSite> implementações de interfaces.</span><span class="sxs-lookup"><span data-stu-id="a97dd-150"><xref:System.Windows.Interop.HwndSource>, <xref:System.Windows.Interop.IKeyboardInputSink>, and <xref:System.Windows.Interop.IKeyboardInputSite> interface implementations.</span></span>  
  
-   <span data-ttu-id="a97dd-151">Teclas de direção e tabulação.</span><span class="sxs-lookup"><span data-stu-id="a97dd-151">Tabbing and arrow keys.</span></span>  
  
-   <span data-ttu-id="a97dd-152">Teclas de comando e teclas de caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a97dd-152">Command keys and dialog box keys.</span></span>  
  
-   <span data-ttu-id="a97dd-153">Processamento do acelerador [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)].</span><span class="sxs-lookup"><span data-stu-id="a97dd-153">[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] accelerator processing.</span></span>  
  
 <span data-ttu-id="a97dd-154">As seções a seguir descrevem essas partes em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a97dd-154">The following sections describe these parts in more detail.</span></span>  
  
### <a name="interface-implementations"></a><span data-ttu-id="a97dd-155">Implementações de interfaces</span><span class="sxs-lookup"><span data-stu-id="a97dd-155">Interface Implementations</span></span>  
 <span data-ttu-id="a97dd-156">Em [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], as mensagens de teclado são encaminhadas para o identificador de janela do controle que tem o foco.</span><span class="sxs-lookup"><span data-stu-id="a97dd-156">In [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)], keyboard messages are routed to the window handle of the control that has focus.</span></span> <span data-ttu-id="a97dd-157">No <xref:System.Windows.Forms.Integration.ElementHost> controle, essas mensagens são roteadas para o elemento hospedado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-157">In the <xref:System.Windows.Forms.Integration.ElementHost> control, these messages are routed to the hosted element.</span></span> <span data-ttu-id="a97dd-158">Para fazer isso, o <xref:System.Windows.Forms.Integration.ElementHost> controle fornece uma <xref:System.Windows.Interop.HwndSource> instância.</span><span class="sxs-lookup"><span data-stu-id="a97dd-158">To accomplish this, the <xref:System.Windows.Forms.Integration.ElementHost> control provides an <xref:System.Windows.Interop.HwndSource> instance.</span></span> <span data-ttu-id="a97dd-159">Se o <xref:System.Windows.Forms.Integration.ElementHost> controle tem foco, o <xref:System.Windows.Interop.HwndSource> instância encaminha a maioria dos teclado de entrada para que possa ser processado pelo [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> classe.</span><span class="sxs-lookup"><span data-stu-id="a97dd-159">If the <xref:System.Windows.Forms.Integration.ElementHost> control has focus, the <xref:System.Windows.Interop.HwndSource> instance routes most keyboard input so that it can be processed by the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> class.</span></span>  
  
 <span data-ttu-id="a97dd-160">O <xref:System.Windows.Interop.HwndSource> classe implementa o <xref:System.Windows.Interop.IKeyboardInputSink> e <xref:System.Windows.Interop.IKeyboardInputSite> interfaces.</span><span class="sxs-lookup"><span data-stu-id="a97dd-160">The <xref:System.Windows.Interop.HwndSource> class implements the <xref:System.Windows.Interop.IKeyboardInputSink> and <xref:System.Windows.Interop.IKeyboardInputSite> interfaces.</span></span>  
  
 <span data-ttu-id="a97dd-161">Interoperação de teclado depende de implementa o <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> método para o identificador de chave de guia e seta para chave de entrada que move o foco para fora de elementos hospedados.</span><span class="sxs-lookup"><span data-stu-id="a97dd-161">Keyboard interoperation relies on implementing the <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> method to handle TAB key and arrow key input that moves focus out of hosted elements.</span></span>  
  
### <a name="tabbing-and-arrow-keys"></a><span data-ttu-id="a97dd-162">Teclas de direção e tabulação</span><span class="sxs-lookup"><span data-stu-id="a97dd-162">Tabbing and Arrow Keys</span></span>  
 <span data-ttu-id="a97dd-163">O [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] lógica de seleção é mapeada para o <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> e <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> navegação de chave de métodos para implementar TAB e direção.</span><span class="sxs-lookup"><span data-stu-id="a97dd-163">The [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] selection logic is mapped to the <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> and <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> methods to implement TAB and arrow key navigation.</span></span> <span data-ttu-id="a97dd-164">Substituindo o <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> método realiza esse mapeamento.</span><span class="sxs-lookup"><span data-stu-id="a97dd-164">Overriding the <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> method accomplishes this mapping.</span></span>  
  
### <a name="command-keys-and-dialog-box-keys"></a><span data-ttu-id="a97dd-165">Teclas de comando e teclas de caixa de diálogo</span><span class="sxs-lookup"><span data-stu-id="a97dd-165">Command Keys and Dialog Box Keys</span></span>  
 <span data-ttu-id="a97dd-166">Para dar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] a primeira oportunidade para processar o comando chaves e as chaves de caixa de diálogo, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] comando pré-processamento está conectado a <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> método.</span><span class="sxs-lookup"><span data-stu-id="a97dd-166">To give [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] the first opportunity to process command keys and dialog keys, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] command preprocessing is connected to the <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> method.</span></span> <span data-ttu-id="a97dd-167">Substituindo o <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=nameWithType> método conecta as duas tecnologias.</span><span class="sxs-lookup"><span data-stu-id="a97dd-167">Overriding the <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=nameWithType> method connects the two technologies.</span></span>  
  
 <span data-ttu-id="a97dd-168">Com o <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> método, os elementos hospedados podem lidar com qualquer mensagem de chave, como WM_KEYDOWN, WM_KEYUP, WM_SYSKEYDOWN ou WM_SYSKEYUP, inclusive teclas de comando, como guia, ENTER, ESC e seta de chaves.</span><span class="sxs-lookup"><span data-stu-id="a97dd-168">With the <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> method, the hosted elements can handle any key message, such as WM_KEYDOWN, WM_KEYUP, WM_SYSKEYDOWN, or WM_SYSKEYUP, including command keys, such as TAB, ENTER, ESC, and arrow keys.</span></span> <span data-ttu-id="a97dd-169">Se uma mensagem de tecla não for tratada, ela será enviada para a hierarquia ancestral de [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] para que seja tratada.</span><span class="sxs-lookup"><span data-stu-id="a97dd-169">If a key message is not handled, it is sent up the [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] ancestor hierarchy for handling.</span></span>  
  
### <a name="accelerator-processing"></a><span data-ttu-id="a97dd-170">Processamento do acelerador</span><span class="sxs-lookup"><span data-stu-id="a97dd-170">Accelerator Processing</span></span>  
 <span data-ttu-id="a97dd-171">Para processar aceleradores corretamente, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] processamento do acelerador deve estar conectado para o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> classe.</span><span class="sxs-lookup"><span data-stu-id="a97dd-171">To process accelerators correctly, [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] accelerator processing must be connected to the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> class.</span></span> <span data-ttu-id="a97dd-172">Além disso, todas as mensagens WM_CHAR devem ser encaminhadas corretamente para os elementos hospedados.</span><span class="sxs-lookup"><span data-stu-id="a97dd-172">Additionally, all WM_CHAR messages must be correctly routed to hosted elements.</span></span>  
  
 <span data-ttu-id="a97dd-173">Porque o padrão <xref:System.Windows.Interop.HwndSource> implementação o <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> método retorna `false`, mensagens WM_CHAR são processadas usando a seguinte lógica:</span><span class="sxs-lookup"><span data-stu-id="a97dd-173">Because the default <xref:System.Windows.Interop.HwndSource> implementation of the <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> method returns `false`, WM_CHAR messages are processed using the following logic:</span></span>  
  
-   <span data-ttu-id="a97dd-174">O <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=nameWithType> método é substituído para garantir que todas as mensagens WM_CHAR são encaminhadas para elementos hospedados.</span><span class="sxs-lookup"><span data-stu-id="a97dd-174">The <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=nameWithType> method is overridden to ensure that all WM_CHAR messages are forwarded to hosted elements.</span></span>  
  
-   <span data-ttu-id="a97dd-175">Se a tecla ALT estiver pressionada, a mensagem será WM_SYSCHAR.</span><span class="sxs-lookup"><span data-stu-id="a97dd-175">If the ALT key is pressed, the message is WM_SYSCHAR.</span></span> [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]<span data-ttu-id="a97dd-176">não processa previamente a esta mensagem por meio de <xref:System.Windows.Forms.Control.IsInputChar%2A> método.</span><span class="sxs-lookup"><span data-stu-id="a97dd-176"> does not preprocess this message through the <xref:System.Windows.Forms.Control.IsInputChar%2A> method.</span></span> <span data-ttu-id="a97dd-177">Portanto, o <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> método é substituído para consultar o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> para um acelerador registrado.</span><span class="sxs-lookup"><span data-stu-id="a97dd-177">Therefore, the <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> method is overridden to query the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> for a registered accelerator.</span></span> <span data-ttu-id="a97dd-178">Se um acelerador registrado for encontrado, <xref:System.Windows.Input.AccessKeyManager> processa.</span><span class="sxs-lookup"><span data-stu-id="a97dd-178">If a registered accelerator is found, <xref:System.Windows.Input.AccessKeyManager> processes it.</span></span>  
  
-   <span data-ttu-id="a97dd-179">Se não for pressionada a tecla ALT, o [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> classe processa a entrada não tratada.</span><span class="sxs-lookup"><span data-stu-id="a97dd-179">If the ALT key is not pressed, the [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> class processes the unhandled input.</span></span> <span data-ttu-id="a97dd-180">Se a entrada é um acelerador de <xref:System.Windows.Input.AccessKeyManager> processa.</span><span class="sxs-lookup"><span data-stu-id="a97dd-180">If the input is an accelerator, the <xref:System.Windows.Input.AccessKeyManager> processes it.</span></span> <span data-ttu-id="a97dd-181">O <xref:System.Windows.Input.InputManager.PostProcessInput> evento é tratado para mensagens WM_CHAR que não foram processadas.</span><span class="sxs-lookup"><span data-stu-id="a97dd-181">The <xref:System.Windows.Input.InputManager.PostProcessInput> event is handled for WM_CHAR messages that were not processed.</span></span>  
  
 <span data-ttu-id="a97dd-182">Quando o usuário pressiona a tecla ALT, indicações visuais do acelerador são mostradas em todo o formulário.</span><span class="sxs-lookup"><span data-stu-id="a97dd-182">When the user presses the ALT key, accelerator visual cues are shown on the whole form.</span></span> <span data-ttu-id="a97dd-183">Para dar suporte a esse comportamento, todos os <xref:System.Windows.Forms.Integration.ElementHost> controles no formulário ativo recebem mensagens WM_SYSKEYDOWN, independentemente de qual controle tem foco.</span><span class="sxs-lookup"><span data-stu-id="a97dd-183">To support this behavior, all <xref:System.Windows.Forms.Integration.ElementHost> controls on the active form receive WM_SYSKEYDOWN messages, regardless of which control has focus.</span></span>  
  
 <span data-ttu-id="a97dd-184">As mensagens são enviadas somente ao <xref:System.Windows.Forms.Integration.ElementHost> controles no formulário ativo.</span><span class="sxs-lookup"><span data-stu-id="a97dd-184">Messages are sent only to <xref:System.Windows.Forms.Integration.ElementHost> controls in the active form.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a97dd-185">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a97dd-185">See Also</span></span>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>  
 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 [<span data-ttu-id="a97dd-186">Passo a passo: hospedando um controle composto do Windows Forms no WPF</span><span class="sxs-lookup"><span data-stu-id="a97dd-186">Walkthrough: Hosting a Windows Forms Composite Control in WPF</span></span>](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)  
 [<span data-ttu-id="a97dd-187">Passo a passo: hospedando um controle composto do WPF no Windows Forms</span><span class="sxs-lookup"><span data-stu-id="a97dd-187">Walkthrough: Hosting a WPF Composite Control in Windows Forms</span></span>](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)  
 [<span data-ttu-id="a97dd-188">Interoperação do WPF e do Win32</span><span class="sxs-lookup"><span data-stu-id="a97dd-188">WPF and Win32 Interoperation</span></span>](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)