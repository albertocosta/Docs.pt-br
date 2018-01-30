---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: "Configurando um TFS criar servidor de implantação da Web | Microsoft Docs"
author: jrjlee
description: "Este tópico descreve como preparar um servidor de compilação do Team Foundation Server (TFS) para criar e implantar suas soluções usando o Team Build e a Internet Informat..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: de31a9dffb95b863a4ec38b74fd2c6e03f287a7f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
<a name="configuring-a-tfs-build-server-for-web-deployment"></a><span data-ttu-id="c64f2-103">Configurando um servidor de compilação do TFS para implantação da Web</span><span class="sxs-lookup"><span data-stu-id="c64f2-103">Configuring a TFS Build Server for Web Deployment</span></span>
====================
<span data-ttu-id="c64f2-104">por [Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c64f2-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c64f2-105">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="c64f2-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c64f2-106">Este tópico descreve como preparar um servidor de compilação do Team Foundation Server (TFS) para criar e implantar suas soluções usando o Team Build e a ferramenta de implantação da Web de serviços de informações da Internet (IIS) (implantação da Web).</span><span class="sxs-lookup"><span data-stu-id="c64f2-106">This topic describes how to prepare a Team Foundation Server (TFS) build server to build and deploy your solutions using Team Build and the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>


<span data-ttu-id="c64f2-107">Este tópico faz parte de uma série de tutoriais com base em torno de requisitos de implantação corporativa de uma empresa fictícia chamada Fabrikam, Inc. Esta série de tutoriais usa uma solução de exemplo & #x 2014; o [solução Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; para representar um aplicativo web com um nível realista de complexidade, incluindo um aplicativo ASP.NET MVC 3, Windows Serviço do Communication Foundation (WCF) e um projeto de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c64f2-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="c64f2-108">O método de implantação no centro desses tutoriais baseia-se a abordagem de arquivo de projeto divisão descrita em [Noções básicas sobre o arquivo de projeto](../web-deployment-in-the-enterprise/understanding-the-project-file.md), em que o processo de compilação é controlado por dois arquivos & #x 2014; projeto contendo um crie instruções que se aplicam a todos os ambientes de destino e que contém configurações específicas ao ambiente de compilação e implantação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="c64f2-109">No momento da compilação, o arquivo de projeto específico do ambiente é mesclado no arquivo de projeto de ambiente independente para formar um conjunto completo de instruções de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c64f2-110">Visão geral da tarefa</span><span class="sxs-lookup"><span data-stu-id="c64f2-110">Task Overview</span></span>

<span data-ttu-id="c64f2-111">Para preparar um servidor de compilação para criar e implantar suas soluções, você precisará:</span><span class="sxs-lookup"><span data-stu-id="c64f2-111">To prepare a build server to build and deploy your solutions, you'll need to:</span></span>

- <span data-ttu-id="c64f2-112">Instalar e configurar o serviço de compilação do TFS.</span><span class="sxs-lookup"><span data-stu-id="c64f2-112">Install and configure the TFS build service.</span></span>
- <span data-ttu-id="c64f2-113">Instale o Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c64f2-113">Install Visual Studio 2010.</span></span>
- <span data-ttu-id="c64f2-114">Instale quaisquer produtos ou componentes que são necessárias para criar sua solução, como nas versões do .NET Framework ou do ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c64f2-114">Install any products or components that are required to build your solution, like versions of the .NET Framework or ASP.NET MVC.</span></span>
- <span data-ttu-id="c64f2-115">Instale a implantação da Web 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c64f2-115">Install Web Deploy 2.0 or later.</span></span>

<span data-ttu-id="c64f2-116">Neste tópico mostram como executar esses procedimentos ou apontar para outros recursos em que elas existem.</span><span class="sxs-lookup"><span data-stu-id="c64f2-116">This topic will show you how to perform these procedures or point to other resources where they exist.</span></span> <span data-ttu-id="c64f2-117">As tarefas e instruções passo a passo neste tópico supõem que:</span><span class="sxs-lookup"><span data-stu-id="c64f2-117">The tasks and walkthroughs in this topic assume that:</span></span>

- <span data-ttu-id="c64f2-118">Você está iniciando com uma compilação limpa de servidor executando o Windows Server 2008 R2 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="c64f2-118">You're starting with a clean server build running Windows Server 2008 R2 Service Pack 1.</span></span>
- <span data-ttu-id="c64f2-119">O servidor está ingressado no domínio com um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="c64f2-119">The server is domain-joined with a static IP address.</span></span>
- <span data-ttu-id="c64f2-120">Você instalou a camada de aplicativo do TFS em um servidor separado, conforme descrito em [implantação de Web corporativa: Visão geral do cenário](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c64f2-120">You've installed the TFS application tier on a separate server, as described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="c64f2-121">Quem executa esses procedimentos?</span><span class="sxs-lookup"><span data-stu-id="c64f2-121">Who Performs These Procedures?</span></span>

<span data-ttu-id="c64f2-122">Na maioria dos casos, um administrador do TFS será responsável por configurar servidores de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-122">In most cases, a TFS administrator will be responsible for configuring build servers.</span></span> <span data-ttu-id="c64f2-123">Em alguns casos, a equipe de desenvolvedores pode apropriar-se dos servidores de compilação específica.</span><span class="sxs-lookup"><span data-stu-id="c64f2-123">In some cases, the developer team may take ownership of specific build servers.</span></span>

## <a name="install-and-configure-the-tfs-build-service"></a><span data-ttu-id="c64f2-124">Instalar e configurar o serviço de compilação do TFS</span><span class="sxs-lookup"><span data-stu-id="c64f2-124">Install and Configure the TFS Build Service</span></span>

<span data-ttu-id="c64f2-125">Quando você configura um servidor de compilação, a primeira tarefa é instalar e configurar o serviço de compilação do TFS.</span><span class="sxs-lookup"><span data-stu-id="c64f2-125">When you configure a build server, your first task is to install and configure the TFS build service.</span></span> <span data-ttu-id="c64f2-126">Como parte desse processo, você precisará:</span><span class="sxs-lookup"><span data-stu-id="c64f2-126">As part of this process, you'll need to:</span></span>

- <span data-ttu-id="c64f2-127">Instale o serviço de compilação do TFS e configure uma conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="c64f2-127">Install the TFS build service and configure a service account.</span></span> <span data-ttu-id="c64f2-128">As tarefas de compilação, incluindo a implantação, serão executado usando a identidade da conta de serviço de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-128">Any build tasks, including deployment, will run using the identity of the build service account.</span></span>
- <span data-ttu-id="c64f2-129">Criar um *controlador de compilação* e um ou mais *agentes de compilação*.</span><span class="sxs-lookup"><span data-stu-id="c64f2-129">Create a *build controller* and one or more *build agents*.</span></span> <span data-ttu-id="c64f2-130">Cada controlador de compilação gerencia um conjunto de agentes de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-130">Each build controller manages a set of build agents.</span></span> <span data-ttu-id="c64f2-131">Quando você enfileirar uma compilação, o controlador de compilação atribui a tarefa de compilação para um agente de compilação disponível.</span><span class="sxs-lookup"><span data-stu-id="c64f2-131">When you queue a build, the build controller assigns the build task to an available build agent.</span></span> <span data-ttu-id="c64f2-132">Cada coleção de projetos de equipe no TFS é mapeada para um controlador de compilação único.</span><span class="sxs-lookup"><span data-stu-id="c64f2-132">Each team project collection in TFS is mapped to a single build controller.</span></span>
- <span data-ttu-id="c64f2-133">Configure uma pasta-depósito para suas saídas de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-133">Configure a drop folder for your build outputs.</span></span> <span data-ttu-id="c64f2-134">Este é um compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="c64f2-134">This is a network share.</span></span> <span data-ttu-id="c64f2-135">Qualquer saídas, como pacotes de implantação da web de compilação, são enviadas para a pasta-depósito.</span><span class="sxs-lookup"><span data-stu-id="c64f2-135">Any build outputs, like web deployment packages, are sent to the drop folder.</span></span>

<span data-ttu-id="c64f2-136">O [administrando o Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) capítulo no MSDN contém todos os recursos que você precisa para executar estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="c64f2-136">The [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) chapter on MSDN contains all the resources you need in order to perform these tasks:</span></span>

- <span data-ttu-id="c64f2-137">Para obter uma visão geral conceitual do Team Foundation Build, incluindo o serviço de compilação, compilação controladores e agentes de compilação, consulte [Noções básicas sobre um sistema de compilação do Team Foundation](https://msdn.microsoft.com/library/dd793166.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-137">For a conceptual overview of Team Foundation Build, including the build service, build controllers, and build agents, see [Understanding a Team Foundation Build System](https://msdn.microsoft.com/library/dd793166.aspx).</span></span>
- <span data-ttu-id="c64f2-138">Para obter informações sobre como instalar e configurar o serviço de compilação, consulte [configurar uma máquina de compilação](https://msdn.microsoft.com/library/ms181712.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-138">For information on installing and configuring the build service, see [Configure a Build Machine](https://msdn.microsoft.com/library/ms181712.aspx).</span></span>
- <span data-ttu-id="c64f2-139">Para obter informações sobre a criação de controladores de compilação, consulte [criar e trabalhar com um controlador de compilação](https://msdn.microsoft.com/library/ee330987.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-139">For information on creating build controllers, see [Create and Work with a Build Controller](https://msdn.microsoft.com/library/ee330987.aspx).</span></span>
- <span data-ttu-id="c64f2-140">Para obter informações sobre a criação de agentes de compilação, consulte [criar e trabalhar com os agentes de compilação](https://msdn.microsoft.com/library/bb399135.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-140">For information on creating build agents, see [Create and Work with Build Agents](https://msdn.microsoft.com/library/bb399135.aspx).</span></span>
- <span data-ttu-id="c64f2-141">Para obter informações sobre como criar e configurar pastas depósitos, consulte [definir pastas de Drop](https://msdn.microsoft.com/library/bb778394.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-141">For information on creating and configuring drop folders, see [Set Up Drop Folders](https://msdn.microsoft.com/library/bb778394.aspx).</span></span>

## <a name="install-required-products-and-components"></a><span data-ttu-id="c64f2-142">Instalar produtos necessários e componentes</span><span class="sxs-lookup"><span data-stu-id="c64f2-142">Install Required Products and Components</span></span>

<span data-ttu-id="c64f2-143">Para habilitar o servidor de compilação criar soluções, você deve instalar qualquer produtos, componentes ou assemblies que sua solução exige.</span><span class="sxs-lookup"><span data-stu-id="c64f2-143">To enable the build server to build your solutions, you must install any products, components, or assemblies that your solution requires.</span></span> <span data-ttu-id="c64f2-144">Antes de instalar os componentes de plataforma da web, você deve instalar o Visual Studio 2010 (qualquer versão) no servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-144">Before you install any web platform components, you should install Visual Studio 2010 (any version) on the build server.</span></span> <span data-ttu-id="c64f2-145">Isso garante que os principais arquivos de destino Microsoft Build Engine (MSBuild) e os arquivos de destino do Pipeline de publicação (WPP) de Web estão disponíveis para o serviço de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-145">This ensures that the core Microsoft Build Engine (MSBuild) target files and the Web Publishing Pipeline (WPP) target files are available to the build service.</span></span> <span data-ttu-id="c64f2-146">O instalador do Visual Studio também deve instalar a implantação da Web, você precisará se você planeja implantar pacotes da web como parte do processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-146">The Visual Studio installer should also install Web Deploy, which you'll need if you plan to deploy web packages as part of your build process.</span></span>

<span data-ttu-id="c64f2-147">A melhor maneira de instalar componentes de plataforma da web comum é usar o [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="c64f2-147">The best way to install common web platform components is to use the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span> <span data-ttu-id="c64f2-148">Isso garante que você está instalando a versão mais recente de cada produto, e também automaticamente detecta e instala todos os pré-requisitos para cada produto.</span><span class="sxs-lookup"><span data-stu-id="c64f2-148">This ensures that you're installing the latest version of each product, and it also automatically detects and installs any prerequisites for each product.</span></span> <span data-ttu-id="c64f2-149">No caso do [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solução, você deve usar o Web Platform Installer para instalar esses produtos e componentes:</span><span class="sxs-lookup"><span data-stu-id="c64f2-149">In the case of the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution, you should use the Web Platform Installer to install these products and components:</span></span>

- <span data-ttu-id="c64f2-150">**.NET Framework 4.0**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-150">**.NET Framework 4.0**.</span></span> <span data-ttu-id="c64f2-151">Isso é necessário para executar aplicativos que foram criados com esta versão do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="c64f2-151">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="c64f2-152">**Web Deployment Tool 2.1 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-152">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="c64f2-153">Isso instala a implantação da Web (e seu executável subjacente, MSDeploy.exe) em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="c64f2-153">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="c64f2-154">Como parte desse processo, ele instala e inicia o serviço de agente de implantação da Web.</span><span class="sxs-lookup"><span data-stu-id="c64f2-154">As part of this process, it installs and starts the Web Deployment Agent Service.</span></span> <span data-ttu-id="c64f2-155">Esse serviço permite que você implante pacotes da web de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="c64f2-155">This service lets you deploy web packages from a remote computer.</span></span>
- <span data-ttu-id="c64f2-156">**ASP.NET MVC 3**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-156">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="c64f2-157">Isso instala os assemblies que você precisa executar aplicativos ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="c64f2-157">This installs the assemblies you need to run ASP.NET MVC 3 applications.</span></span>

<span data-ttu-id="c64f2-158">**Para instalar os componentes e produtos necessários**</span><span class="sxs-lookup"><span data-stu-id="c64f2-158">**To install the required products and components**</span></span>

1. <span data-ttu-id="c64f2-159">Instale o Visual Studio 2010.</span><span class="sxs-lookup"><span data-stu-id="c64f2-159">Install Visual Studio 2010.</span></span> <span data-ttu-id="c64f2-160">Quando solicitado a selecionar os recursos a serem instalados, você deve incluir:</span><span class="sxs-lookup"><span data-stu-id="c64f2-160">When prompted to select features to install, you should include:</span></span>

    1. <span data-ttu-id="c64f2-161">Linguagens de programação que você precisa compilar.</span><span class="sxs-lookup"><span data-stu-id="c64f2-161">Any programming languages that you need to compile.</span></span>
    2. <span data-ttu-id="c64f2-162">Visual Web Developer.</span><span class="sxs-lookup"><span data-stu-id="c64f2-162">Visual Web Developer.</span></span> <span data-ttu-id="c64f2-163">Isso garante que os destinos WPP são adicionados ao seu servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-163">This ensures that the WPP targets are added to your build server.</span></span>

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. <span data-ttu-id="c64f2-164">Quando a instalação do Visual Studio 2010 for concluída, baixe e instale [Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (se ainda não estiver incluído na mídia de instalação).</span><span class="sxs-lookup"><span data-stu-id="c64f2-164">When the installation of Visual Studio 2010 is complete, download and install [Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (if it's not already included in your installation media).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c64f2-165">Visual Studio 2010 Service Pack 1 resolve um erro que pode impedir a localizar o executável do MSDeploy do MSBuild.</span><span class="sxs-lookup"><span data-stu-id="c64f2-165">Visual Studio 2010 Service Pack 1 resolves a bug that can prevent MSBuild from locating the MSDeploy executable.</span></span>
3. <span data-ttu-id="c64f2-166">Baixe e inicie o [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span><span class="sxs-lookup"><span data-stu-id="c64f2-166">Download and launch the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
4. <span data-ttu-id="c64f2-167">Na parte superior do **Web Platform Installer 3.0** janela, clique em **produtos**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-167">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
5. <span data-ttu-id="c64f2-168">No lado esquerdo da janela, no painel de navegação, clique em **estruturas**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-168">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
6. <span data-ttu-id="c64f2-169">No **Microsoft .NET Framework 4** de linha, se o .NET Framework já não estiver instalado, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-169">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c64f2-170">Você já pode ter instalado o .NET Framework 4.0 através do Windows Update.</span><span class="sxs-lookup"><span data-stu-id="c64f2-170">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="c64f2-171">Se um produto ou componente já está instalado, o Web Platform Installer indicará isso substituindo o **adicionar** botão com o texto **instalado**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-171">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. <span data-ttu-id="c64f2-172">No **ASP.NET MVC 3 (Visual Studio 2010)** de linha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-172">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
8. <span data-ttu-id="c64f2-173">No painel de navegação, clique em **Server**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-173">In the navigation pane, click **Server**.</span></span>
9. <span data-ttu-id="c64f2-174">No **ferramenta de implantação da Web 2.1** de linha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-174">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="c64f2-175">Clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-175">Click **Install**.</span></span> <span data-ttu-id="c64f2-176">O Web Platform Installer mostrará uma lista de produtos & #x 2014; juntamente com quaisquer dependências associadas & #x 2014; a serem instalados e solicitará que você aceite os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="c64f2-176">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>
11. <span data-ttu-id="c64f2-177">Leia os termos de licença e se você concordar com os termos, clique em **aceito**.</span><span class="sxs-lookup"><span data-stu-id="c64f2-177">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="c64f2-178">Quando a instalação for concluída, clique em **concluir**e, em seguida, feche o **Web Platform Installer 3.0** janela.</span><span class="sxs-lookup"><span data-stu-id="c64f2-178">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

> [!NOTE]
> <span data-ttu-id="c64f2-179">Se o processo de implantação inclui o uso de ferramentas como VSDBCMD.exe ou SQLCMD.exe, você precisará garantir que eles são instalados no seu servidor de compilação.</span><span class="sxs-lookup"><span data-stu-id="c64f2-179">If your deployment process includes the use of tools like VSDBCMD.exe or SQLCMD.exe, you'll need to ensure that these are installed on your build server.</span></span> <span data-ttu-id="c64f2-180">VSDBCMD.exe é uma ferramenta do Visual Studio e normalmente é adicionada ao servidor quando você instalar o Team Foundation Build.</span><span class="sxs-lookup"><span data-stu-id="c64f2-180">VSDBCMD.exe is a Visual Studio tool and is typically added to the server when you install Team Foundation Build.</span></span> <span data-ttu-id="c64f2-181">SQLCMD.exe é uma ferramenta do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c64f2-181">SQLCMD.exe is a SQL Server tool.</span></span> <span data-ttu-id="c64f2-182">Você pode baixar uma versão autônoma do SQLCMD.exe do [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) página.</span><span class="sxs-lookup"><span data-stu-id="c64f2-182">You can download a stand-alone version of SQLCMD.exe from the [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) page.</span></span>


## <a name="conclusion"></a><span data-ttu-id="c64f2-183">Conclusão</span><span class="sxs-lookup"><span data-stu-id="c64f2-183">Conclusion</span></span>

<span data-ttu-id="c64f2-184">Neste ponto, seu servidor de compilação está pronto para começar a criar e implantar seus projetos de aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="c64f2-184">At this point, your build server is ready to start building and deploying your web application projects.</span></span> <span data-ttu-id="c64f2-185">O próximo tópico, [criar uma implantação de dá suporte a que definição de compilação](creating-a-build-definition-that-supports-deployment.md), descreve como criar e configurar uma definição de compilação para controlar quando e como os projetos são criados e implantados.</span><span class="sxs-lookup"><span data-stu-id="c64f2-185">The next topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md), describes how to create and configure a build definition to control when and how your projects are built and deployed.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c64f2-186">Leitura adicional</span><span class="sxs-lookup"><span data-stu-id="c64f2-186">Further Reading</span></span>

<span data-ttu-id="c64f2-187">Para obter orientação geral sobre como trabalhar com o Team Build, consulte [administrando o Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).</span><span class="sxs-lookup"><span data-stu-id="c64f2-187">For more general guidance on working with Team Build, see [Administering Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c64f2-188">[Anterior](adding-content-to-source-control.md)
[Próximo](creating-a-build-definition-that-supports-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="c64f2-188">[Previous](adding-content-to-source-control.md)
[Next](creating-a-build-definition-that-supports-deployment.md)</span></span>