---
title: .NET Standard | Microsoft Docs
description: "了解 .NET Standard、其版本及支援的 .NET 實作。"
keywords: .NET Standard, PCL, .NET
author: mairaw
ms.author: mairaw
ms.date: 08/13/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: c044882c-af15-45f2-96d1-534557a5ee9b
ms.translationtype: HT
ms.sourcegitcommit: b47d4c74a01b99d743b69328c201096bc8d89794
ms.openlocfilehash: eaae98ce0f7a1b49669098812193ae1b629584a4
ms.contentlocale: zh-tw
ms.lasthandoff: 08/21/2017

---
# <a name="net-standard"></a><span data-ttu-id="4b9c9-104">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4b9c9-104">.NET Standard</span></span>

<span data-ttu-id="4b9c9-105">[.NET Standard](https://github.com/dotnet/standard) 是計劃在所有 .NET 實作提供的 .NET API 型式規格。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-105">The [.NET Standard](https://github.com/dotnet/standard) is a formal specification of .NET APIs that are intended to be available on all .NET implementations.</span></span> <span data-ttu-id="4b9c9-106">.NET Standard 背後的動機是在 .NET 生態系統中建立更高的一致性。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-106">The motivation behind the .NET Standard is establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="4b9c9-107">[ECMA 335](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) 會繼續建立 .NET 實作行為的一致性，但沒有 .NET 程式庫實作之 .NET 基底類別庫 (BCL) 的類似規格。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-107">[ECMA 335](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) continues to establish uniformity for .NET implementation behavior, but there is no similar spec for the .NET Base Class Libraries (BCL) for .NET library implementations.</span></span> 

<span data-ttu-id="4b9c9-108">.NET Standard 支援下列重要案例：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-108">The .NET Standard enables the following key scenarios:</span></span> 

- <span data-ttu-id="4b9c9-109">定義一致的 BCL API 集合，以供所有 .NET 實作來實作，而不論工作負載為何。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-109">Defines uniform set of BCL APIs for all .NET implementations to implement, independent of workload.</span></span>
- <span data-ttu-id="4b9c9-110">可讓開發人員使用這組相同的 API，產生可跨 .NET 實作使用的可攜式程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-110">Enables developers to produce portable libraries that are usable across .NET implementations, using this same set of APIs.</span></span>
- <span data-ttu-id="4b9c9-111">減少或甚至排除因 .NET API 而必須對共用原始檔進行的條件式編譯，僅適用於 OS API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-111">Reduces or even eliminates conditional compilation of shared source due to .NET APIs, only for OS APIs.</span></span>

<span data-ttu-id="4b9c9-112">不同的 .NET 實作會以特定版本的 .NET Standard 為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-112">The various .NET implementations target specific versions of .NET Standard.</span></span> <span data-ttu-id="4b9c9-113">每個 .NET 實作版本會宣佈它所支援的最高 .NET Standard 版本，此聲明表示它也會支援舊版。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-113">Each .NET implementation version advertises the highest .NET Standard version it supports, a statement that means it also supports previous versions.</span></span> <span data-ttu-id="4b9c9-114">例如，.NET Framework 4.6 會實作 .NET Standard 1.3，這意謂著它會公開 .NET Standard 1.0 到 1.3 版中定義的所有 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-114">For example, the .NET Framework 4.6 implements .NET Standard 1.3, which means that it exposes all APIs defined in .NET Standard versions 1.0 through 1.3.</span></span> <span data-ttu-id="4b9c9-115">同樣地，.NET Framework 4.6.1 會實作 .NET Standard 1.4，而 .NET Core 1.0 會實作 .NET Standard 1.6。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-115">Similarly, the .NET Framework 4.6.1 implements .NET Standard 1.4, while .NET Core 1.0 implements .NET Standard 1.6.</span></span>

## <a name="net-implementation-support"></a><span data-ttu-id="4b9c9-116">.NET 實作支援</span><span class="sxs-lookup"><span data-stu-id="4b9c9-116">.NET implementation support</span></span>

<span data-ttu-id="4b9c9-117">下表列出所有 .NET Standard 版本和支援的平台：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-117">The following table lists all versions of .NET Standard and the platforms supported:</span></span>

[!INCLUDE [net-standard-table](~/includes/net-standard-table.md)]

<span data-ttu-id="4b9c9-118">若要尋找可作為您目標的最新 .NET Standard 版本，請執行下列操作：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-118">To find the highest version of .NET Standard that you can target, do the following:</span></span>
1. <span data-ttu-id="4b9c9-119">尋找指出要作為您執行位置之 .NET 實作的資料列。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-119">Find the row that indicate the .NET implementation you want to run on.</span></span>
2. <span data-ttu-id="4b9c9-120">在該資料列中，由左到右尋找指出您版本的資料行。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-120">Find the column in that row that indicates your version starting from right to left.</span></span>
3. <span data-ttu-id="4b9c9-121">資料行標題會指出您目標所支援的 .NET Standard 版本 (而所有較舊的 .NET Standard 版本也都會支援它)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-121">The column header indicates the .NET Standard version that your target supports (and any lower .NET Standard versions will also support it).</span></span>
4. <span data-ttu-id="4b9c9-122">針對您想要作為目標的每個平台重複此程序。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-122">Repeat this process for each platform you want to target.</span></span> <span data-ttu-id="4b9c9-123">如果您有多個目標平台，應該從中挑選最舊的版本。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-123">If you have more than one target platform, you should pick the smaller version among them.</span></span> <span data-ttu-id="4b9c9-124">例如，如果您想要在 .NET Framework 4.5 和 .NET Core 1.0 上執行，則可以使用的最新 .NET Standard 版本是 .NET Standard 1.1。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-124">For example, if you want to run on .NET Framework 4.5 and .NET Core 1.0, the highest .NET Standard version you can use is .NET Standard 1.1.</span></span>

### <a name="which-net-standard-version-to-target"></a><span data-ttu-id="4b9c9-125">要以哪個 .NET Standard 版本作為目標</span><span class="sxs-lookup"><span data-stu-id="4b9c9-125">Which .NET Standard version to target</span></span>

<span data-ttu-id="4b9c9-126">選擇 .NET Standard 版本時，您應該考量下列取捨：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-126">When choosing a .NET Standard version, you should consider this trade-off:</span></span>

- <span data-ttu-id="4b9c9-127">版本越新，可供您使用的 API 就越多。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-127">The higher the version, the more APIs are available to you.</span></span>
- <span data-ttu-id="4b9c9-128">版本越舊，可實作它的平台就越多。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-128">The lower the version, the more platforms implement it.</span></span>

<span data-ttu-id="4b9c9-129">一般而言，建議您儘可能以「最舊的」.NET Standard 版本為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-129">In general, we recommend you to target the *lowest* version of .NET Standard possible.</span></span> <span data-ttu-id="4b9c9-130">因此，在您找到可作為目標的最新 .NET Standard 版本之後，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-130">So, after you find the highest .NET Standard version you can target, follow these steps:</span></span>
1. <span data-ttu-id="4b9c9-131">以次舊的 .NET Standard 版本為目標並建置您的專案。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-131">Target the next lower version of .NET Standard and build your project.</span></span>
2. <span data-ttu-id="4b9c9-132">如果您的專案建置成功，便重複步驟 1。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-132">If your project builds successfully, repeat step 1.</span></span> <span data-ttu-id="4b9c9-133">否則，請將目標重新設定為次新版本，這會是您應該使用的版本。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-133">Otherwise, retarget to the next higher version and that's the version you should use.</span></span>

### <a name="net-standard-versioning-rules"></a><span data-ttu-id="4b9c9-134">.NET Standard 版本控制規則</span><span class="sxs-lookup"><span data-stu-id="4b9c9-134">.NET Standard versioning rules</span></span>

<span data-ttu-id="4b9c9-135">有兩個主要的版本控制規則：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-135">There are two primary versioning rules:</span></span>

- <span data-ttu-id="4b9c9-136">累加：.NET Standard 版本就邏輯而言是同心圓：較新的版本會包含來自較舊版本的所有 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-136">Additive: .NET Standard versions are logically concentric circles: higher versions incorporate all APIs from previous versions.</span></span> <span data-ttu-id="4b9c9-137">版本之間並沒有任何重大變更。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-137">There are no breaking changes between versions.</span></span>
- <span data-ttu-id="4b9c9-138">不可變。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-138">Immutable.</span></span> <span data-ttu-id="4b9c9-139">.NET Standard 在交付後，版本便已凍結。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-139">Once shipped, .NET Standard versions are frozen.</span></span> <span data-ttu-id="4b9c9-140">新 API 將先在特定的 .NET 實作 (例如 .NET Core) 中提供。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-140">New APIs will first become available in specific .NET implementations, such as .NET Core.</span></span> <span data-ttu-id="4b9c9-141">如果 .NET Standard 審查委員會認為應該在所有平台都提供新的 API，就會在新的 .NET Standard 版本中新增這些 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-141">If the .NET Standard review board believes the new APIs should be made available everywhere, they'll be added in a new .NET Standard version.</span></span>

## <a name="comparison-to-portable-class-libraries"></a><span data-ttu-id="4b9c9-142">與可攜式類別庫的比較</span><span class="sxs-lookup"><span data-stu-id="4b9c9-142">Comparison to Portable Class Libraries</span></span>

<span data-ttu-id="4b9c9-143">.NET Standard 會取代[可攜式類別庫 (PCL)](./cross-platform/cross-platform-development-with-the-portable-class-library.md)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-143">.NET Standard is the replacement for [Portable Class Libraries (PCL)](./cross-platform/cross-platform-development-with-the-portable-class-library.md).</span></span> <span data-ttu-id="4b9c9-144">.NET Standard 可透過策劃標準 BCL，進而在 .NET 實作之間建立更高的一致性，來改善建立可攜式程式庫的體驗。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-144">The .NET Standard improves on the experience of creating portable libraries by curating a standard BCL and establishing greater uniformity across .NET implementations as a result.</span></span> <span data-ttu-id="4b9c9-145">以 .NET Standard 為目標的程式庫是 PCL 或「.NET Standard 型 PCL」。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-145">A library that targets .NET Standard is a PCL or a ".NET Standard-based PCL".</span></span> <span data-ttu-id="4b9c9-146">現有的 PCL 是「設定檔型 PCL」。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-146">Existing PCLs are "profile-based PCLs".</span></span>

<span data-ttu-id="4b9c9-147">.NET Standard 和 PCL 設定檔是為了類似的目的而建立，但也有幾點重要的不同之處。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-147">.NET Standard and PCL profiles were created for similar purposes but also differ in key ways.</span></span>

<span data-ttu-id="4b9c9-148">相似之處：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-148">Similarities:</span></span>

- <span data-ttu-id="4b9c9-149">定義可用於二進位字碼共用的 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-149">Defines APIs that can be used for binary code sharing.</span></span>

<span data-ttu-id="4b9c9-150">不同之處：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-150">Differences:</span></span>

- <span data-ttu-id="4b9c9-151">.NET Standard 是一組經過策劃的 API，而 PCL 設定檔則是由現有平台的交集所定義。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-151">.NET Standard is a curated set of APIs, while PCL profiles are defined by intersections of existing platforms.</span></span>
- <span data-ttu-id="4b9c9-152">.NET Standard 是以線性方式控制版本，而 PCL 設定檔則不是。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-152">.NET Standard linearly versions, while PCL profiles do not.</span></span>
- <span data-ttu-id="4b9c9-153">PCL 設定檔代表 Microsoft 平台，而 .NET Standard 則無從驗證平台。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-153">PCL profiles represents Microsoft platforms while the .NET Standard is agnostic to platform.</span></span>

## <a name="specification"></a><span data-ttu-id="4b9c9-154">規格</span><span class="sxs-lookup"><span data-stu-id="4b9c9-154">Specification</span></span>

<span data-ttu-id="4b9c9-155">.NET Standard 規格是一組標準化的 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-155">The .NET Standard specification is a standardized set of APIs.</span></span> <span data-ttu-id="4b9c9-156">此規格是由 .NET 實作者所維護，具體而言即 Microsoft (包括 .NET Framework、.NET Core 和 Mono) 和 Unity。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-156">The specification is maintained by .NET implementors, specifically Microsoft (includes .NET Framework, .NET Core and Mono) and Unity.</span></span> <span data-ttu-id="4b9c9-157">透過 [GitHub](https://github.com/dotnet/standard) 建立新的 .NET Standard 版本時，會使用公開回饋程序。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-157">A public feedback process is used as part of establishing new .NET Standard versions through [GitHub](https://github.com/dotnet/standard).</span></span>

### <a name="official-artifacts"></a><span data-ttu-id="4b9c9-158">正式成品</span><span class="sxs-lookup"><span data-stu-id="4b9c9-158">Official artifacts</span></span>

<span data-ttu-id="4b9c9-159">正式規格是一組定義 API 的 .cs 檔案，這些 API 是標準的一部分。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-159">The official specification is a set of .cs files that define the APIs that are part of the standard.</span></span> <span data-ttu-id="4b9c9-160">[dotnet/standard 存放庫](https://github.com/dotnet/corefx/tree/master/src)中的 [ref 目錄](https://github.com/dotnet/standard/tree/master/netstandard/ref)定義 .NET Standard API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-160">The [ref directory](https://github.com/dotnet/standard/tree/master/netstandard/ref) in the [dotnet/standard repository](https://github.com/dotnet/corefx/tree/master/src) defines the .NET Standard APIs.</span></span>

<span data-ttu-id="4b9c9-161">[NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) 中繼套件 ([原始檔](https://github.com/dotnet/standard/blob/master/netstandard/pkg/NETStandard.Library.dependencies.props)) 描述定義 (部分) 一或多個 .NET Standard 版本的程式庫集合。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-161">The [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library) metapackage ([source](https://github.com/dotnet/standard/blob/master/netstandard/pkg/NETStandard.Library.dependencies.props)) describes the set of libraries that define (in part) one or more .NET Standard versions.</span></span>

<span data-ttu-id="4b9c9-162">System.Runtime 等指定元件描述：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-162">A given component, like System.Runtime, describes:</span></span>

- <span data-ttu-id="4b9c9-163">.NET Standard 的組件 (僅限其範圍)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-163">Part of .NET Standard (just its scope).</span></span>
- <span data-ttu-id="4b9c9-164">適用於該範圍的多個 .NET Standard 版本。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-164">Multiple versions of .NET Standard, for that scope.</span></span>

<span data-ttu-id="4b9c9-165">為了更方便閱讀及支援特定開發人員案例 (例如使用編譯器)，已提供衍生成品。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-165">Derivative artifacts are provided to enable more convenient reading and to enable certain developer scenarios (for example, using a compiler).</span></span>

- [<span data-ttu-id="4b9c9-166">Markdown 中的 API 清單</span><span class="sxs-lookup"><span data-stu-id="4b9c9-166">API list in markdown</span></span>](https://github.com/dotnet/standard/tree/master/docs/versions)
- <span data-ttu-id="4b9c9-167">以 [NuGet 套件](../core/packages.md)散發並由 [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/) 中繼套件參考的參考組件。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-167">Reference assemblies, distributed as [NuGet packages](../core/packages.md) and referenced by the [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/) metapackage.</span></span>

### <a name="package-representation"></a><span data-ttu-id="4b9c9-168">封裝表示</span><span class="sxs-lookup"><span data-stu-id="4b9c9-168">Package representation</span></span>

<span data-ttu-id="4b9c9-169">.NET Standard 參考組件的主要散發工具是 [NuGet 套件](../core/packages.md)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-169">The primary distribution vehicle for the .NET Standard reference assemblies is [NuGet packages](../core/packages.md).</span></span> <span data-ttu-id="4b9c9-170">您可以根據每個 .NET 實作，以各種適當的方式來提供實作。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-170">Implementations will be delivered in a variety of ways, appropriate for each .NET implementation.</span></span>

<span data-ttu-id="4b9c9-171">NuGet 套件是以一個或多個[架構](frameworks.md)為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-171">NuGet packages target one or more [frameworks](frameworks.md).</span></span> <span data-ttu-id="4b9c9-172">.NET Standard 套件是以 ".NET Standard" 架構為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-172">The .NET Standard packages target the ".NET Standard" framework.</span></span> <span data-ttu-id="4b9c9-173">您可以使用 `netstandard` [Compact TFM](frameworks.md) (例如 `netstandard1.4`) 將 .NET Standard 程式庫設為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-173">You can target the .NET Standard Framework using the `netstandard` [compact TFM](frameworks.md) (for example, `netstandard1.4`).</span></span> <span data-ttu-id="4b9c9-174">要在多個執行階段上執行的程式庫應以此架構為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-174">Libraries that are intended to run on multiple runtimes should target this framework.</span></span> 

<span data-ttu-id="4b9c9-175">`NETStandard.Library` 中繼套件會參考定義 .NET Standard 的一組完整 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-175">The `NETStandard.Library` metapackage references the complete set of NuGet packages that define .NET Standard.</span></span>  <span data-ttu-id="4b9c9-176">若要將 `netstandard` 設為目標，最常見方式是參考這個中繼套件。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-176">The most common way to target `netstandard` is by referencing this metapackage.</span></span> <span data-ttu-id="4b9c9-177">它描述大約 40 種定義 .NET Standard 的 .NET 程式庫和相關 API，並提供其存取權。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-177">It describes and provides access to the ~40 .NET libraries and associated APIs that define .NET Standard.</span></span> <span data-ttu-id="4b9c9-178">您可以參考目標為 `netstandard` 的其他套件，以存取其他 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-178">You can reference additional packages that target `netstandard` to get access to additional APIs.</span></span> 

### <a name="versioning"></a><span data-ttu-id="4b9c9-179">版本控制</span><span class="sxs-lookup"><span data-stu-id="4b9c9-179">Versioning</span></span>

<span data-ttu-id="4b9c9-180">此規格不是單一的，而是一組以累加方式擴充並以線性方式控制版本的 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-180">The specification is not singular, but an incrementally growing and linearly versioned set of APIs.</span></span> <span data-ttu-id="4b9c9-181">此標準的第一個版本會建立一組基準 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-181">The first version of the standard establishes a baseline set of APIs.</span></span> <span data-ttu-id="4b9c9-182">後續版本會新增 API，並繼承舊版所定義的 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-182">Subsequent versions add APIs and inherit APIs defined by previous versions.</span></span> <span data-ttu-id="4b9c9-183">沒有任何既定的佈建可從標準中移除 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-183">There is no established provision for removing APIs from the standard.</span></span>

<span data-ttu-id="4b9c9-184">.NET Standard 並非專屬於任何一個 .NET 實作，也不符合任何這些執行階段的版本配置。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-184">.NET Standard is not specific to any one .NET implementation, nor does it match the versioning scheme of any of those runtimes.</span></span>

<span data-ttu-id="4b9c9-185">新增至任何實作 (例如 .NET Framework、.NET Core 和 Mono) 的 API 都可視為要新增至規格的候選項目，尤其是如果本質上要作為基礎的 API。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-185">APIs added to any of the implementations (such as, .NET Framework, .NET Core and Mono) can be considered as candidates to add to the specification, particularly if they are thought to be fundamental in nature.</span></span> <span data-ttu-id="4b9c9-186">新的 [.NET Standard 版本](https://github.com/dotnet/standard/blob/master/docs/versions.md)是根據 .NET 實作版本所建立，可讓您以來自 .NET Standard PCL 的新 API 為目標。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-186">New [versions of .NET Standard](https://github.com/dotnet/standard/blob/master/docs/versions.md) are created based on .NET implementation releases, enabling you to target new APIs from a .NET Standard PCL.</span></span> <span data-ttu-id="4b9c9-187">如需版本控制機制的詳細資訊，請參閱 [.NET Core 版本控制](../core/versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-187">The versioning mechanics are described in more detail in [.NET Core Versioning](../core/versions/index.md).</span></span>

<span data-ttu-id="4b9c9-188">.NET Standard 版本控制對於使用至關重要。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-188">.NET Standard versioning is important for usage.</span></span> <span data-ttu-id="4b9c9-189">指定 .NET Standard 版本之後，您可以使用以相同版本或更舊版本為目標的程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-189">Given a .NET Standard version, you can use libraries that target that same or lower version.</span></span> <span data-ttu-id="4b9c9-190">下列方法描述使用 .NET Standard PCL (專門用於 .NET Standard 目標設定) 的工作流程。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-190">The following approach describes the workflow for using .NET Standard PCLs, specific to .NET Standard targeting.</span></span>

- <span data-ttu-id="4b9c9-191">選取要用於 PCL 的 .NET Standard 版本。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-191">Select a .NET Standard version to use for your PCL.</span></span>
- <span data-ttu-id="4b9c9-192">使用相依於相同 .NET Standard 版本或更舊版本的程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-192">Use libraries that depend on the same .NET Standard version or lower.</span></span>
- <span data-ttu-id="4b9c9-193">如果您發現有程式庫相依於更新的 .NET Standard 版本，就需要採用該相同的版本，或決定不要使用該程式庫。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-193">If you find a library that depends on a higher .NET Standard version, you either need to adopt that same version or decide not to use that library.</span></span>

### <a name="pcl-compatibility"></a><span data-ttu-id="4b9c9-194">PCL 相容性</span><span class="sxs-lookup"><span data-stu-id="4b9c9-194">PCL compatibility</span></span>

<span data-ttu-id="4b9c9-195">.NET Standard 與 PCL 設定檔子集相容。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-195">.NET Standard is compatible with a subset of PCL profiles.</span></span> <span data-ttu-id="4b9c9-196">.NET Standard Library 1.0、1.1 和 1.2 會各自與一組 PCL 設定檔重疊。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-196">.NET Standard 1.0, 1.1 and 1.2 each overlap with a set of PCL profiles.</span></span> <span data-ttu-id="4b9c9-197">建立此重疊的原因有兩個：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-197">This overlap was created for two reasons:</span></span>

- <span data-ttu-id="4b9c9-198">可讓 .NET Standard 型 PCL 參考設定檔型 PCL。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-198">Enable .NET Standard-based PCLs to reference profile-based PCLs.</span></span>
- <span data-ttu-id="4b9c9-199">可將設定檔型 PCL 封裝成 .NET Standard 型 PCL。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-199">Enable profile-based PCLs to be packaged as .NET Standard-based PCLs.</span></span>

<span data-ttu-id="4b9c9-200">[Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) NuGet 套件提供設定檔型 PCL 相容性。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-200">Profile-based PCL compatibility is provided by the [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) NuGet package.</span></span> <span data-ttu-id="4b9c9-201">參考包含設定檔型 PCL 的 NuGet 套件時需要此相依性。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-201">This dependency is required when referencing NuGet packages that contain profile-based PCLs.</span></span>

<span data-ttu-id="4b9c9-202">封裝成 `netstandard` 的設定檔型 PCL，會比一般封裝的設定檔型 PCL 更容易使用。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-202">Profile-based PCLs packaged as `netstandard` are easier to consume than typically packaged profile-based PCLs.</span></span> <span data-ttu-id="4b9c9-203">現有的使用者可以使用 `netstandard` 封裝。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-203">`netstandard` packaging is compatible with existing users.</span></span>

<span data-ttu-id="4b9c9-204">您會看到與 .NET Standard 相容的 PCL 設定檔集合：</span><span class="sxs-lookup"><span data-stu-id="4b9c9-204">You can see the set of PCL profiles that are compatible with the .NET Standard:</span></span> 

| <span data-ttu-id="4b9c9-205">PCL 設定檔</span><span class="sxs-lookup"><span data-stu-id="4b9c9-205">PCL Profile</span></span> | <span data-ttu-id="4b9c9-206">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4b9c9-206">.NET Standard</span></span> | <span data-ttu-id="4b9c9-207">PCL 平台</span><span class="sxs-lookup"><span data-stu-id="4b9c9-207">PCL Platforms</span></span>
|:-----------:|:-------------:|------------------------------------------------------------------------------
| <span data-ttu-id="4b9c9-208">Profile7</span><span class="sxs-lookup"><span data-stu-id="4b9c9-208">Profile7</span></span>    | <span data-ttu-id="4b9c9-209">1.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-209">1.1</span></span>           | <span data-ttu-id="4b9c9-210">.NET Framework 4.5、Windows 8</span><span class="sxs-lookup"><span data-stu-id="4b9c9-210">.NET Framework 4.5, Windows 8</span></span>
| <span data-ttu-id="4b9c9-211">Profile31</span><span class="sxs-lookup"><span data-stu-id="4b9c9-211">Profile31</span></span>   | <span data-ttu-id="4b9c9-212">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-212">1.0</span></span>           | <span data-ttu-id="4b9c9-213">Windows 8.1、Windows Phone Silverlight 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-213">Windows 8.1, Windows Phone Silverlight 8.1</span></span>
| <span data-ttu-id="4b9c9-214">Profile32</span><span class="sxs-lookup"><span data-stu-id="4b9c9-214">Profile32</span></span>   | <span data-ttu-id="4b9c9-215">1.2</span><span class="sxs-lookup"><span data-stu-id="4b9c9-215">1.2</span></span>           | <span data-ttu-id="4b9c9-216">Windows 8.1、Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-216">Windows 8.1, Windows Phone 8.1</span></span>
| <span data-ttu-id="4b9c9-217">Profile44</span><span class="sxs-lookup"><span data-stu-id="4b9c9-217">Profile44</span></span>   | <span data-ttu-id="4b9c9-218">1.2</span><span class="sxs-lookup"><span data-stu-id="4b9c9-218">1.2</span></span>           | <span data-ttu-id="4b9c9-219">.NET Framework 4.5.1、Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-219">.NET Framework 4.5.1, Windows 8.1</span></span>
| <span data-ttu-id="4b9c9-220">Profile49</span><span class="sxs-lookup"><span data-stu-id="4b9c9-220">Profile49</span></span>   | <span data-ttu-id="4b9c9-221">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-221">1.0</span></span>           | <span data-ttu-id="4b9c9-222">.NET Framework 4.5、Windows Phone Silverlight 8</span><span class="sxs-lookup"><span data-stu-id="4b9c9-222">.NET Framework 4.5, Windows Phone Silverlight 8</span></span>
| <span data-ttu-id="4b9c9-223">Profile78</span><span class="sxs-lookup"><span data-stu-id="4b9c9-223">Profile78</span></span>   | <span data-ttu-id="4b9c9-224">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-224">1.0</span></span>           | <span data-ttu-id="4b9c9-225">.NET Framework 4.5、Windows 8, Windows Phone Silverlight 8</span><span class="sxs-lookup"><span data-stu-id="4b9c9-225">.NET Framework 4.5, Windows 8, Windows Phone Silverlight 8</span></span>
| <span data-ttu-id="4b9c9-226">Profile84</span><span class="sxs-lookup"><span data-stu-id="4b9c9-226">Profile84</span></span>   | <span data-ttu-id="4b9c9-227">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-227">1.0</span></span>           | <span data-ttu-id="4b9c9-228">Windows Phone 8.1、Windows Phone Silverlight 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-228">Windows Phone 8.1, Windows Phone Silverlight 8.1</span></span>
| <span data-ttu-id="4b9c9-229">Profile111</span><span class="sxs-lookup"><span data-stu-id="4b9c9-229">Profile111</span></span>  | <span data-ttu-id="4b9c9-230">1.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-230">1.1</span></span>           | <span data-ttu-id="4b9c9-231">.NET Framework 4.5、Windows 8, Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-231">.NET Framework 4.5, Windows 8, Windows Phone 8.1</span></span>
| <span data-ttu-id="4b9c9-232">Profile151</span><span class="sxs-lookup"><span data-stu-id="4b9c9-232">Profile151</span></span>  | <span data-ttu-id="4b9c9-233">1.2</span><span class="sxs-lookup"><span data-stu-id="4b9c9-233">1.2</span></span>           | <span data-ttu-id="4b9c9-234">.NET Framework 4.5.1、Windows 8.1、Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-234">.NET Framework 4.5.1, Windows 8.1, Windows Phone 8.1</span></span>
| <span data-ttu-id="4b9c9-235">Profile157</span><span class="sxs-lookup"><span data-stu-id="4b9c9-235">Profile157</span></span>  | <span data-ttu-id="4b9c9-236">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-236">1.0</span></span>           | <span data-ttu-id="4b9c9-237">Windows 8.1、Windows Phone 8.1、Windows Phone Silverlight 8.1</span><span class="sxs-lookup"><span data-stu-id="4b9c9-237">Windows 8.1, Windows Phone 8.1, Windows Phone Silverlight 8.1</span></span>
| <span data-ttu-id="4b9c9-238">Profile259</span><span class="sxs-lookup"><span data-stu-id="4b9c9-238">Profile259</span></span>  | <span data-ttu-id="4b9c9-239">1.0</span><span class="sxs-lookup"><span data-stu-id="4b9c9-239">1.0</span></span>           | <span data-ttu-id="4b9c9-240">.NET Framework 4.5、Windows 8、Windows Phone 8.1、Windows Phone Silverlight 8</span><span class="sxs-lookup"><span data-stu-id="4b9c9-240">.NET Framework 4.5, Windows 8, Windows Phone 8.1, Windows Phone Silverlight 8</span></span>


## <a name="targeting-net-standard"></a><span data-ttu-id="4b9c9-241">以 .NET Standard 為目標</span><span class="sxs-lookup"><span data-stu-id="4b9c9-241">Targeting .NET Standard</span></span>

<span data-ttu-id="4b9c9-242">您可以搭配使用 `netstandard` 架構和 NETStandard.Library 中繼套件，來[建置 .NET Standard 程式庫](../core/tutorials/libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-242">You can [build .NET Standard Libraries](../core/tutorials/libraries.md) using a combination of the `netstandard` framework and the NETStandard.Library metapackage.</span></span> <span data-ttu-id="4b9c9-243">您可以查看[使用 .NET Core 工具將 .NET Standard 設為目標](../core/packages.md)的範例。</span><span class="sxs-lookup"><span data-stu-id="4b9c9-243">You can see examples of [targeting the .NET Standard with .NET Core tools](../core/packages.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4b9c9-244">請參閱</span><span class="sxs-lookup"><span data-stu-id="4b9c9-244">See also</span></span>
[<span data-ttu-id="4b9c9-245">.NET Standard 版本</span><span class="sxs-lookup"><span data-stu-id="4b9c9-245">.NET Standard Versions</span></span>](https://github.com/dotnet/standard/blob/master/docs/versions.md)
