---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: Os aplicativos SignalR de teste de unidade | Microsoft Docs
author: pfletcher
description: Este artigo descreve como usar os recursos de teste de unidade do SignalR 2.0.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/10/2014
ms.topic: article
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: d767e1a9d27670387133e5a48a8f92f5bdd39d9e
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
<a name="unit-testing-signalr-applications"></a><span data-ttu-id="b9b20-103">Teste de unidade e os aplicativos SignalR</span><span class="sxs-lookup"><span data-stu-id="b9b20-103">Unit Testing SignalR Applications</span></span>
====================
<span data-ttu-id="b9b20-104">por [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="b9b20-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

> <span data-ttu-id="b9b20-105">Este artigo descreve como usar os recursos de teste de unidade do SignalR 2.</span><span class="sxs-lookup"><span data-stu-id="b9b20-105">This article describes using the Unit Testing features of SignalR 2.</span></span> 
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="b9b20-106">Versões de software usadas neste tópico</span><span class="sxs-lookup"><span data-stu-id="b9b20-106">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="b9b20-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b9b20-107">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="b9b20-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="b9b20-108">.NET 4.5</span></span>
> - <span data-ttu-id="b9b20-109">SignalR versão 2</span><span class="sxs-lookup"><span data-stu-id="b9b20-109">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="b9b20-110">Perguntas e comentários</span><span class="sxs-lookup"><span data-stu-id="b9b20-110">Questions and comments</span></span>
> 
> <span data-ttu-id="b9b20-111">Deixe comentários em como você gostou neste tutorial e o que podemos melhorar nos comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="b9b20-111">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b9b20-112">Se você tiver dúvidas que não estão diretamente relacionadas ao tutorial, você poderá postá-los para o [ASP.NET SignalR fórum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) ou [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="b9b20-112">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a><span data-ttu-id="b9b20-113">Os aplicativos SignalR de teste de unidade</span><span class="sxs-lookup"><span data-stu-id="b9b20-113">Unit testing SignalR applications</span></span>

<span data-ttu-id="b9b20-114">Você pode usar os recursos de teste de unidade no SignalR 2 para criar testes de unidade para o seu aplicativo SignalR.</span><span class="sxs-lookup"><span data-stu-id="b9b20-114">You can use the unit test features in SignalR 2 to create unit tests for your SignalR application.</span></span> <span data-ttu-id="b9b20-115">SignalR 2 inclui a [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, que pode ser usado para criar um objeto de simulação para simular seus métodos de hub para teste.</span><span class="sxs-lookup"><span data-stu-id="b9b20-115">SignalR 2 includes the [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) interface, which can be used to create a mock object to simulate your hub methods for testing.</span></span>

<span data-ttu-id="b9b20-116">Nesta seção, você adicionará os testes de unidade para o aplicativo criado no [tutorial de Introdução](../getting-started/tutorial-getting-started-with-signalr.md) usando [XUnit.net](https://github.com/xunit/xunit) e [Moq](https://github.com/Moq/moq4).</span><span class="sxs-lookup"><span data-stu-id="b9b20-116">In this section, you'll add unit tests for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using [XUnit.net](https://github.com/xunit/xunit) and [Moq](https://github.com/Moq/moq4).</span></span>

<span data-ttu-id="b9b20-117">XUnit.net será usado para controlar o teste; Moq será usado para criar um [simular](http://en.wikipedia.org/wiki/Mock_object) objeto para teste.</span><span class="sxs-lookup"><span data-stu-id="b9b20-117">XUnit.net will be used to control the test; Moq will be used to create a [mock](http://en.wikipedia.org/wiki/Mock_object) object for testing.</span></span> <span data-ttu-id="b9b20-118">Outras estruturas fictícias podem ser usadas se quiser; [NSubstitute](http://nsubstitute.github.io/) também é uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="b9b20-118">Other mocking frameworks can be used if desired; [NSubstitute](http://nsubstitute.github.io/) is also a good choice.</span></span> <span data-ttu-id="b9b20-119">Este tutorial demonstra como configurar o objeto de simulação de duas maneiras: primeiro, usando um `dynamic` objeto (introduzido no .NET Framework 4) e, segundo, usando uma interface.</span><span class="sxs-lookup"><span data-stu-id="b9b20-119">This tutorial demonstrates how to set up the mock object in two ways: First, using a `dynamic` object (introduced in .NET Framework 4), and second, using an interface.</span></span>

### <a name="contents"></a><span data-ttu-id="b9b20-120">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="b9b20-120">Contents</span></span>

<span data-ttu-id="b9b20-121">Este tutorial contém as seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9b20-121">This tutorial contains the following sections.</span></span>

- [<span data-ttu-id="b9b20-122">Testes de unidade com dinâmico</span><span class="sxs-lookup"><span data-stu-id="b9b20-122">Unit testing with Dynamic</span></span>](#dynamic)
- [<span data-ttu-id="b9b20-123">Teste pelo tipo de unidade</span><span class="sxs-lookup"><span data-stu-id="b9b20-123">Unit testing by type</span></span>](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a><span data-ttu-id="b9b20-124">Testes de unidade com dinâmico</span><span class="sxs-lookup"><span data-stu-id="b9b20-124">Unit testing with Dynamic</span></span>

<span data-ttu-id="b9b20-125">Nesta seção, você adicionará um teste de unidade para o aplicativo criado no [tutorial de Introdução](../getting-started/tutorial-getting-started-with-signalr.md) usando um objeto dinâmico.</span><span class="sxs-lookup"><span data-stu-id="b9b20-125">In this section, you'll add a unit test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using a dynamic object.</span></span>

1. <span data-ttu-id="b9b20-126">Instalar o [extensão XUnit executor](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b9b20-126">Install the [XUnit Runner extension](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) for Visual Studio 2013.</span></span>
2. <span data-ttu-id="b9b20-127">Completar o [tutorial de Introdução](../getting-started/tutorial-getting-started-with-signalr.md), ou baixe o aplicativo concluído de [Galeria de códigos do MSDN](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span><span class="sxs-lookup"><span data-stu-id="b9b20-127">Either complete the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md), or download the completed application from [MSDN Code Gallery](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).</span></span>
3. <span data-ttu-id="b9b20-128">Se você estiver usando a versão de download do aplicativo Introdução, abra **Package Manager Console** e clique em **restaurar** para adicionar o pacote de SignalR ao projeto.</span><span class="sxs-lookup"><span data-stu-id="b9b20-128">If you are using the download version of the Getting Started application, open **Package Manager Console** and click **Restore** to add the SignalR package to the project.</span></span>

    ![Restaurar os pacotes](unit-testing-signalr-applications/_static/image1.png)
4. <span data-ttu-id="b9b20-130">Adicione um projeto à solução para o teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="b9b20-130">Add a project to the solution for the unit test.</span></span> <span data-ttu-id="b9b20-131">Clique com botão direito em sua solução de **Solution Explorer** e selecione **adicionar**, **novo projeto...** . Sob o **c#** nó, selecione o **Windows** nó.</span><span class="sxs-lookup"><span data-stu-id="b9b20-131">Right-click your solution in **Solution Explorer** and select **Add**, **New Project...**. Under the **C#** node, select the **Windows** node.</span></span> <span data-ttu-id="b9b20-132">Selecione **a biblioteca de classe**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-132">Select **Class Library**.</span></span> <span data-ttu-id="b9b20-133">Nomeie o novo projeto **TestLibrary** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-133">Name the new project **TestLibrary** and click **OK**.</span></span>

    ![Criar a biblioteca de teste](unit-testing-signalr-applications/_static/image2.png)
5. <span data-ttu-id="b9b20-135">Adicione uma referência no projeto de biblioteca de teste ao projeto SignalRChat.</span><span class="sxs-lookup"><span data-stu-id="b9b20-135">Add a reference in the test library project to the SignalRChat project.</span></span> <span data-ttu-id="b9b20-136">Clique com botão direito do **TestLibrary** do projeto e selecione **adicionar**, **referência...** . Selecione o **projetos** nó sob o **solução** nó e seleção **SignalRChat**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-136">Right-click the **TestLibrary** project and select **Add**, **Reference...**. Select the **Projects** node under the **Solution** node, and check **SignalRChat**.</span></span> <span data-ttu-id="b9b20-137">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-137">Click **OK**.</span></span>

    ![Adicionar referência de projeto](unit-testing-signalr-applications/_static/image3.png)
6. <span data-ttu-id="b9b20-139">Adicionar os pacotes SignalR, Moq e XUnit o **TestLibrary** projeto.</span><span class="sxs-lookup"><span data-stu-id="b9b20-139">Add the SignalR, Moq, and XUnit packages to the **TestLibrary** project.</span></span> <span data-ttu-id="b9b20-140">No **Package Manager Console**, defina o **projeto padrão** lista suspensa para **TestLibrary**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-140">In the **Package Manager Console**, set the **Default Project** dropdown to **TestLibrary**.</span></span> <span data-ttu-id="b9b20-141">Execute os comandos a seguir na janela do console:</span><span class="sxs-lookup"><span data-stu-id="b9b20-141">Run the following commands in the console window:</span></span>

    - `Install-Package Microsoft.AspNet.SignalR`
    - `Install-Package Moq`
    - `Install-Package XUnit`

    ![Instalar pacotes](unit-testing-signalr-applications/_static/image4.png)
7. <span data-ttu-id="b9b20-143">Crie o arquivo de teste.</span><span class="sxs-lookup"><span data-stu-id="b9b20-143">Create the test file.</span></span> <span data-ttu-id="b9b20-144">Clique com botão direito do **TestLibrary** do projeto e clique em **adicionar...** , **Classe**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-144">Right-click the **TestLibrary** project and click **Add...**, **Class**.</span></span> <span data-ttu-id="b9b20-145">Nomeie a nova classe **Tests.cs**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-145">Name the new class **Tests.cs**.</span></span>
8. <span data-ttu-id="b9b20-146">Substitua o conteúdo de Tests.cs com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9b20-146">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    <span data-ttu-id="b9b20-147">No código acima, um cliente de teste é criado usando o `Mock` de objeto o [Moq](https://github.com/Moq/moq4) biblioteca de tipo [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (2.1 SignalR, atribuir `dynamic` para o tipo parâmetro). O `IHubCallerConnectionContext` interface é o objeto de proxy com o qual você chamar métodos no cliente.</span><span class="sxs-lookup"><span data-stu-id="b9b20-147">In the code above, a test client is created using the `Mock` object from the [Moq](https://github.com/Moq/moq4) library, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span> <span data-ttu-id="b9b20-148">O `broadcastMessage` função é definida para o cliente fictício para que ele possa ser chamado `ChatHub` classe.</span><span class="sxs-lookup"><span data-stu-id="b9b20-148">The `broadcastMessage` function is then defined for the mock client so that it can be called by the `ChatHub` class.</span></span> <span data-ttu-id="b9b20-149">O mecanismo de teste, em seguida, chama o `Send` método o `ChatHub` classe, que por sua vez, chama o fictícios `broadcastMessage` função.</span><span class="sxs-lookup"><span data-stu-id="b9b20-149">The test engine then calls the `Send` method of the `ChatHub` class, which in turn calls the mocked `broadcastMessage` function.</span></span>
9. <span data-ttu-id="b9b20-150">Compile a solução pressionando **F6**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-150">Build the solution by pressing **F6**.</span></span>
10. <span data-ttu-id="b9b20-151">Execute o teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="b9b20-151">Run the unit test.</span></span> <span data-ttu-id="b9b20-152">No Visual Studio, selecione **teste**, **Windows**, **Gerenciador de testes**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-152">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="b9b20-153">Na janela do Gerenciador de testes, clique com botão direito **HubsAreMockableViaDynamic** e selecione **executar testes selecionados**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-153">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Gerenciador de Testes](unit-testing-signalr-applications/_static/image5.png)
11. <span data-ttu-id="b9b20-155">Verifique se que o teste foi bem-sucedido, verificando o painel inferior na janela do Gerenciador de testes.</span><span class="sxs-lookup"><span data-stu-id="b9b20-155">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="b9b20-156">A janela mostrará que o teste foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="b9b20-156">The window will show that the test passed.</span></span>

    ![Teste aprovado](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a><span data-ttu-id="b9b20-158">Teste pelo tipo de unidade</span><span class="sxs-lookup"><span data-stu-id="b9b20-158">Unit testing by type</span></span>

<span data-ttu-id="b9b20-159">Nesta seção, você adicionará um teste para o aplicativo criado no [tutorial de Introdução](../getting-started/tutorial-getting-started-with-signalr.md) usando uma interface que contém o método a ser testada.</span><span class="sxs-lookup"><span data-stu-id="b9b20-159">In this section, you'll add a test for the application created in the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md) using an interface that contains the method to be tested.</span></span>

1. <span data-ttu-id="b9b20-160">Conclua as etapas 1 a 7 no [testes de unidade com dinâmico](#dynamic) tutorial acima.</span><span class="sxs-lookup"><span data-stu-id="b9b20-160">Complete steps 1-7 in the [Unit testing with Dynamic](#dynamic) tutorial above.</span></span>
2. <span data-ttu-id="b9b20-161">Substitua o conteúdo de Tests.cs com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b9b20-161">Replace the contents of Tests.cs with the following code.</span></span>

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    <span data-ttu-id="b9b20-162">No código acima, uma interface é criada definindo a assinatura do `broadcastMessage` método para o qual o mecanismo de teste irá criar um cliente de simulação.</span><span class="sxs-lookup"><span data-stu-id="b9b20-162">In the code above, an interface is created defining the signature of the `broadcastMessage` method for which the test engine will create a mock client.</span></span> <span data-ttu-id="b9b20-163">Um cliente de simulação é criado usando o `Mock` objeto do tipo [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (2.1 SignalR, atribuir `dynamic` para o parâmetro de tipo.) O `IHubCallerConnectionContext` interface é o objeto de proxy com o qual você chamar métodos no cliente.</span><span class="sxs-lookup"><span data-stu-id="b9b20-163">A mock client is then created using the `Mock` object, of type [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) (in SignalR 2.1, assign `dynamic` for the type parameter.) The `IHubCallerConnectionContext` interface is the proxy object with which you invoke methods on the client.</span></span>

    <span data-ttu-id="b9b20-164">O teste, em seguida, cria uma instância de `ChatHub`e, em seguida, cria uma versão fictícia do `broadcastMessage` método, que por sua vez é invocado por chamar o `Send` método no hub.</span><span class="sxs-lookup"><span data-stu-id="b9b20-164">The test then creates an instance of `ChatHub`, and then creates a mock version of the `broadcastMessage` method, which in turn is invoked by calling the `Send` method on the hub.</span></span>
3. <span data-ttu-id="b9b20-165">Compile a solução pressionando **F6**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-165">Build the solution by pressing **F6**.</span></span>
4. <span data-ttu-id="b9b20-166">Execute o teste de unidade.</span><span class="sxs-lookup"><span data-stu-id="b9b20-166">Run the unit test.</span></span> <span data-ttu-id="b9b20-167">No Visual Studio, selecione **teste**, **Windows**, **Gerenciador de testes**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-167">In Visual Studio, select **Test**, **Windows**, **Test Explorer**.</span></span> <span data-ttu-id="b9b20-168">Na janela do Gerenciador de testes, clique com botão direito **HubsAreMockableViaDynamic** e selecione **executar testes selecionados**.</span><span class="sxs-lookup"><span data-stu-id="b9b20-168">In the Test Explorer window, right-click **HubsAreMockableViaDynamic** and select **Run Selected Tests**.</span></span>

    ![Gerenciador de Testes](unit-testing-signalr-applications/_static/image7.png)
5. <span data-ttu-id="b9b20-170">Verifique se que o teste foi bem-sucedido, verificando o painel inferior na janela do Gerenciador de testes.</span><span class="sxs-lookup"><span data-stu-id="b9b20-170">Verify that the test passed by checking the lower pane in the Test Explorer window.</span></span> <span data-ttu-id="b9b20-171">A janela mostrará que o teste foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="b9b20-171">The window will show that the test passed.</span></span>

    ![Teste aprovado](unit-testing-signalr-applications/_static/image8.png)