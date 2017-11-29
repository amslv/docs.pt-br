---
title: Contadores de desempenho do WCF
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: performance counters [WCF]
ms.assetid: f559b2bd-ed83-4988-97a1-e88f06646609
caps.latest.revision: "37"
author: Erikre
ms.author: erikre
manager: erikre
ms.openlocfilehash: 2136b4f9ab97f7ed0e4c31e6ffc26f788546419b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2017
---
# <a name="wcf-performance-counters"></a><span data-ttu-id="ee89c-102">Contadores de desempenho do WCF</span><span class="sxs-lookup"><span data-stu-id="ee89c-102">WCF Performance Counters</span></span>
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)]<span data-ttu-id="ee89c-103">inclui um grande conjunto de contadores de desempenho para ajudá-lo a avaliar o desempenho do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee89c-103"> includes a large set of performance counters to help you gauge your application's performance.</span></span>  
  
## <a name="enabling-performance-counters"></a><span data-ttu-id="ee89c-104">Habilitar contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="ee89c-104">Enabling Performance Counters</span></span>  
 <span data-ttu-id="ee89c-105">Você pode habilitar os contadores de desempenho para um [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] serviço por meio do arquivo de configuração App. config do [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] de serviço da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ee89c-105">You can enable performance counters for a [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] service through the app.config configuration file of the [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] service as follows:</span></span>  
  
```xml  
<configuration>  
    <system.serviceModel>  
        <diagnostics performanceCounters="All" />  
    </system.serviceModel>  
</configuration>  
```  
  
 <span data-ttu-id="ee89c-106">O `performanceCounters` atributo pode ser definido para habilitar um tipo específico de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-106">The `performanceCounters` attribute can be set to enable a specific type of performance counters.</span></span> <span data-ttu-id="ee89c-107">Os valores válidos são</span><span class="sxs-lookup"><span data-stu-id="ee89c-107">Valid values are</span></span>  
  
-   <span data-ttu-id="ee89c-108">Todos: Todos os contadores de categoria (ServiceModelService, ServiceModelEndpoint e ServiceModelOperation) estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="ee89c-108">All: All category counters (ServiceModelService, ServiceModelEndpoint and ServiceModelOperation) are enabled.</span></span>  
  
-   <span data-ttu-id="ee89c-109">ServiceOnly: Somente contadores de categoria de ServiceModelService estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="ee89c-109">ServiceOnly: Only ServiceModelService category counters are enabled.</span></span> <span data-ttu-id="ee89c-110">Este é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="ee89c-110">This is the default value.</span></span>  
  
-   <span data-ttu-id="ee89c-111">Off: Os contadores de desempenho do ServiceModel * são desabilitados.</span><span class="sxs-lookup"><span data-stu-id="ee89c-111">Off: ServiceModel* performance counters are disabled.</span></span>  
  
 <span data-ttu-id="ee89c-112">Se você deseja habilitar os contadores de desempenho para todos os [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] aplicativos, você pode colocar as definições de configuração no arquivo Machine. config.</span><span class="sxs-lookup"><span data-stu-id="ee89c-112">If you want to enable performance counters for all [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] applications, you can place the configuration settings in the Machine.config file.</span></span>  <span data-ttu-id="ee89c-113">Consulte o **aumentando o tamanho de memória para contadores de desempenho** seção abaixo para obter mais informações sobre como configurar a memória suficiente para contadores de desempenho em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ee89c-113">Please see the **Increasing Memory Size for Performance Counters** section below for more information on configuring sufficient memory for performance counters on your machine.</span></span>  
  
 <span data-ttu-id="ee89c-114">Se você usar [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] pontos de extensibilidade, como chamadores de operação personalizado, você deve também emitir seus próprios contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-114">If you use [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] extensibility points such as custom operation invokers, you should also emit your own performance counters.</span></span> <span data-ttu-id="ee89c-115">Isso ocorre porque se você implementar um ponto de extensibilidade, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] não pode emitir os dados do contador de desempenho padrão no caminho padrão.</span><span class="sxs-lookup"><span data-stu-id="ee89c-115">This is because if you implement an extensibility point, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] may no longer emit the standard performance counter data in the default path.</span></span> <span data-ttu-id="ee89c-116">Se você não implementa o suporte de contador de desempenho manual, você não verá os dados de contador de desempenho esperados.</span><span class="sxs-lookup"><span data-stu-id="ee89c-116">If you do not implement manual performance counter support, you may not see the performance counter data you expect.</span></span>  
  
 <span data-ttu-id="ee89c-117">Você também pode habilitar os contadores de desempenho no seu código seguinte:</span><span class="sxs-lookup"><span data-stu-id="ee89c-117">You can also enable performance counters in your code as follows,</span></span>  
  
