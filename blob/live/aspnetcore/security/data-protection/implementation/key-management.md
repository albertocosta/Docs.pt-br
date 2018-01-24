---
title: Gerenciamento de chaves
author: rick-anderson
description: "Este documento descreve os detalhes da implementação do ASP.NET Core dados proteção gerenciamento APIs."
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/implementation/key-management
ms.openlocfilehash: 53adb067751917a9539a310bb7d91e599696f213
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/19/2018
---
# <a name="key-management"></a><span data-ttu-id="1f6af-103">Gerenciamento de chaves</span><span class="sxs-lookup"><span data-stu-id="1f6af-103">Key Management</span></span>

<a name="data-protection-implementation-key-management"></a>

<span data-ttu-id="1f6af-104">O sistema de proteção de dados gerencia automaticamente o tempo de vida das chaves mestras usado para proteger e Desproteger cargas.</span><span class="sxs-lookup"><span data-stu-id="1f6af-104">The data protection system automatically manages the lifetime of master keys used to protect and unprotect payloads.</span></span> <span data-ttu-id="1f6af-105">Cada chave pode existir em um dos quatro estágios:</span><span class="sxs-lookup"><span data-stu-id="1f6af-105">Each key can exist in one of four stages:</span></span>

* <span data-ttu-id="1f6af-106">Criado - a chave existe em anel chave, mas ainda não foi ativada.</span><span class="sxs-lookup"><span data-stu-id="1f6af-106">Created - the key exists in the key ring but has not yet been activated.</span></span> <span data-ttu-id="1f6af-107">A chave não deve ser usada para novas operações de proteção até que tenha decorrido tempo suficiente que a chave tenha tido a oportunidade de se propague para todos os computadores que estão consumindo anel essa chave.</span><span class="sxs-lookup"><span data-stu-id="1f6af-107">The key shouldn't be used for new Protect operations until sufficient time has elapsed that the key has had a chance to propagate to all machines that are consuming this key ring.</span></span>

* <span data-ttu-id="1f6af-108">Ativo - a chave existe do anel de chave e deve ser usado para todas as operações de proteção de novo.</span><span class="sxs-lookup"><span data-stu-id="1f6af-108">Active - the key exists in the key ring and should be used for all new Protect operations.</span></span>

* <span data-ttu-id="1f6af-109">A chave expirada - ficou seu tempo de vida natural e não deve ser usada para novas operações de proteção.</span><span class="sxs-lookup"><span data-stu-id="1f6af-109">Expired - the key has run its natural lifetime and should no longer be used for new Protect operations.</span></span>

* <span data-ttu-id="1f6af-110">A chave revogada - estiver comprometida e não deve ser usada para novas operações de proteção.</span><span class="sxs-lookup"><span data-stu-id="1f6af-110">Revoked - the key is compromised and must not be used for new Protect operations.</span></span>

