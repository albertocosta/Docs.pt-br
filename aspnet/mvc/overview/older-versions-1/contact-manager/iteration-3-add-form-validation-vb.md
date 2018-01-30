---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: "Iteração #3 – adicionar validação do formulário (VB) | Microsoft Docs"
author: microsoft
description: "Na terceira iteração, podemos adicionar validação de forma básica. Vamos impedir que pessoas enviando um formulário sem concluir os campos obrigatórios do formulário. Além disso, podemos validar e-mail..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: e9ed182fb58addd8c5dadbe6e3d09c391840ca00
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
<a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="d4d1e-105">Iteração #3 – adicionar validação do formulário (VB)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-105">Iteration #3 – Add form validation (VB)</span></span>
====================
<span data-ttu-id="d4d1e-106">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d4d1e-107">Baixar o código</span><span class="sxs-lookup"><span data-stu-id="d4d1e-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="d4d1e-108">Na terceira iteração, podemos adicionar validação de forma básica.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="d4d1e-109">Vamos impedir que pessoas enviando um formulário sem concluir os campos obrigatórios do formulário.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="d4d1e-110">Além disso, podemos validar endereços de email e números de telefone.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="d4d1e-111">Criando um aplicativo ASP.NET MVC de gerenciamento de contatos (VB)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="d4d1e-112">Esta série de tutoriais, vamos criar um aplicativo de gerenciamento de entre em contato com toda a partir do início ao fim.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="d4d1e-113">O aplicativo Gerenciador de entrar em contato com permite armazenar informações de contato - nomes, números de telefone e endereços de email - para obter uma lista de pessoas.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="d4d1e-114">Vamos criar o aplicativo em várias iterações.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="d4d1e-115">Com cada iteração, podemos melhorar gradualmente o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="d4d1e-116">O objetivo dessa abordagem iteração vários é para que você possa entender o motivo para cada alteração.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="d4d1e-117">Iteração #1 - criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="d4d1e-118">A primeira iteração, criamos o gerente do contato da maneira mais simples possível.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="d4d1e-119">Adicionamos suporte para operações de banco de dados básicos: criar, leitura, atualização e exclusão (CRUD).</span><span class="sxs-lookup"><span data-stu-id="d4d1e-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="d4d1e-120">Iteração #2 - Verifique o aplicativo parecer adequado.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="d4d1e-121">Essa iteração, podemos melhorar a aparência do aplicativo, modificando a página mestra do ASP.NET MVC exibição padrão e em cascata a folha de estilos.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="d4d1e-122">Iteração #3 - adicionar validação do formulário.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="d4d1e-123">Na terceira iteração, podemos adicionar validação de forma básica.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="d4d1e-124">Vamos impedir que pessoas enviando um formulário sem concluir os campos obrigatórios do formulário.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="d4d1e-125">Além disso, podemos validar endereços de email e números de telefone.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="d4d1e-126">Iteração #4 - Verifique o aplicativo acoplados de forma flexível.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="d4d1e-127">Essa terceira iteração, podemos aproveitar vários padrões de design de software para facilitar a manutenção e modificar o aplicativo Gerenciador de contato.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-127">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="d4d1e-128">Por exemplo, podemos refatorar nosso aplicativo para usar o padrão de repositório e o padrão de injeção de dependência.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="d4d1e-129">Iteração #5 - criar testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="d4d1e-130">Na quinta iteração, fazemos nosso aplicativo mais fácil de manter e modificar adicionando testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="d4d1e-131">Vamos simular nossas classes de modelo de dados e criar testes de unidade para nossos controladores e lógica de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="d4d1e-132">Iteração #6 - Use desenvolvimento controlado por testes.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="d4d1e-133">Essa iteração do sexto, adicionamos novas funcionalidades para nosso aplicativo escrevendo testes de unidade primeiro e escrever código os testes de unidade.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="d4d1e-134">Essa iteração, adicionamos grupos de contatos.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="d4d1e-135">Iteração #7 - adicionar funcionalidade Ajax.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="d4d1e-136">A sétima iteração, podemos melhorar a capacidade de resposta e o desempenho do nosso aplicativo, adicionando suporte para Ajax.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="d4d1e-137">Essa iteração</span><span class="sxs-lookup"><span data-stu-id="d4d1e-137">This Iteration</span></span>

