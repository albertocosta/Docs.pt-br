---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Single Sign-On (Criando aplicativos de nuvem do mundo Real com o Azure) | Microsoft Docs
author: MikeWasson
description: "Os aplicativos de nuvem criando Real World com livro eletrônico do Azure baseia-se em uma apresentação desenvolvida por Scott Guthrie. Ele explica 13 padrões e práticas recomendadas que ele..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: b3640c94a8ae9ede330c0fe6a392acb5843cb65c
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
<a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="c9f02-104">Logon único (Criando aplicativos de nuvem do mundo Real com o Azure)</span><span class="sxs-lookup"><span data-stu-id="c9f02-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="c9f02-105">por [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c9f02-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="c9f02-106">[Download corrigi-lo projeto](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) ou [baixar livro eletrônico](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9f02-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="c9f02-107">O **nuvem aplicativos do mundo Real criando com o Azure** livro eletrônico baseia-se em uma apresentação desenvolvida por Scott Guthrie.</span><span class="sxs-lookup"><span data-stu-id="c9f02-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="c9f02-108">Explica as 13 padrões e práticas que podem ajudá-lo a ser bem-sucedido de desenvolvimento de aplicativos da web para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="c9f02-109">Para obter informações sobre o livro eletrônico, consulte [primeiro capítulo](introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9f02-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="c9f02-110">Há muitos problemas de segurança de pensar sobre quando você estiver desenvolvendo um aplicativo de nuvem, mas para esta série nos concentraremos em um: o logon único.</span><span class="sxs-lookup"><span data-stu-id="c9f02-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="c9f02-111">Pessoas pergunta frequentemente perguntam é: "Estou principalmente criando aplicativos para os funcionários da minha empresa; como hospedar esses aplicativos na nuvem e ainda permitir que eles usam o mesmo modelo de segurança que Meus funcionários conhece e usam no ambiente local quando estiver executando aplicativos que são hospedados dentro do firewall?"</span><span class="sxs-lookup"><span data-stu-id="c9f02-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="c9f02-112">Uma das maneiras que podemos habilitar este cenário é chamada do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c9f02-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c9f02-113">AD do Azure permite que você disponibilizar enterprise linha de negócios (LOB) aplicativos pela Internet, e permite que você disponibilizar esses aplicativos para parceiros de negócios.</span><span class="sxs-lookup"><span data-stu-id="c9f02-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="c9f02-114">Introdução ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9f02-114">Introduction to Azure AD</span></span>

<span data-ttu-id="c9f02-115">[O AD do Azure](https://docs.microsoft.com/azure/active-directory/) fornece [do Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="c9f02-116">Os principais recursos incluem o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c9f02-116">Key features include the following:</span></span>

- <span data-ttu-id="c9f02-117">Ele se integra ao Active Directory no local.</span><span class="sxs-lookup"><span data-stu-id="c9f02-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="c9f02-118">Ele permite o logon único com seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c9f02-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="c9f02-119">Ele oferece suporte a padrões abertos como [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), e [OAuth 2.0](http://oauth.net/2/).</span><span class="sxs-lookup"><span data-stu-id="c9f02-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="c9f02-120">Ele dá suporte a Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9f02-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="c9f02-121">Suponha que você tenha um ambiente do Active Directory do Windows Server no local que você usa para habilitar os funcionários entrar aplicativos de Intranet:</span><span class="sxs-lookup"><span data-stu-id="c9f02-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="c9f02-122">O que o AD do Azure permite fazer é criar um diretório na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="c9f02-123">É um recurso gratuito e fácil de configurar.</span><span class="sxs-lookup"><span data-stu-id="c9f02-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="c9f02-124">Ele pode ser totalmente independente do seu local no Active Directory. Você pode colocar qualquer pessoa que você deseja nele e autenticá-los em aplicativos da Internet.</span><span class="sxs-lookup"><span data-stu-id="c9f02-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="c9f02-126">Ou você pode integrar suas instalações AD.</span><span class="sxs-lookup"><span data-stu-id="c9f02-126">Or you can integrate it with your on-premises AD.</span></span>

![AD e a integração do WAAD](single-sign-on/_static/image3.png)

<span data-ttu-id="c9f02-128">Agora todos os funcionários que podem autenticar local também podem autenticar através da Internet – sem a necessidade de abrir um firewall ou implantar novos servidores no seu data center.</span><span class="sxs-lookup"><span data-stu-id="c9f02-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="c9f02-129">Você pode continuar a utilizar todos os o ambiente existente do Active Directory que você conhece e usa atualmente para fornecer seus aplicativos internos logon único no recurso.</span><span class="sxs-lookup"><span data-stu-id="c9f02-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="c9f02-130">Depois que você fez essa conexão entre o AD e o AD do Azure, você também pode habilitar seus aplicativos web e seus dispositivos móveis para autenticar os funcionários na nuvem e você pode habilitar aplicativos de terceiros, como o Office 365, o SalesForce.com ou o Google apps, para aceitar o credenciais de funcionários.</span><span class="sxs-lookup"><span data-stu-id="c9f02-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="c9f02-131">Se você estiver usando o Office 365, você está já configurado com o AD do Azure como o Office 365 usa o AD do Azure para autenticação e autorização.</span><span class="sxs-lookup"><span data-stu-id="c9f02-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![3º aplicativos de terceiros](single-sign-on/_static/image4.png)

<span data-ttu-id="c9f02-133">A vantagem dessa abordagem é que, quando sua organização adiciona ou exclui um usuário ou um usuário altera uma senha, use o mesmo processo que você usa atualmente no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="c9f02-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="c9f02-134">Todos os das suas instalações AD alterações são propagadas automaticamente para o ambiente de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="c9f02-135">Se sua empresa está usando ou mover para o Office 365, a boa notícia é que você terá de configurar automaticamente como o Office 365 usa o AD do Azure para autenticação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f02-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="c9f02-136">Portanto, você pode usar facilmente em seus próprios aplicativos de autenticação mesmo que usa o Office 365.</span><span class="sxs-lookup"><span data-stu-id="c9f02-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="c9f02-137">Configurar um locatário do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9f02-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="c9f02-138">um diretório do AD do Azure é chamado um AD do Azure [locatário](https://technet.microsoft.com/library/jj573650.aspx), e é muito fácil configurar um locatário.</span><span class="sxs-lookup"><span data-stu-id="c9f02-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="c9f02-139">Vamos mostrar como é feito no Portal de gerenciamento do Azure para ilustrar os conceitos, mas claro como as outras funções portais você também pode fazê-lo usando um script ou uma API de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="c9f02-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="c9f02-140">No portal de gerenciamento, clique na guia do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c9f02-140">In the management portal click the Active Directory tab.</span></span>

![WAAD no portal](single-sign-on/_static/image5.png)

<span data-ttu-id="c9f02-142">Você automaticamente tem um locatário do AD do Azure para sua conta do Azure, e você pode clicar no **adicionar** botão na parte inferior da página para criar diretórios adicionais.</span><span class="sxs-lookup"><span data-stu-id="c9f02-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="c9f02-143">Talvez você queira um para um ambiente de teste e outro para produção, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="c9f02-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="c9f02-144">Pense cuidadosamente sobre o que você nomear um novo diretório.</span><span class="sxs-lookup"><span data-stu-id="c9f02-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="c9f02-145">Se você usar seu nome para o diretório e, em seguida, você pode usar o nome novamente para um dos usuários, que podem ser confusas.</span><span class="sxs-lookup"><span data-stu-id="c9f02-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![Adicionar diretório](single-sign-on/_static/image6.png)

<span data-ttu-id="c9f02-147">O portal tem suporte completo para criar, excluir e gerenciar os usuários nesse ambiente.</span><span class="sxs-lookup"><span data-stu-id="c9f02-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="c9f02-148">Por exemplo, para adicionar um usuário acesse o **usuários** guia e clique no **adicionar usuário** botão.</span><span class="sxs-lookup"><span data-stu-id="c9f02-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![Botão Adicionar usuário](single-sign-on/_static/image7.png)

![Adicionar caixa de diálogo do usuário](single-sign-on/_static/image8.png)

<span data-ttu-id="c9f02-151">Você pode criar um novo usuário que existe somente nesse diretório, ou você pode registrar uma Account da Microsoft como um usuário nesse diretório, ou o registro ou um usuário de outro diretório do AD do Azure como um usuário neste diretório.</span><span class="sxs-lookup"><span data-stu-id="c9f02-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="c9f02-152">(Em um diretório real, o domínio padrão seria ContosoTest.onmicrosoft.com. Você também pode usar um domínio de sua escolha, como contoso.com.)</span><span class="sxs-lookup"><span data-stu-id="c9f02-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com. You can also use a domain of your own choosing, like contoso.com.)</span></span>

![Tipos de usuário](single-sign-on/_static/image9.png)

![Adicionar caixa de diálogo do usuário](single-sign-on/_static/image10.png)

<span data-ttu-id="c9f02-155">Você pode atribuir o usuário a uma função.</span><span class="sxs-lookup"><span data-stu-id="c9f02-155">You can assign the user to a role.</span></span>

![Perfil de usuário](single-sign-on/_static/image11.png)

<span data-ttu-id="c9f02-157">E a conta é criada com uma senha temporária.</span><span class="sxs-lookup"><span data-stu-id="c9f02-157">And the account is created with a temporary password.</span></span>

![Senha temporária](single-sign-on/_static/image12.png)

<span data-ttu-id="c9f02-159">Os usuários que você criar dessa maneira imediatamente podem fazer logon para seus aplicativos web usando este diretório na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-159">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="c9f02-160">O que é excelente de enterprise single sign-on, no entanto, é o **integração de diretórios** guia:</span><span class="sxs-lookup"><span data-stu-id="c9f02-160">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![Guia de integração de diretório](single-sign-on/_static/image13.png)

<span data-ttu-id="c9f02-162">Se você habilitar a integração de diretório e [Baixe uma ferramenta](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), você pode sincronizar esse diretório na nuvem com o existente no Active Directory local que você já estiver usando dentro da sua organização.</span><span class="sxs-lookup"><span data-stu-id="c9f02-162">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="c9f02-163">Em seguida, todos os usuários armazenados em seu diretório aparecerá nesse diretório de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-163">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="c9f02-164">Seus aplicativos de nuvem agora podem se autenticar todos os seus funcionários usando suas credenciais do Active Directory existentes.</span><span class="sxs-lookup"><span data-stu-id="c9f02-164">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="c9f02-165">E tudo isso é livre – a ferramenta de sincronização e o Azure AD em si.</span><span class="sxs-lookup"><span data-stu-id="c9f02-165">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="c9f02-166">A ferramenta é um assistente que é fácil de usar, como você pode ver essas capturas de tela.</span><span class="sxs-lookup"><span data-stu-id="c9f02-166">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="c9f02-167">Eles não são instruções completas, apenas um exemplo mostrando o processo básico.</span><span class="sxs-lookup"><span data-stu-id="c9f02-167">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="c9f02-168">Para obter mais informações de how-a--it, consulte os links a [recursos](#resources) seção no final deste capítulo.</span><span class="sxs-lookup"><span data-stu-id="c9f02-168">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image14.png)

<span data-ttu-id="c9f02-170">Clique em **próximo**e, em seguida, insira suas credenciais do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f02-170">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image15.png)

<span data-ttu-id="c9f02-172">Clique em **próximo**e, em seguida, insira seu local as credenciais do AD.</span><span class="sxs-lookup"><span data-stu-id="c9f02-172">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image16.png)

<span data-ttu-id="c9f02-174">Clique em **próximo**e, em seguida, indique se você deseja armazenar um hash de suas senhas do AD na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-174">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image17.png)

<span data-ttu-id="c9f02-176">O hash de senha que você pode armazenar na nuvem é um hash unidirecional; as senhas reais nunca são armazenadas no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f02-176">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="c9f02-177">Se você decidir armazenar hashes na nuvem, você terá que usar [os serviços de Federação do Active Directory](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span><span class="sxs-lookup"><span data-stu-id="c9f02-177">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="c9f02-178">Também há [outros fatores a considerar ao escolher se deseja ou não usar o ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9f02-178">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="c9f02-179">A opção AD FS requer algumas etapas de configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="c9f02-179">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="c9f02-180">Se você optar por armazenar hashes na nuvem, terminar e a ferramenta inicia a sincronização de diretórios quando você clica em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c9f02-180">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image18.png)

<span data-ttu-id="c9f02-182">E, em alguns minutos terminar.</span><span class="sxs-lookup"><span data-stu-id="c9f02-182">And in a few minutes you're done.</span></span>

![Assistente de configuração da ferramenta de sincronização de WAAD](single-sign-on/_static/image19.png)

<span data-ttu-id="c9f02-184">Você só precisa executar isso em um controlador de domínio da empresa, no Windows 2003 ou superior.</span><span class="sxs-lookup"><span data-stu-id="c9f02-184">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="c9f02-185">E nenhuma reinicialização é necessária.</span><span class="sxs-lookup"><span data-stu-id="c9f02-185">And no need to reboot.</span></span> <span data-ttu-id="c9f02-186">Quando terminar, todos os seus usuários estão na nuvem e você pode fazer logon único de qualquer web ou aplicativo móvel, usando SAML, OAuth ou WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="c9f02-186">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="c9f02-187">Às vezes, fazemos sobre o nível de segurança, isso é – Microsoft usá-lo para seus próprios dados confidenciais da empresa?</span><span class="sxs-lookup"><span data-stu-id="c9f02-187">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="c9f02-188">E a resposta for Sim, que podemos fazer.</span><span class="sxs-lookup"><span data-stu-id="c9f02-188">And the answer is yes we do.</span></span> <span data-ttu-id="c9f02-189">Por exemplo, se você for para o site do Microsoft SharePoint interno no [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), for solicitado a fazer logon.</span><span class="sxs-lookup"><span data-stu-id="c9f02-189">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Entrar no Office 365](single-sign-on/_static/image20.png)