```  
using System.Configuration;  
using System.ServiceModel.Configuration;  
using System.ServiceModel.Diagnostics;  
Configuration config = ConfigurationManager.OpenExeConfiguration(  
    ConfigurationUserLevel.None);  
ServiceModelSectionGroup sg = ServiceModelSectionGroup.GetSectionGroup(config);  
sg.Diagnostic.PerformanceCounters = PerformanceCounterScope.All;  
config.Save();  
```  
  
## <a name="viewing-performance-data"></a><span data-ttu-id="ee89c-118">Exibir dados de desempenho</span><span class="sxs-lookup"><span data-stu-id="ee89c-118">Viewing Performance Data</span></span>  
 <span data-ttu-id="ee89c-119">Para exibir os dados capturados por contadores de desempenho, você pode usar o Monitor de desempenho (Perfmon.exe) que vem com o Windows.</span><span class="sxs-lookup"><span data-stu-id="ee89c-119">To view data captured by the performance counters, you can use the Performance Monitor (Perfmon.exe) that comes with Windows.</span></span> <span data-ttu-id="ee89c-120">Você pode iniciar essa ferramenta indo para **iniciar**e clique em **executar** e digite `perfmon.exe` na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee89c-120">You can launch this tool by going to **Start**, and click **Run** and type `perfmon.exe` in the dialog box.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ee89c-121">Instâncias do contador de desempenho podem ser liberadas antes das últimas mensagens foram processadas pelo dispatcher do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ee89c-121">Performance counter instances may be released before the last messages have been processed by the endpoint dispatcher.</span></span> <span data-ttu-id="ee89c-122">Isso pode resultar em dados de desempenho não são capturados para algumas mensagens.</span><span class="sxs-lookup"><span data-stu-id="ee89c-122">This can result in performance data not being captured for a few messages.</span></span>  
  