<span data-ttu-id="d4d1e-138">Essa segunda iteração do aplicativo Gerenciador de contato, adicionamos validação de forma básica.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="d4d1e-139">Vamos impedir que pessoas enviando um contato sem inserir valores para os campos obrigatórios do formulário.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="d4d1e-140">Além disso, podemos validar números de telefone e endereços de email (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="d4d1e-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="d4d1e-141">[![A caixa de diálogo Novo projeto](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="d4d1e-142">**Figura 01**: um formulário com validação ([clique para exibir a imagem em tamanho normal](iteration-3-add-form-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d4d1e-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>


<span data-ttu-id="d4d1e-143">Essa iteração, adicionamos a lógica de validação diretamente para as ações do controlador.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="d4d1e-144">Em geral, isso não é a maneira recomendada para adicionar validação a um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="d4d1e-145">Uma abordagem melhor é colocar uma lógica de validação do aplicativo s em uma separada [camada de serviço](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span><span class="sxs-lookup"><span data-stu-id="d4d1e-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="d4d1e-146">Na próxima iteração, podemos refatorar o aplicativo Gerenciador de contato para tornar o aplicativo mais fácil manutenção.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="d4d1e-147">Essa iteração, para manter as coisas simples, vamos escrever todo o código de validação manualmente.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="d4d1e-148">Em vez de escrever código de validação de nós, podemos pode tirar proveito de uma estrutura de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="d4d1e-149">Por exemplo, você pode usar o Microsoft Enterprise Library validação aplicativo bloco (VAB) para implementar a lógica de validação para o seu aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="d4d1e-150">Para saber mais sobre o bloco de aplicativo de validação, consulte:</span><span class="sxs-lookup"><span data-stu-id="d4d1e-150">To learn more about the Validation Application Block, see:</span></span>

[<span data-ttu-id="d4d1e-151">*http://msdn.microsoft.com/library/dd203099.aspx*</span><span class="sxs-lookup"><span data-stu-id="d4d1e-151">*http://msdn.microsoft.com/library/dd203099.aspx*</span></span>](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="d4d1e-152">Adicionando validação para o modo de criação</span><span class="sxs-lookup"><span data-stu-id="d4d1e-152">Adding Validation to the Create View</span></span>

<span data-ttu-id="d4d1e-153">Permitir que o s comece adicionando lógica de validação para o modo de criação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-153">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="d4d1e-154">Felizmente, porque é gerado o Create view com o Visual Studio, o modo de exibição de criar já contém toda a lógica de interface de usuário necessários para exibir mensagens de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-154">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="d4d1e-155">O modo de exibição de criar está contido na listagem 1.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-155">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="d4d1e-156">**Listando 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="d4d1e-156">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="d4d1e-157">A classe de erro de validação de campo é usada para definir o estilo a saída processada pelo auxiliar de Html.ValidationMessage().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-157">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="d4d1e-158">A classe de erro de validação de entrada é usada para definir o estilo de caixa de texto (entrada) processado pelo auxiliar de Html.TextBox().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-158">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="d4d1e-159">A classe de erros de resumo de validação é usada para definir o estilo de lista não ordenada renderizada pelo auxiliar de Html.ValidationSummary().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-159">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d4d1e-160">Você pode modificar as classes de folha de estilo descritas nesta seção para personalizar a aparência das mensagens de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-160">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="d4d1e-161">Adicionando a lógica de validação a criar ação</span><span class="sxs-lookup"><span data-stu-id="d4d1e-161">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="d4d1e-162">Neste momento, a criar nunca exibe mensagens de erro de validação porque nós não foram gravadas a lógica para gerar todas as mensagens.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-162">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="d4d1e-163">Para exibir mensagens de erro de validação, você precisa adicionar as mensagens de erro para o ModelState.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-163">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d4d1e-164">O método UpdateModel() adiciona mensagens de erro para o ModelState automaticamente quando há um erro ao atribuir o valor de um campo de formulário a uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-164">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="d4d1e-165">Por exemplo, se você tentar atribuir a cadeia de caracteres "apple" em uma propriedade de data de nascimento que aceita valores de data e hora, o método UpdateModel() adiciona um erro ao ModelState.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-165">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="d4d1e-166">O método Create () modificado na listagem 2 contém uma nova seção que valida as propriedades da classe contato antes do novo contato é inserido no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-166">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="d4d1e-167">**A listagem 2 - Controllers\ContactController.vb (criar com validação)**</span><span class="sxs-lookup"><span data-stu-id="d4d1e-167">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="d4d1e-168">A seção de validar impõe quatro regras de validação distintos:</span><span class="sxs-lookup"><span data-stu-id="d4d1e-168">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="d4d1e-169">A propriedade de nome deve ter um comprimento maior que zero (e ele não pode conter somente espaços)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-169">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="d4d1e-170">A propriedade LastName deve ter um comprimento maior que zero (e ele não pode conter somente espaços)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-170">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="d4d1e-171">Se a propriedade de telefone tem um valor (tem um comprimento maior que 0), em seguida, a propriedade do telefone deve corresponder a uma expressão regular.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-171">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="d4d1e-172">Se a propriedade de Email tem um valor (tem um comprimento maior que 0), em seguida, a propriedade de Email deve corresponder a uma expressão regular.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-172">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="d4d1e-173">Quando há uma violação de regra de validação, uma mensagem de erro é adicionada ao ModelState com a Ajuda do método AddModelError().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-173">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="d4d1e-174">Quando você adiciona uma mensagem para o ModelState, forneça o nome de uma propriedade e o texto de uma mensagem de erro de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-174">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="d4d1e-175">Essa mensagem de erro é exibida no modo de exibição, os métodos auxiliares Html.ValidationSummary() e Html.ValidationMessage().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-175">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="d4d1e-176">Depois que as regras de validação são executadas, a propriedade IsValid de ModelState é verificada.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-176">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="d4d1e-177">A propriedade IsValid retorna false quando as mensagens de erro de validação foram adicionadas ao ModelState.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-177">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="d4d1e-178">Se a validação falhar, o formulário de criação é exibida novamente com as mensagens de erro.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-178">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d4d1e-179">Recebi as expressões regulares para validar o telefone e endereço de email do repositório de expressão regular no [ *http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-179">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="d4d1e-180">Adicionando lógica de validação para a ação de edição</span><span class="sxs-lookup"><span data-stu-id="d4d1e-180">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="d4d1e-181">A ação Edit() atualiza um contato.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-181">The Edit() action updates a Contact.</span></span> <span data-ttu-id="d4d1e-182">A ação Edit() precisa executar a mesma validação como a ação Create ().</span><span class="sxs-lookup"><span data-stu-id="d4d1e-182">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="d4d1e-183">Em vez de duplicar o mesmo código de validação, podemos deve refatorar o controlador de contato para que as ações de Create () e Edit() chamar o mesmo método de validação.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-183">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="d4d1e-184">A classe do controlador contato modificada está contida na listagem 3.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-184">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="d4d1e-185">Essa classe tem um novo método ValidateContact() que é chamado dentro de Create () e Edit() ações.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-185">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="d4d1e-186">**A listagem 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="d4d1e-186">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="d4d1e-187">Resumo</span><span class="sxs-lookup"><span data-stu-id="d4d1e-187">Summary</span></span>

<span data-ttu-id="d4d1e-188">Essa iteração, adicionamos validação do formulário básico para nosso aplicativo Gerenciador de contato.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-188">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="d4d1e-189">Nossa lógica de validação impede que os usuários enviar um novo contato ou editar um contato existente sem fornecer valores para as propriedades de nome e sobrenome.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-189">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="d4d1e-190">Além disso, os usuários devem fornecer endereços de email e números de telefone válido.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-190">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="d4d1e-191">Essa iteração, adicionamos a lógica de validação ao nosso aplicativo Gerenciador de contato da maneira mais fácil possível.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-191">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="d4d1e-192">No entanto, misturar nossa lógica de validação em nossa lógica do controlador criará problemas para que possamos a longo prazo.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-192">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="d4d1e-193">Nosso aplicativo poderá ser mais difícil de manter e modificar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-193">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="d4d1e-194">Na próxima iteração, podemos será refatorar nossa lógica de validação e a lógica de acesso a banco de dados fora de nosso controladores.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-194">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="d4d1e-195">Vamos dar aproveitar vários princípios de design de software que permitem a criação de um aplicativo mais flexível e mais fácil manutenção.</span><span class="sxs-lookup"><span data-stu-id="d4d1e-195">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="d4d1e-196">[Anterior](iteration-2-make-the-application-look-nice-vb.md)
[Próximo](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="d4d1e-196">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>