<span data-ttu-id="c9f02-191">Microsoft habilitou o ADFS, portanto, quando você inserir uma ID da Microsoft, você é redirecionado para uma página de logon do ADFS.</span><span class="sxs-lookup"><span data-stu-id="c9f02-191">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![Entrada do AD FS](single-sign-on/_static/image21.png)

<span data-ttu-id="c9f02-193">E, depois que você insere as credenciais armazenadas em uma conta interna do AD do Microsoft, você tem acesso a esse aplicativo interno.</span><span class="sxs-lookup"><span data-stu-id="c9f02-193">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![Site do SharePoint MS](single-sign-on/_static/image22.png)

<span data-ttu-id="c9f02-195">Estamos usando um servidor de entrada do AD principalmente porque já tínhamos ADFS configurar antes do AD do Azure se tornou disponível, mas o processo de log é feito por meio de um diretório do AD do Azure na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-195">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="c9f02-196">Podemos colocar nossos documentos importantes, controle de origem, arquivos de gerenciamento de desempenho, relatórios de vendas e muito mais na nuvem e está usando essa mesma solução exata para protegê-los.</span><span class="sxs-lookup"><span data-stu-id="c9f02-196">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="c9f02-197">Criar um aplicativo ASP.NET que usa o AD do Azure para logon único</span><span class="sxs-lookup"><span data-stu-id="c9f02-197">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="c9f02-198">Visual Studio torna fácil criar um aplicativo que usa o AD do Azure para logon único, como você pode ver algumas capturas de tela.</span><span class="sxs-lookup"><span data-stu-id="c9f02-198">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="c9f02-199">Quando você cria um novo aplicativo ASP.NET, MVC ou Web Forms, o método de autenticação padrão é a identidade do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9f02-199">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="c9f02-200">Para alterá-la para o AD do Azure, clique em uma **alterar autenticação** botão.</span><span class="sxs-lookup"><span data-stu-id="c9f02-200">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![Alterar autenticação](single-sign-on/_static/image23.png)