## <a name="increasing-memory-size-for-performance-counters"></a><span data-ttu-id="ee89c-123">Aumentando o tamanho de memória para contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="ee89c-123">Increasing Memory Size for Performance Counters</span></span>  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]<span data-ttu-id="ee89c-124">usa separar memória compartilhada para suas categorias de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-124"> uses separate shared memory for its performance counter categories.</span></span>  
  
 <span data-ttu-id="ee89c-125">Por padrão, separado de memória compartilhada é definida como um quarto do tamanho da memória do contador de desempenho global.</span><span class="sxs-lookup"><span data-stu-id="ee89c-125">By default, separate shared memory is set to a quarter the size of global performance counter memory.</span></span> <span data-ttu-id="ee89c-126">A memória de contador de desempenho global padrão é 524.288 bytes.</span><span class="sxs-lookup"><span data-stu-id="ee89c-126">The default global performance counter memory is 524,288 bytes.</span></span> <span data-ttu-id="ee89c-127">Portanto, os três [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] categorias de contador de desempenho têm um tamanho padrão de aproximadamente 128 KB cada.</span><span class="sxs-lookup"><span data-stu-id="ee89c-127">Therefore, the three [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] performance counter categories have a default size of approximately 128KB each.</span></span> <span data-ttu-id="ee89c-128">Dependendo das características tempo de execução do [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] aplicativos em um computador, a memória de contador de desempenho podem ser esgotados.</span><span class="sxs-lookup"><span data-stu-id="ee89c-128">Depending upon the runtime characteristics of the [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] applications on a machine, performance counter memory may be exhausted.</span></span> <span data-ttu-id="ee89c-129">Quando isso acontece, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] grava um erro no log de eventos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee89c-129">When this happens, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] writes an error to the application event log.</span></span> <span data-ttu-id="ee89c-130">O conteúdo do erro informa que um contador de desempenho não foi carregado, e a entrada contém a exceção "System. InvalidOperationException: modo de exibição de arquivo de contadores personalizados está esgotada."</span><span class="sxs-lookup"><span data-stu-id="ee89c-130">The content of the error states that a performance counter was not loaded, and the entry contains the exception "System.InvalidOperationException: Custom counters file view is out of memory."</span></span> <span data-ttu-id="ee89c-131">Se o rastreamento estiver habilitado no nível de erro, essa falha também é rastreada.</span><span class="sxs-lookup"><span data-stu-id="ee89c-131">If tracing is enabled at the error level, this failure is also traced.</span></span> <span data-ttu-id="ee89c-132">Se a memória de contador de desempenho é esgotada, continuando a executar sua [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] aplicativos com contadores de desempenho ativados podem resultar em degradação do desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-132">If performance counter memory is exhausted, continuing to run your [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] applications with performance counters enabled could result in performance degradation.</span></span> <span data-ttu-id="ee89c-133">Se você for um administrador do computador, você deve configurá-lo para alocar memória suficiente para suportar o número máximo de contadores de desempenho que podem existir a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="ee89c-133">If you are an administrator of the machine, you should configure it to allocate enough memory to support the maximum number of performance counters that can exist at any time.</span></span>  
  
 <span data-ttu-id="ee89c-134">Você pode alterar a quantidade de memória do contador de desempenho para [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] categorias no registro.</span><span class="sxs-lookup"><span data-stu-id="ee89c-134">You can change the amount of performance counter memory for [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] categories in the registry.</span></span> <span data-ttu-id="ee89c-135">Para fazer isso, você precisa adicionar um novo valor DWORD chamado `FileMappingSize` para três locais a seguir e defina-o como o valor desejado em bytes.</span><span class="sxs-lookup"><span data-stu-id="ee89c-135">To do so, you need to add a new DWORD value named `FileMappingSize` to the three following locations, and set it to the desired value in bytes.</span></span> <span data-ttu-id="ee89c-136">Reinicialize o computador para que essas alterações são levadas em vigor.</span><span class="sxs-lookup"><span data-stu-id="ee89c-136">Reboot your machine so that these changes are taken into effect.</span></span>  
  
-   <span data-ttu-id="ee89c-137">HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="ee89c-137">HKLM\System\CurrentControlSet\Services\ServiceModelEndpoint 4.0.0.0\Performance</span></span>  
  
-   <span data-ttu-id="ee89c-138">HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="ee89c-138">HKLM\System\CurrentControlSet\Services\ServiceModelOperation 4.0.0.0\Performance</span></span>  
  
-   <span data-ttu-id="ee89c-139">HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance</span><span class="sxs-lookup"><span data-stu-id="ee89c-139">HKLM\System\CurrentControlSet\Services\ServiceModelService 4.0.0.0\Performance</span></span>  
  
 <span data-ttu-id="ee89c-140">Quando um grande número de objetos (por exemplo, ServiceHost) é descartado, mas esperando para ser coletado como lixo, a `PrivateBytes` contador de desempenho registrará um número extraordinariamente alto.</span><span class="sxs-lookup"><span data-stu-id="ee89c-140">When a large number of objects (for example, ServiceHost) are disposed of but waiting to be garbage-collected, the `PrivateBytes` performance counter will register an unusually high number.</span></span> <span data-ttu-id="ee89c-141">Para resolver esse problema, você pode adicionar seus próprios contadores específicos do aplicativo, ou usar o `performanceCounters` atributo para habilitar os contadores de nível de serviço somente.</span><span class="sxs-lookup"><span data-stu-id="ee89c-141">To resolve this problem, you can either add your own application-specific counters, or use the `performanceCounters` attribute to enable only service-level counters.</span></span>  
  
