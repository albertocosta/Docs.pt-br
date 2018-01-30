---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: "Introdução ao ASP.NET Web API 2 (c#)"
author: MikeWasson
description: "HTTP não é apenas para serviços de páginas da web. Também é uma plataforma poderosa para a criação de APIs que expõem os dados e serviços. O HTTP é simples, flexível e ubiq..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/28/2017
ms.topic: article
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 6ff9fd279a03197f761454bba3f180d7428b1b1f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
<a name="getting-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="ee376-105">Introdução ao ASP.NET Web API 2 (c#)</span><span class="sxs-lookup"><span data-stu-id="ee376-105">Getting Started with ASP.NET Web API 2 (C#)</span></span>
====================
<span data-ttu-id="ee376-106">por [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ee376-106">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ee376-107">Baixe o projeto concluído</span><span class="sxs-lookup"><span data-stu-id="ee376-107">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="ee376-108">HTTP não é apenas para serviços de páginas da web.</span><span class="sxs-lookup"><span data-stu-id="ee376-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="ee376-109">HTTP também é uma plataforma poderosa para a criação de APIs que expõem os dados e serviços.</span><span class="sxs-lookup"><span data-stu-id="ee376-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="ee376-110">O HTTP é simples, flexível e de todos os lugares.</span><span class="sxs-lookup"><span data-stu-id="ee376-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="ee376-111">Praticamente qualquer plataforma que você pode pensar tem uma biblioteca HTTP para que serviços HTTP podem atingir uma ampla gama de clientes, incluindo navegadores, dispositivos móveis e aplicativos de área de trabalho tradicionais.</span><span class="sxs-lookup"><span data-stu-id="ee376-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>
 
<span data-ttu-id="ee376-112">API da Web do ASP.NET é uma estrutura para a criação de APIs na parte superior do .NET Framework da web.</span><span class="sxs-lookup"><span data-stu-id="ee376-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> <span data-ttu-id="ee376-113">Neste tutorial, você usará a API da Web do ASP.NET para criar uma web API que retorna uma lista de produtos.</span><span class="sxs-lookup"><span data-stu-id="ee376-113">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

 
 ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ee376-114">Versões de software usadas no tutorial</span><span class="sxs-lookup"><span data-stu-id="ee376-114">Software versions used in the tutorial</span></span>
  
 - [<span data-ttu-id="ee376-115">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ee376-115">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
 - <span data-ttu-id="ee376-116">Web API 2</span><span class="sxs-lookup"><span data-stu-id="ee376-116">Web API 2</span></span>

<span data-ttu-id="ee376-117">Consulte [criar uma API da web com o Visual Studio para Windows e o ASP.NET Core](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) para uma versão mais recente deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee376-117">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="ee376-118">Criar um projeto de API da Web</span><span class="sxs-lookup"><span data-stu-id="ee376-118">Create a Web API Project</span></span>

<span data-ttu-id="ee376-119">Neste tutorial, você usará a API da Web do ASP.NET para criar uma web API que retorna uma lista de produtos.</span><span class="sxs-lookup"><span data-stu-id="ee376-119">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="ee376-120">A página da web front-end usa jQuery para exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="ee376-120">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="ee376-121">Inicie o Visual Studio e selecione **novo projeto** do **iniciar** página.</span><span class="sxs-lookup"><span data-stu-id="ee376-121">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="ee376-122">Ou, do **arquivo** menu, selecione **novo** e **projeto**.</span><span class="sxs-lookup"><span data-stu-id="ee376-122">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="ee376-123">No **modelos** painel, selecione **modelos instalados** e expanda o **Visual C#** nó.</span><span class="sxs-lookup"><span data-stu-id="ee376-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="ee376-124">Em **Visual C#**, selecione **Web**.</span><span class="sxs-lookup"><span data-stu-id="ee376-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="ee376-125">Na lista de modelos de projeto, selecione **aplicativo Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="ee376-125">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="ee376-126">Nomeie o projeto "ProductsApp" e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ee376-126">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="ee376-127">No **novo projeto ASP.NET** caixa de diálogo, selecione o **vazio** modelo.</span><span class="sxs-lookup"><span data-stu-id="ee376-127">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="ee376-128">Em &quot;adicionar pastas e referências de núcleo&quot;, verifique **API da Web**.</span><span class="sxs-lookup"><span data-stu-id="ee376-128">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="ee376-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee376-129">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="ee376-130">Você também pode criar um projeto de API da Web usando o &quot;API da Web&quot; modelo.</span><span class="sxs-lookup"><span data-stu-id="ee376-130">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="ee376-131">O modelo de API da Web usa o ASP.NET MVC para fornecer páginas de Ajuda da API.</span><span class="sxs-lookup"><span data-stu-id="ee376-131">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="ee376-132">Estou usando o modelo vazio para este tutorial porque Mostrar API da Web sem MVC.</span><span class="sxs-lookup"><span data-stu-id="ee376-132">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="ee376-133">Em geral, você não precisa saber o ASP.NET MVC para usar a API da Web.</span><span class="sxs-lookup"><span data-stu-id="ee376-133">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>


## <a name="adding-a-model"></a><span data-ttu-id="ee376-134">Adicionando um modelo</span><span class="sxs-lookup"><span data-stu-id="ee376-134">Adding a Model</span></span>

<span data-ttu-id="ee376-135">Um *modelo* é um objeto que representa os dados em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee376-135">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="ee376-136">ASP.NET Web API pode serializar automaticamente seu modelo para outro formato, XML ou JSON e, em seguida, gravar os dados serializados no corpo da mensagem de resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="ee376-136">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="ee376-137">Como um cliente pode ler o formato de serialização, ele pode desserializar o objeto.</span><span class="sxs-lookup"><span data-stu-id="ee376-137">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="ee376-138">A maioria dos clientes pode analisar XML ou JSON.</span><span class="sxs-lookup"><span data-stu-id="ee376-138">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="ee376-139">Além disso, o cliente pode indicar que ele deseja definindo o cabeçalho Accept na mensagem de solicitação HTTP de formato.</span><span class="sxs-lookup"><span data-stu-id="ee376-139">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="ee376-140">Vamos começar criando um modelo simples que representa um produto.</span><span class="sxs-lookup"><span data-stu-id="ee376-140">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="ee376-141">Se o Gerenciador de soluções não estiver visível, clique no **exibição** menu e selecione **Gerenciador de soluções**.</span><span class="sxs-lookup"><span data-stu-id="ee376-141">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="ee376-142">No Gerenciador de soluções, clique na pasta de modelos.</span><span class="sxs-lookup"><span data-stu-id="ee376-142">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="ee376-143">No menu de contexto, selecione **adicionar** , em seguida, selecione **classe**.</span><span class="sxs-lookup"><span data-stu-id="ee376-143">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="ee376-144">Nomeie a classe &quot;produto&quot;.</span><span class="sxs-lookup"><span data-stu-id="ee376-144">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="ee376-145">Adicione as seguintes propriedades para o `Product` classe.</span><span class="sxs-lookup"><span data-stu-id="ee376-145">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="ee376-146">Adicionando um controlador</span><span class="sxs-lookup"><span data-stu-id="ee376-146">Adding a Controller</span></span>

<span data-ttu-id="ee376-147">Na API da Web, um *controlador* é um objeto que manipula as solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="ee376-147">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="ee376-148">Vamos adicionar um controlador que pode retornar uma lista de produtos ou um único produto especificado por ID.</span><span class="sxs-lookup"><span data-stu-id="ee376-148">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="ee376-149">Se você tiver usado o ASP.NET MVC, você já está familiarizados com os controladores.</span><span class="sxs-lookup"><span data-stu-id="ee376-149">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="ee376-150">Controladores de API da Web são semelhantes aos controladores MVC, mas herdam o **ApiController** classe o **controlador** classe.</span><span class="sxs-lookup"><span data-stu-id="ee376-150">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="ee376-151">Em **Solution Explorer**, clique na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="ee376-151">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="ee376-152">Selecione **adicionar** e, em seguida, selecione **controlador**.</span><span class="sxs-lookup"><span data-stu-id="ee376-152">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="ee376-153">No **adicionar Scaffold** caixa de diálogo, selecione **controlador de API da Web - vazio**.</span><span class="sxs-lookup"><span data-stu-id="ee376-153">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="ee376-154">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ee376-154">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="ee376-155">No **Adicionar controlador** caixa de diálogo, o nome do controlador &quot;ProductsController&quot;.</span><span class="sxs-lookup"><span data-stu-id="ee376-155">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="ee376-156">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ee376-156">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="ee376-157">O scaffolding cria um arquivo chamado ProductsController.cs na pasta controladores.</span><span class="sxs-lookup"><span data-stu-id="ee376-157">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="ee376-158">Não é necessário colocar os controladores em uma pasta chamada controladores.</span><span class="sxs-lookup"><span data-stu-id="ee376-158">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="ee376-159">O nome da pasta é apenas uma maneira conveniente de organizar seus arquivos de origem.</span><span class="sxs-lookup"><span data-stu-id="ee376-159">The folder name is just a convenient way to organize your source files.</span></span>


<span data-ttu-id="ee376-160">Se esse arquivo não estiver aberto, clique duas vezes no arquivo para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="ee376-160">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="ee376-161">Substitua o código neste arquivo com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ee376-161">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="ee376-162">Para manter o exemplo simples, os produtos são armazenados em uma matriz fixa dentro da classe do controlador.</span><span class="sxs-lookup"><span data-stu-id="ee376-162">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="ee376-163">É claro que, em um aplicativo real, você consulta um banco de dados ou usar outra fonte de dados externa.</span><span class="sxs-lookup"><span data-stu-id="ee376-163">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="ee376-164">O controlador define dois métodos que retornam produtos:</span><span class="sxs-lookup"><span data-stu-id="ee376-164">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="ee376-165">O `GetAllProducts` método retorna a lista completa de produtos como um **IEnumerable&lt;produto&gt;**  tipo.</span><span class="sxs-lookup"><span data-stu-id="ee376-165">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="ee376-166">O `GetProduct` método procura um único produto por sua ID.</span><span class="sxs-lookup"><span data-stu-id="ee376-166">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="ee376-167">É só isso!</span><span class="sxs-lookup"><span data-stu-id="ee376-167">That's it!</span></span> <span data-ttu-id="ee376-168">Você tem uma API da web do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ee376-168">You have a working web API.</span></span> <span data-ttu-id="ee376-169">Cada método do controlador corresponde a um ou mais URIs:</span><span class="sxs-lookup"><span data-stu-id="ee376-169">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="ee376-170">Método do controlador</span><span class="sxs-lookup"><span data-stu-id="ee376-170">Controller Method</span></span> | <span data-ttu-id="ee376-171">URI</span><span class="sxs-lookup"><span data-stu-id="ee376-171">URI</span></span> |
| --- | --- |
| <span data-ttu-id="ee376-172">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="ee376-172">GetAllProducts</span></span> | <span data-ttu-id="ee376-173">produtos/api /</span><span class="sxs-lookup"><span data-stu-id="ee376-173">/api/products</span></span> |
| <span data-ttu-id="ee376-174">GetProduct</span><span class="sxs-lookup"><span data-stu-id="ee376-174">GetProduct</span></span> | <span data-ttu-id="ee376-175">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="ee376-175">/api/products/*id*</span></span> |

<span data-ttu-id="ee376-176">Para o `GetProduct` método, o *id* no URI é um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="ee376-176">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="ee376-177">Por exemplo, para obter o produto com ID 5, o URI é `api/products/5`.</span><span class="sxs-lookup"><span data-stu-id="ee376-177">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="ee376-178">Para obter mais informações sobre como a API da Web encaminha solicitações HTTP para os métodos do controlador, consulte [roteamento na API da Web ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="ee376-178">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="ee376-179">Chamar a API da Web com Javascript e jQuery</span><span class="sxs-lookup"><span data-stu-id="ee376-179">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="ee376-180">Nesta seção, vamos adicionar uma página HTML que usa AJAX para chamar a API da web.</span><span class="sxs-lookup"><span data-stu-id="ee376-180">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="ee376-181">Vamos usar jQuery para fazer chamadas AJAX e também para atualizar a página com os resultados.</span><span class="sxs-lookup"><span data-stu-id="ee376-181">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="ee376-182">No Gerenciador de soluções, clique com o botão direito e selecione **adicionar**, em seguida, selecione **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="ee376-182">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="ee376-183">No **Adicionar Novo Item** caixa de diálogo, selecione o **Web** nó **Visual C#**e, em seguida, selecione o **página HTML** item.</span><span class="sxs-lookup"><span data-stu-id="ee376-183">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="ee376-184">Nomeie a página &quot;index.html&quot;.</span><span class="sxs-lookup"><span data-stu-id="ee376-184">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="ee376-185">Substitua tudo neste arquivo com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ee376-185">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="ee376-186">Há várias maneiras de obter jQuery.</span><span class="sxs-lookup"><span data-stu-id="ee376-186">There are several ways to get jQuery.</span></span> <span data-ttu-id="ee376-187">Neste exemplo, usei a [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee376-187">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="ee376-188">Você também pode baixá-lo do [http://jquery.com/](http://jquery.com/)e o ASP.NET "API Web" jQuery também inclui o modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="ee376-188">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="ee376-189">Obtendo uma lista de produtos</span><span class="sxs-lookup"><span data-stu-id="ee376-189">Getting a List of Products</span></span>

<span data-ttu-id="ee376-190">Para obter uma lista de produtos, envie uma solicitação HTTP GET para &quot;/api/produtos&quot;.</span><span class="sxs-lookup"><span data-stu-id="ee376-190">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="ee376-191">O jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) função envia uma solicitação AJAX.</span><span class="sxs-lookup"><span data-stu-id="ee376-191">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="ee376-192">Para a resposta contém uma matriz de objetos JSON.</span><span class="sxs-lookup"><span data-stu-id="ee376-192">For response contains array of JSON objects.</span></span> <span data-ttu-id="ee376-193">O `done` função especifica um retorno de chamada que é chamado quando a solicitação for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="ee376-193">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="ee376-194">O retorno de chamada, atualizamos o DOM com as informações de produto.</span><span class="sxs-lookup"><span data-stu-id="ee376-194">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="ee376-195">Um produto por ID</span><span class="sxs-lookup"><span data-stu-id="ee376-195">Getting a Product By ID</span></span>

<span data-ttu-id="ee376-196">Para obter um produto por ID, envie uma solicitação HTTP GET para &quot;/api/produtos/*id*&quot;, onde *id* é a ID do produto.</span><span class="sxs-lookup"><span data-stu-id="ee376-196">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="ee376-197">Chamamos ainda `getJSON` para enviar a solicitação AJAX, mas desta vez colocamos a ID no URI de solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee376-197">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="ee376-198">A resposta dessa solicitação é uma representação JSON de um único produto.</span><span class="sxs-lookup"><span data-stu-id="ee376-198">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="ee376-199">Executando o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee376-199">Running the Application</span></span>

<span data-ttu-id="ee376-200">Pressione F5 para iniciar a depuração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee376-200">Press F5 to start debugging the application.</span></span> <span data-ttu-id="ee376-201">A página da web deve parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ee376-201">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="ee376-202">Para obter um produto por ID, insira a ID e clique em Pesquisar:</span><span class="sxs-lookup"><span data-stu-id="ee376-202">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="ee376-203">Se você inserir uma ID inválida, o servidor retornará um erro HTTP:</span><span class="sxs-lookup"><span data-stu-id="ee376-203">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="ee376-204">Usando a tecla F12 para exibir a solicitação e resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="ee376-204">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="ee376-205">Quando você estiver trabalhando com um serviço HTTP, ele pode ser muito útil ver a solicitação HTTP e mensagens de solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee376-205">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="ee376-206">Você pode fazer isso usando as ferramentas de desenvolvedor F12 no Internet Explorer 9.</span><span class="sxs-lookup"><span data-stu-id="ee376-206">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="ee376-207">No Internet Explorer 9, pressione **F12** para abrir as ferramentas.</span><span class="sxs-lookup"><span data-stu-id="ee376-207">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="ee376-208">Clique o **rede** guia e pressione **iniciar captura**.</span><span class="sxs-lookup"><span data-stu-id="ee376-208">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="ee376-209">Agora vá para a página da web e pressione **F5** para recarregar a página da web.</span><span class="sxs-lookup"><span data-stu-id="ee376-209">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="ee376-210">Internet Explorer capturará o tráfego HTTP entre o navegador e o servidor web.</span><span class="sxs-lookup"><span data-stu-id="ee376-210">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="ee376-211">O modo de exibição de resumo mostra todo o tráfego de rede para uma página:</span><span class="sxs-lookup"><span data-stu-id="ee376-211">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="ee376-212">Localize a entrada para o URI relativo "api/produtos /".</span><span class="sxs-lookup"><span data-stu-id="ee376-212">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="ee376-213">Selecione esta opção e clique em **acesse a exibição detalhada**.</span><span class="sxs-lookup"><span data-stu-id="ee376-213">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="ee376-214">Na exibição detalhes, há guias para exibir os corpos e cabeçalhos de solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="ee376-214">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="ee376-215">Por exemplo, se você clicar no **cabeçalhos de solicitação** guia, você pode ver que o cliente solicitou &quot;aplicativo/json&quot; no cabeçalho Accept.</span><span class="sxs-lookup"><span data-stu-id="ee376-215">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="ee376-216">Se você clicar na guia de corpo de resposta, você pode ver como a lista de produtos foi serializada como JSON.</span><span class="sxs-lookup"><span data-stu-id="ee376-216">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="ee376-217">Outros navegadores têm funcionalidade semelhante.</span><span class="sxs-lookup"><span data-stu-id="ee376-217">Other browsers have similar functionality.</span></span> <span data-ttu-id="ee376-218">Outra ferramenta útil é [Fiddler](http://www.fiddler2.com/fiddler2/), um web proxy de depuração.</span><span class="sxs-lookup"><span data-stu-id="ee376-218">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="ee376-219">Você pode usar o Fiddler para exibir o tráfego HTTP e também para compor as solicitações HTTP, que lhe dá controle total sobre os cabeçalhos HTTP na solicitação.</span><span class="sxs-lookup"><span data-stu-id="ee376-219">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="ee376-220">Consulte este aplicativo em execução no Azure</span><span class="sxs-lookup"><span data-stu-id="ee376-220">See this App Running on Azure</span></span>

<span data-ttu-id="ee376-221">Você gostaria de ver o site concluído em execução como um aplicativo web em tempo real?</span><span class="sxs-lookup"><span data-stu-id="ee376-221">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="ee376-222">Você pode implantar uma versão completa do aplicativo para sua conta do Azure, clicando no botão a seguir.</span><span class="sxs-lookup"><span data-stu-id="ee376-222">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="ee376-223">Você precisa de uma conta do Azure para implantar essa solução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ee376-223">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="ee376-224">Se você não tiver uma conta, você tem as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="ee376-224">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="ee376-225">[Abra uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -você obtém créditos você pode usar para experimentar os serviços do Azure pagos e mesmo depois que eles são usados até que você pode manter a conta e livre de usar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee376-225">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="ee376-226">[Ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -assinatura do MSDN fornece créditos de cada mês em que você pode usar para os serviços do Azure pagos.</span><span class="sxs-lookup"><span data-stu-id="ee376-226">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee376-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee376-227">Next Steps</span></span>

- <span data-ttu-id="ee376-228">Para obter um exemplo mais completo de um serviço HTTP que dá suporte a ações de POST, PUT e DELETE e grava em um banco de dados, consulte [usando API Web 2 com o Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span><span class="sxs-lookup"><span data-stu-id="ee376-228">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="ee376-229">Para obter mais informações sobre como criar aplicativos web flexível e responsivo sobre um serviço HTTP, consulte [único aplicativo de página ASP.NET](../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="ee376-229">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="ee376-230">Para obter informações sobre como implantar um projeto da web do Visual Studio para o serviço de aplicativo do Azure, consulte [criar um aplicativo web ASP.NET no serviço de aplicativo do Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span><span class="sxs-lookup"><span data-stu-id="ee376-230">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>