<span data-ttu-id="c9f02-202">Selecione as contas organizacionais, insira seu nome de domínio e, em seguida, selecionar o logon único.</span><span class="sxs-lookup"><span data-stu-id="c9f02-202">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![Configurar a caixa de diálogo de autenticação](single-sign-on/_static/image24.png)

<span data-ttu-id="c9f02-204">Também pode dar a aplicativo de leitura ou leitura/gravação permissão para dados de diretório.</span><span class="sxs-lookup"><span data-stu-id="c9f02-204">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="c9f02-205">Se você fizer isso, ele pode usar o [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) para consultar o número de telefone dos usuários, descubra se estiverem no escritório, quando o último logon, etc.</span><span class="sxs-lookup"><span data-stu-id="c9f02-205">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="c9f02-206">Isso é tudo o que você precisa fazer - Visual Studio solicitará as credenciais de um administrador para seu locatário do AD do Azure e, em seguida, ele configura seu projeto e o seu locatário do AD do Azure para o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9f02-206">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="c9f02-207">Quando você executar o projeto, você verá uma página de entrada, e você pode entrar com credenciais de um usuário em seu diretório do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f02-207">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![Org conta entrar](single-sign-on/_static/image25.png)

![Conectado](single-sign-on/_static/image26.png)

<span data-ttu-id="c9f02-210">Quando você implanta o aplicativo no Azure, tudo o que você precisa fazer é selecionar um **habilitar a autenticação organizacional** caixa de seleção e novamente o Visual Studio cuida da configuração para você.</span><span class="sxs-lookup"><span data-stu-id="c9f02-210">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![Publicar na Web](single-sign-on/_static/image27.png)