## <a name="types-of-performance-counters"></a><span data-ttu-id="ee89c-142">Tipos de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="ee89c-142">Types of Performance Counters</span></span>  
 <span data-ttu-id="ee89c-143">Contadores de desempenho têm como escopo três níveis diferentes: serviço, o ponto de extremidade e a operação.</span><span class="sxs-lookup"><span data-stu-id="ee89c-143">Performance counters are scoped to three different levels: Service, Endpoint and Operation.</span></span>  
  
 <span data-ttu-id="ee89c-144">Você pode usar o WMI para recuperar o nome de uma instância de contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-144">You can use WMI to retrieve the name of a performance counter instance.</span></span> <span data-ttu-id="ee89c-145">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="ee89c-145">For example,</span></span>  
  
-   <span data-ttu-id="ee89c-146">Nome de instância do contador de serviço pode ser obtido por meio do WMI [Service](../../../../../docs/framework/wcf/diagnostics/wmi/service.md) propriedade de "CounterInstanceName" da instância.</span><span class="sxs-lookup"><span data-stu-id="ee89c-146">Service counter instance name can be obtained through WMI [Service](../../../../../docs/framework/wcf/diagnostics/wmi/service.md) instance's "CounterInstanceName" property.</span></span>  
  
-   <span data-ttu-id="ee89c-147">Nome de instância de contador do ponto de extremidade pode ser obtido por meio do WMI [ponto de extremidade](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) propriedade de "CounterInstanceName" da instância.</span><span class="sxs-lookup"><span data-stu-id="ee89c-147">Endpoint counter instance name can be obtained through WMI [Endpoint](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) instance's "CounterInstanceName" property.</span></span>  
  
-   <span data-ttu-id="ee89c-148">Nome de instância do contador de operação pode ser obtido por meio do WMI [ponto de extremidade](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) "GetOperationCounterInstanceName" de método instância do.</span><span class="sxs-lookup"><span data-stu-id="ee89c-148">Operation counter instance name can be obtained through WMI [Endpoint](../../../../../docs/framework/wcf/diagnostics/wmi/endpoint.md) instance's "GetOperationCounterInstanceName" method.</span></span>  
  
 <span data-ttu-id="ee89c-149">Para obter mais informações sobre WMI, consulte [usando o Windows Management Instrumentation para diagnóstico](../../../../../docs/framework/wcf/diagnostics/wmi/index.md).</span><span class="sxs-lookup"><span data-stu-id="ee89c-149">For more information on WMI, see [Using Windows Management Instrumentation for Diagnostics](../../../../../docs/framework/wcf/diagnostics/wmi/index.md).</span></span>  
  
### <a name="service-performance-counters"></a><span data-ttu-id="ee89c-150">Contadores de desempenho do serviço</span><span class="sxs-lookup"><span data-stu-id="ee89c-150">Service performance counters</span></span>  
 <span data-ttu-id="ee89c-151">Contadores de desempenho serviço medem o comportamento de serviço como um todo e podem ser usados para diagnosticar o desempenho do serviço inteiro.</span><span class="sxs-lookup"><span data-stu-id="ee89c-151">Service performance counters measure the service behavior as a whole and can be used to diagnose the performance of the whole service.</span></span> <span data-ttu-id="ee89c-152">Eles podem ser encontrados no `ServiceModelService 4.0.0.0` objeto de desempenho durante a exibição de Monitor de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-152">They can be found under the `ServiceModelService 4.0.0.0` performance object when viewing with Performance Monitor.</span></span> <span data-ttu-id="ee89c-153">As instâncias são nomeadas usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="ee89c-153">The instances are named using the following pattern:</span></span>  
  