<span data-ttu-id="1f6af-111">Todas as chaves expiradas, ativas e criadas podem ser usadas para desproteger cargas de entrada.</span><span class="sxs-lookup"><span data-stu-id="1f6af-111">Created, active, and expired keys may all be used to unprotect incoming payloads.</span></span> <span data-ttu-id="1f6af-112">Chaves revogadas por padrão não podem ser usadas para desproteger cargas, mas o desenvolvedor do aplicativo pode [substituir esse comportamento](../consumer-apis/dangerous-unprotect.md#data-protection-consumer-apis-dangerous-unprotect) se necessário.</span><span class="sxs-lookup"><span data-stu-id="1f6af-112">Revoked keys by default may not be used to unprotect payloads, but the application developer can [override this behavior](../consumer-apis/dangerous-unprotect.md#data-protection-consumer-apis-dangerous-unprotect) if necessary.</span></span>

>[!WARNING]
> <span data-ttu-id="1f6af-113">O desenvolvedor pode ser tentado para excluir uma chave do anel de chave (por exemplo, excluindo o arquivo correspondente do sistema de arquivos).</span><span class="sxs-lookup"><span data-stu-id="1f6af-113">The developer might be tempted to delete a key from the key ring (e.g., by deleting the corresponding file from the file system).</span></span> <span data-ttu-id="1f6af-114">Nesse ponto, todos os dados protegidos pela chave é indecifráveis permanentemente e não há nenhuma substituição de emergência como ocorre com chaves revogadas.</span><span class="sxs-lookup"><span data-stu-id="1f6af-114">At that point, all data protected by the key is permanently undecipherable, and there is no emergency override like there is with revoked keys.</span></span> <span data-ttu-id="1f6af-115">Exclusão de uma chave é realmente destrutivo comportamento e, consequentemente, o sistema de proteção de dados não expõe nenhuma API de primeira classe para executar esta operação.</span><span class="sxs-lookup"><span data-stu-id="1f6af-115">Deleting a key is truly destructive behavior, and consequently the data protection system exposes no first-class API for performing this operation.</span></span>

## <a name="default-key-selection"></a><span data-ttu-id="1f6af-116">Seleção de chave padrão</span><span class="sxs-lookup"><span data-stu-id="1f6af-116">Default key selection</span></span>

<span data-ttu-id="1f6af-117">Quando o sistema de proteção de dados lê o anel de chave do repositório de backup, ele tentará localizar uma chave "padrão" do anel de chave.</span><span class="sxs-lookup"><span data-stu-id="1f6af-117">When the data protection system reads the key ring from the backing repository, it will attempt to locate a "default" key from the key ring.</span></span> <span data-ttu-id="1f6af-118">A chave padrão é usada para novas operações de proteção.</span><span class="sxs-lookup"><span data-stu-id="1f6af-118">The default key is used for new Protect operations.</span></span>

<span data-ttu-id="1f6af-119">A heurística geral é que o sistema de proteção de dados escolhe a chave com a data mais recente de ativação como a chave padrão.</span><span class="sxs-lookup"><span data-stu-id="1f6af-119">The general heuristic is that the data protection system chooses the key with the most recent activation date as the default key.</span></span> <span data-ttu-id="1f6af-120">(Há um pequeno fator para permitir o relógio do servidor-para-servidor distorção.) Se a chave expirou ou foi revogada, e se o aplicativo não tiver desabilitado automática da chave de geração, uma nova chave será gerada com a ativação imediata pelo [chave expiração e sem interrupção](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) diretiva abaixo.</span><span class="sxs-lookup"><span data-stu-id="1f6af-120">(There's a small fudge factor to allow for server-to-server clock skew.) If the key is expired or revoked, and if the application has not disabled automatic key generation, then a new key will be generated with immediate activation per the [key expiration and rolling](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management-expiration) policy below.</span></span>

<span data-ttu-id="1f6af-121">O motivo pelo qual o sistema de proteção de dados gera uma nova chave imediatamente em vez de fazer fallback para uma chave diferente é que a nova geração de chave deve ser tratada como uma expiração implícita de todas as chaves que foram ativados antes da nova chave.</span><span class="sxs-lookup"><span data-stu-id="1f6af-121">The reason the data protection system generates a new key immediately rather than falling back to a different key is that new key generation should be treated as an implicit expiration of all keys that were activated prior to the new key.</span></span> <span data-ttu-id="1f6af-122">A ideia geral é que novas chaves podem ter sido configuradas com algoritmos diferentes ou mecanismos de criptografia em repouso que as chaves antigas, e o sistema deve preferir a configuração atual em vez de fazer o fallback.</span><span class="sxs-lookup"><span data-stu-id="1f6af-122">The general idea is that new keys may have been configured with different algorithms or encryption-at-rest mechanisms than old keys, and the system should prefer the current configuration over falling back.</span></span>

<span data-ttu-id="1f6af-123">Há uma exceção.</span><span class="sxs-lookup"><span data-stu-id="1f6af-123">There is an exception.</span></span> <span data-ttu-id="1f6af-124">Se o desenvolvedor do aplicativo tiver [desabilitado a geração automática de chaves](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), em seguida, o sistema de proteção de dados deve escolher algo como a chave padrão.</span><span class="sxs-lookup"><span data-stu-id="1f6af-124">If the application developer has [disabled automatic key generation](xref:security/data-protection/configuration/overview#disableautomatickeygeneration), then the data protection system must choose something as the default key.</span></span> <span data-ttu-id="1f6af-125">Neste cenário de fallback, o sistema escolherá a chave não revogado com a data de ativação mais recente, com preferência para chaves que tem tido tempo para ser propagada para outros computadores no cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6af-125">In this fallback scenario, the system will choose the non-revoked key with the most recent activation date, with preference given to keys that have had time to propagate to other machines in the cluster.</span></span> <span data-ttu-id="1f6af-126">O sistema de fallback pode acabar escolhendo uma chave padrão expiradas como resultado.</span><span class="sxs-lookup"><span data-stu-id="1f6af-126">The fallback system may end up choosing an expired default key as a result.</span></span> <span data-ttu-id="1f6af-127">O sistema de fallback nunca escolherá uma chave revogada como a chave padrão e se o anel de chave está vazio ou foi revogado cada chave, em seguida, o sistema produzirá um erro na inicialização.</span><span class="sxs-lookup"><span data-stu-id="1f6af-127">The fallback system will never choose a revoked key as the default key, and if the key ring is empty or every key has been revoked then the system will produce an error upon initialization.</span></span>

<a name="data-protection-implementation-key-management-expiration"></a>

## <a name="key-expiration-and-rolling"></a><span data-ttu-id="1f6af-128">Expiração e sem interrupção</span><span class="sxs-lookup"><span data-stu-id="1f6af-128">Key expiration and rolling</span></span>

<span data-ttu-id="1f6af-129">Quando uma chave é criada, ele recebe automaticamente uma data de ativação de {agora + 2 dias} e uma data de expiração de {agora + 90 dias}.</span><span class="sxs-lookup"><span data-stu-id="1f6af-129">When a key is created, it is automatically given an activation date of { now + 2 days } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="1f6af-130">O atraso de 2 dias antes da ativação fornece o momento chave se propague através do sistema.</span><span class="sxs-lookup"><span data-stu-id="1f6af-130">The 2-day delay before activation gives the key time to propagate through the system.</span></span> <span data-ttu-id="1f6af-131">Ou seja, permite que outros aplicativos apontando para o armazenamento de backup observar a chave em seu próximo período de atualização automática, portanto, maximizando a probabilidade de que quando a chave de anel faz se tornar ativo foi propagado para todos os aplicativos que talvez precisem usá-la.</span><span class="sxs-lookup"><span data-stu-id="1f6af-131">That is, it allows other applications pointing at the backing store to observe the key at their next auto-refresh period, thus maximizing the chances that when the key ring does become active it has propagated to all applications that might need to use it.</span></span>

<span data-ttu-id="1f6af-132">Se a chave padrão expirará dentro de 2 dias e o anel de chave ainda não tiver uma chave que ficará ativa após a expiração da chave padrão, o sistema de proteção de dados persistirá automaticamente uma nova chave para o anel de chave.</span><span class="sxs-lookup"><span data-stu-id="1f6af-132">If the default key will expire within 2 days and if the key ring does not already have a key that will be active upon expiration of the default key, then the data protection system will automatically persist a new key to the key ring.</span></span> <span data-ttu-id="1f6af-133">Essa nova chave tem uma data de ativação de {data de validade da chave padrão} e a data de expiração de {agora + 90 dias}.</span><span class="sxs-lookup"><span data-stu-id="1f6af-133">This new key has an activation date of { default key's expiration date } and an expiration date of { now + 90 days }.</span></span> <span data-ttu-id="1f6af-134">Isso permite que o sistema automaticamente reverter chaves regularmente sem interrupção do serviço.</span><span class="sxs-lookup"><span data-stu-id="1f6af-134">This allows the system to automatically roll keys on a regular basis with no interruption of service.</span></span>

<span data-ttu-id="1f6af-135">Pode haver circunstâncias em que uma chave será criada com a ativação imediata.</span><span class="sxs-lookup"><span data-stu-id="1f6af-135">There might be circumstances where a key will be created with immediate activation.</span></span> <span data-ttu-id="1f6af-136">Um exemplo seria quando o aplicativo não tiver sido executada por um tempo e todas as chaves do anel de chave expiradas.</span><span class="sxs-lookup"><span data-stu-id="1f6af-136">One example would be when the application hasn't run for a time and all keys in the key ring are expired.</span></span> <span data-ttu-id="1f6af-137">Quando isso acontece, a chave é fornecida uma data de ativação de {agora} sem o atraso de ativação de 2 dias normal.</span><span class="sxs-lookup"><span data-stu-id="1f6af-137">When this happens, the key is given an activation date of { now } without the normal 2-day activation delay.</span></span>

<span data-ttu-id="1f6af-138">O tempo de vida de chave padrão é de 90 dias, embora isso é configurado como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f6af-138">The default key lifetime is 90 days, though this is configurable as in the following example.</span></span>

```csharp
services.AddDataProtection()
       // use 14-day lifetime instead of 90-day lifetime
       .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
```

<span data-ttu-id="1f6af-139">Um administrador também pode alterar o padrão para todo o sistema, embora uma chamada explícita para `SetDefaultKeyLifetime` substituirá qualquer política de todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="1f6af-139">An administrator can also change the default system-wide, though an explicit call to `SetDefaultKeyLifetime` will override any system-wide policy.</span></span> <span data-ttu-id="1f6af-140">O tempo de vida de chave padrão não pode ser menor do que 7 dias.</span><span class="sxs-lookup"><span data-stu-id="1f6af-140">The default key lifetime cannot be shorter than 7 days.</span></span>

## <a name="automatic-key-ring-refresh"></a><span data-ttu-id="1f6af-141">Atualização automática anel de chave</span><span class="sxs-lookup"><span data-stu-id="1f6af-141">Automatic key ring refresh</span></span>

<span data-ttu-id="1f6af-142">Quando o sistema de proteção de dados inicializado, ele lê o anel de chave do repositório subjacente e armazena em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="1f6af-142">When the data protection system initializes, it reads the key ring from the underlying repository and caches it in memory.</span></span> <span data-ttu-id="1f6af-143">Esse cache permite proteger e Desproteger operações continuem sem atingir o armazenamento de backup.</span><span class="sxs-lookup"><span data-stu-id="1f6af-143">This cache allows Protect and Unprotect operations to proceed without hitting the backing store.</span></span> <span data-ttu-id="1f6af-144">O sistema verifica automaticamente o repositório de backup para alterações de aproximadamente a cada 24 horas ou quando a chave padrão atual expirar, o que ocorrer primeiro.</span><span class="sxs-lookup"><span data-stu-id="1f6af-144">The system will automatically check the backing store for changes approximately every 24 hours or when the current default key expires, whichever comes first.</span></span>

>[!WARNING]
> <span data-ttu-id="1f6af-145">Os desenvolvedores devem muito raramente (se) precisa usar APIs de gerenciamento de chave diretamente.</span><span class="sxs-lookup"><span data-stu-id="1f6af-145">Developers should very rarely (if ever) need to use the key management APIs directly.</span></span> <span data-ttu-id="1f6af-146">O sistema de proteção de dados executará gerenciamento automático de chaves, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="1f6af-146">The data protection system will perform automatic key management as described above.</span></span>

<span data-ttu-id="1f6af-147">O sistema de proteção de dados expõe uma interface `IKeyManager` que pode ser usado para inspecionar e fazer alterações para o anel de chave.</span><span class="sxs-lookup"><span data-stu-id="1f6af-147">The data protection system exposes an interface `IKeyManager` that can be used to inspect and make changes to the key ring.</span></span> <span data-ttu-id="1f6af-148">O sistema de DI que forneceu a instância do `IDataProtectionProvider` também pode fornecer uma instância de `IKeyManager` para seu consumo.</span><span class="sxs-lookup"><span data-stu-id="1f6af-148">The DI system that provided the instance of `IDataProtectionProvider` can also provide an instance of `IKeyManager` for your consumption.</span></span> <span data-ttu-id="1f6af-149">Como alternativa, você pode extrair o `IKeyManager` diretamente do `IServiceProvider` como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f6af-149">Alternatively, you can pull the `IKeyManager` straight from the `IServiceProvider` as in the example below.</span></span>

<span data-ttu-id="1f6af-150">Qualquer operação que modifica o anel de chave (Criando uma nova chave explicitamente ou uma revogação) invalida o cache na memória.</span><span class="sxs-lookup"><span data-stu-id="1f6af-150">Any operation which modifies the key ring (creating a new key explicitly or performing a revocation) will invalidate the in-memory cache.</span></span> <span data-ttu-id="1f6af-151">A próxima chamada para `Protect` ou `Unprotect` fará com que o sistema de proteção de dados reler o anel de chave e recriar o cache.</span><span class="sxs-lookup"><span data-stu-id="1f6af-151">The next call to `Protect` or `Unprotect` will cause the data protection system to reread the key ring and recreate the cache.</span></span>

<span data-ttu-id="1f6af-152">O exemplo a seguir demonstra como usar o `IKeyManager` interface para inspecionar e manipular o anel de chave, incluindo a revogação existente chaves e gerar uma nova chave manualmente.</span><span class="sxs-lookup"><span data-stu-id="1f6af-152">The sample below demonstrates using the `IKeyManager` interface to inspect and manipulate the key ring, including revoking existing keys and generating a new key manually.</span></span>

[!code-csharp[Main](key-management/samples/key-management.cs)]

## <a name="key-storage"></a><span data-ttu-id="1f6af-153">Armazenamento de chaves</span><span class="sxs-lookup"><span data-stu-id="1f6af-153">Key storage</span></span>

<span data-ttu-id="1f6af-154">O sistema de proteção de dados tem uma heurística na qual ele tenta deduzir um local de armazenamento de chave apropriado e criptografia no mecanismo de rest automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1f6af-154">The data protection system has a heuristic whereby it tries to deduce an appropriate key storage location and encryption at rest mechanism automatically.</span></span> <span data-ttu-id="1f6af-155">Isso também é configurável pelo desenvolvedor do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f6af-155">This is also configurable by the app developer.</span></span> <span data-ttu-id="1f6af-156">Os documentos a seguir discutem as implementações de caixa de entrada desses mecanismos:</span><span class="sxs-lookup"><span data-stu-id="1f6af-156">The following documents discuss the in-box implementations of these mechanisms:</span></span>

* [<span data-ttu-id="1f6af-157">Na caixa de provedores de armazenamento de chaves</span><span class="sxs-lookup"><span data-stu-id="1f6af-157">In-box key storage providers</span></span>](key-storage-providers.md#data-protection-implementation-key-storage-providers)

* [<span data-ttu-id="1f6af-158">Na caixa de criptografia de chave nos provedores de rest</span><span class="sxs-lookup"><span data-stu-id="1f6af-158">In-box key encryption at rest providers</span></span>](key-encryption-at-rest.md#data-protection-implementation-key-encryption-at-rest-providers)