<span data-ttu-id="c9f02-212">Essas capturas de tela vêm de um tutorial passo a passo completo que mostra como criar um aplicativo que usa a autenticação do AD do Azure: [desenvolvendo aplicativos do ASP.NET com o Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c9f02-212">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="c9f02-213">Resumo</span><span class="sxs-lookup"><span data-stu-id="c9f02-213">Summary</span></span>

<span data-ttu-id="c9f02-214">Neste capítulo, você viu que Active Directory do Azure, o Visual Studio e o ASP.NET, mais fácil configurar o logon único em aplicativos da Internet para os usuários da organização.</span><span class="sxs-lookup"><span data-stu-id="c9f02-214">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="c9f02-215">Seus usuários podem inscrever-se em aplicativos da Internet usando as mesmas credenciais que eles usam para fazer logon usando o Active Directory na sua rede interna.</span><span class="sxs-lookup"><span data-stu-id="c9f02-215">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="c9f02-216">O [próximo capítulo](data-storage-options.md) examina as opções de armazenamento de dados disponíveis para um aplicativo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c9f02-216">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="c9f02-217">Recursos</span><span class="sxs-lookup"><span data-stu-id="c9f02-217">Resources</span></span>

<span data-ttu-id="c9f02-218">Para obter mais informações, consulte os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="c9f02-218">For more information, see the following resources:</span></span>

- <span data-ttu-id="c9f02-219">[Documentação do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c9f02-219">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="c9f02-220">Página do portal para obter a documentação do AD do Azure no site windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="c9f02-220">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="c9f02-221">Para obter os tutoriais passo a passo, consulte o **desenvolver** seção.</span><span class="sxs-lookup"><span data-stu-id="c9f02-221">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="c9f02-222">[Autenticação multifator do Azure](https://docs.microsoft.com/azure/multi-factor-authentication/).</span><span class="sxs-lookup"><span data-stu-id="c9f02-222">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="c9f02-223">Página do portal para documentação sobre a autenticação multifator no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f02-223">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="c9f02-224">[Opções de autenticação de conta organizacional](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span><span class="sxs-lookup"><span data-stu-id="c9f02-224">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="c9f02-225">Explicação das opções de autenticação do AD do Azure, na caixa de diálogo de novo projeto Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c9f02-225">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="c9f02-226">[Padrões e práticas - Microsoft federada padrão de identidade](https://msdn.microsoft.com/library/dn589790.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9f02-226">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="c9f02-227">[Como: Instalar a ferramenta de sincronização do Active Directory do Azure](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9f02-227">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="c9f02-228">[Serviços de Federação do Active Directory 2.0 mapa de conteúdo](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9f02-228">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="c9f02-229">Links para documentação sobre o AD FS 2.0.</span><span class="sxs-lookup"><span data-stu-id="c9f02-229">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="c9f02-230">[Autorização baseada em função e baseada em ACL em um aplicativo do Windows Azure AD](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span><span class="sxs-lookup"><span data-stu-id="c9f02-230">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="c9f02-231">Aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c9f02-231">Sample application.</span></span>
- <span data-ttu-id="c9f02-232">[Blog do Azure Active Directory Graph API](https://blogs.msdn.com/b/aadgraphteam/).</span><span class="sxs-lookup"><span data-stu-id="c9f02-232">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="c9f02-233">[Controle de acesso no BYOD e integração de diretórios em uma infraestrutura de identidade híbrida](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span><span class="sxs-lookup"><span data-stu-id="c9f02-233">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="c9f02-234">Tech Ed 2014 sessão vídeo por Gayana Bagdasaryan.</span><span class="sxs-lookup"><span data-stu-id="c9f02-234">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="c9f02-235">[Anterior](web-development-best-practices.md)
[Próximo](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="c9f02-235">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>