```  
ServiceName@ServiceBaseAddress  
```  
  
 <span data-ttu-id="ee89c-154">Um contador em um escopo do serviço é agregado de contador em uma coleção de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ee89c-154">A counter in a service scope is aggregated from counter in a collection of endpoints.</span></span>  
  
 <span data-ttu-id="ee89c-155">Contadores de desempenho para a criação de instância de serviço são incrementados quando um InstanceContext novo é criado.</span><span class="sxs-lookup"><span data-stu-id="ee89c-155">Performance counters for service instance creation are incremented when a new InstanceContext is created.</span></span> <span data-ttu-id="ee89c-156">Observe que um InstanceContext novo é criado, mesmo quando você receber uma mensagem de ativação não (com um serviço existente), ou quando você se conectar a uma instância de uma sessão, encerra a sessão e, em seguida, reconectar-se de outra sessão.</span><span class="sxs-lookup"><span data-stu-id="ee89c-156">Note that a new InstanceContext is created even when you receive a non-activating message (with an existing service), or when you connect to an instance from one session, end the session, and then reconnect from another session.</span></span>  
  
### <a name="endpoint-performance-counters"></a><span data-ttu-id="ee89c-157">Contadores de desempenho do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="ee89c-157">Endpoint performance counters</span></span>  
 <span data-ttu-id="ee89c-158">Contadores de desempenho do ponto de extremidade permitem que você examinar dados refletindo como um ponto de extremidade é aceitar mensagens.</span><span class="sxs-lookup"><span data-stu-id="ee89c-158">Endpoint performance counters enable you to look at data reflecting how an endpoint is accepting messages.</span></span> <span data-ttu-id="ee89c-159">Eles podem ser encontrados no `ServiceModelEndpoint 4.0.0.0` objeto de desempenho ao exibir usando o Monitor de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-159">They can be found under the `ServiceModelEndpoint 4.0.0.0` performance object when viewing using the Performance Monitor.</span></span> <span data-ttu-id="ee89c-160">As instâncias são nomeadas usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="ee89c-160">The instances are named using the following pattern:</span></span>  
  
```  
(ServiceName).(ContractName)@(endpoint listener address)  
```  
  
 <span data-ttu-id="ee89c-161">Os dados são semelhantes ao que é coletado para operações individuais, mas só é agregado entre o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="ee89c-161">The data is similar to what is collected for individual operations, but is only aggregated across the endpoint.</span></span>  
  
 <span data-ttu-id="ee89c-162">Um contador em um escopo de ponto de extremidade é agregado de contadores em uma coleção de operações.</span><span class="sxs-lookup"><span data-stu-id="ee89c-162">A counter in an endpoint scope is aggregated from counters in a collection of operations.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ee89c-163">Se dois pontos de extremidade têm endereços e nomes de contrato idênticos, eles serão mapeados para a mesma instância do contador.</span><span class="sxs-lookup"><span data-stu-id="ee89c-163">If two endpoints have identical contract names and addresses, they are mapped to the same counter instance.</span></span>  
  
### <a name="operation-performance-counters"></a><span data-ttu-id="ee89c-164">Contadores de desempenho da operação</span><span class="sxs-lookup"><span data-stu-id="ee89c-164">Operation performance counters</span></span>  
 <span data-ttu-id="ee89c-165">Contadores de desempenho da operação estão localizados sob o `ServiceModelOperation 4.0.0.0` objeto de desempenho durante a exibição com o Monitor de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-165">Operation performance counters are found under the `ServiceModelOperation 4.0.0.0` performance object when viewing with the Performance Monitor.</span></span> <span data-ttu-id="ee89c-166">Cada operação tem uma instância individual.</span><span class="sxs-lookup"><span data-stu-id="ee89c-166">Each operation has an individual instance.</span></span> <span data-ttu-id="ee89c-167">Ou seja, se um dado contrato tem operações de 10, 10 instâncias de contador de operação são associadas com esse contrato.</span><span class="sxs-lookup"><span data-stu-id="ee89c-167">That is, if a given contract has 10 operations, 10 operation counter instances are associated with that contract.</span></span> <span data-ttu-id="ee89c-168">As instâncias de objeto são nomeadas usando o seguinte padrão:</span><span class="sxs-lookup"><span data-stu-id="ee89c-168">The object instances are named using the following pattern:</span></span>  
  
```  
(ServiceName).(ContractName).(OperationName)@(first endpoint listener address)  
```  
  
 <span data-ttu-id="ee89c-169">Esse contador permite avaliar como a chamada está sendo usada e como a operação está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="ee89c-169">This counter enables you to measure how the call is being used and how well the operation is performing.</span></span>  
  
 <span data-ttu-id="ee89c-170">Quando os contadores estão visíveis em vários escopos, os dados coletados de um escopo superior são agregados com dados de escopos inferiores.</span><span class="sxs-lookup"><span data-stu-id="ee89c-170">When counters are visible at multiple scopes, data gathered from a higher scope are aggregated with data from lower scopes.</span></span> <span data-ttu-id="ee89c-171">Por exemplo, `Calls` em um ponto de extremidade representa a soma de todas as chamadas de operação no ponto de extremidade; `Calls` em um serviço representa a soma de todas as chamadas para todos os pontos de extremidade no serviço.</span><span class="sxs-lookup"><span data-stu-id="ee89c-171">For example, `Calls` at an endpoint represents the sum of all operation calls within the endpoint; `Calls` at a service represents the sum of all calls to all endpoints within the service.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="ee89c-172">Se você tiver nomes de operação duplicado em um contrato, você somente obtém instâncias de um contador para as duas operações.</span><span class="sxs-lookup"><span data-stu-id="ee89c-172">If you have duplicate operation names on a contract, you only get one counter instances for both operations.</span></span>  
  
## <a name="programming-the-wcf-performance-counters"></a><span data-ttu-id="ee89c-173">Os contadores de desempenho do WCF de programação</span><span class="sxs-lookup"><span data-stu-id="ee89c-173">Programming the WCF Performance Counters</span></span>  
 <span data-ttu-id="ee89c-174">Vários arquivos são instalados na pasta de instalação do SDK para que você pode acessar o [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] programaticamente os contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="ee89c-174">Several files are installed in the SDK install folder so that you can access the [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] performance counters programmatically.</span></span> <span data-ttu-id="ee89c-175">Esses arquivos estão listados a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee89c-175">These files are listed as follows.</span></span>  
  
-   <span data-ttu-id="ee89c-176">_ServiceModelEndpointPerfCounters.vrg</span><span class="sxs-lookup"><span data-stu-id="ee89c-176">_ServiceModelEndpointPerfCounters.vrg</span></span>  
  
-   <span data-ttu-id="ee89c-177">_ServiceModelOperationPerfCounters.vrg</span><span class="sxs-lookup"><span data-stu-id="ee89c-177">_ServiceModelOperationPerfCounters.vrg</span></span>  
  
-   <span data-ttu-id="ee89c-178">_ServiceModelServicePerfCounters.vrg</span><span class="sxs-lookup"><span data-stu-id="ee89c-178">_ServiceModelServicePerfCounters.vrg</span></span>  
  
-   <span data-ttu-id="ee89c-179">_SMSvcHostPerfCounters.vrg</span><span class="sxs-lookup"><span data-stu-id="ee89c-179">_SMSvcHostPerfCounters.vrg</span></span>  
  
-   <span data-ttu-id="ee89c-180">_TransactionBridgePerfCounters.vrg</span><span class="sxs-lookup"><span data-stu-id="ee89c-180">_TransactionBridgePerfCounters.vrg</span></span>  
  
 <span data-ttu-id="ee89c-181">Para obter mais informações sobre como acessar os contadores de forma programática, consulte [arquitetura de programação de contador de desempenho](http://go.microsoft.com/fwlink/?LinkId=95179).</span><span class="sxs-lookup"><span data-stu-id="ee89c-181">For more information on how to access the counters programmatically, see [Performance Counter Programming Architecture](http://go.microsoft.com/fwlink/?LinkId=95179).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ee89c-182">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ee89c-182">See Also</span></span>  
 <span data-ttu-id="ee89c-183">[Administration and Diagnostics](../../../../../docs/framework/wcf/diagnostics/index.md) (Administração e diagnósticos)</span><span class="sxs-lookup"><span data-stu-id="ee89c-183">[Administration and Diagnostics](../../../../../docs/framework/wcf/diagnostics/index.md)</span></span>