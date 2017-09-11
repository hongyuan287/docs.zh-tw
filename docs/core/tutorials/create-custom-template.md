---
title: "建立 dotnet new 的自訂範本"
description: "了解如何在此好玩的教學課程中建立 dotnet new 命令的自訂範本。"
keywords: ".NET, .NET Core, 範本, 建立範本, 教學課程, dotnet new"
author: guardrex
ms.author: mairaw
ms.date: 08/12/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 519b910a-6efe-4394-9b81-0546aa3e7462
ms.translationtype: HT
ms.sourcegitcommit: c58ed1b3c09f1e358d0b66f6cf7186821601fd69
ms.openlocfilehash: e31977c511f18737aef673c78a3e295d7c24782f
ms.contentlocale: zh-tw
ms.lasthandoff: 08/12/2017

---

# <a name="create-a-custom-template-for-dotnet-new"></a><span data-ttu-id="2a4d0-104">建立 dotnet new 的自訂範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-104">Create a custom template for dotnet new</span></span>

<span data-ttu-id="2a4d0-105">本教學課程會示範如何：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-105">This tutorial shows you how to:</span></span>

- <span data-ttu-id="2a4d0-106">從現有的專案或新的主控台應用程式專案建立基本範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-106">Create a basic template from an existing project or a new console app project.</span></span>
- <span data-ttu-id="2a4d0-107">封裝範本，以在 nuget.org 或從本機 *nupkg* 檔案發佈。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-107">Pack the template for distribution at nuget.org or from a local *nupkg* file.</span></span>
- <span data-ttu-id="2a4d0-108">從 nuget.org (本機 *nupkg* 檔案) 或本機檔案系統安裝範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-108">Install the template from nuget.org, a local *nupkg* file, or the local file system.</span></span>
- <span data-ttu-id="2a4d0-109">解除安裝範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-109">Uninstall the template.</span></span>

<span data-ttu-id="2a4d0-110">如果您偏好使用完整範例來進行教學課程，請下載[範例專案範本](https://github.com/dotnet/dotnet-template-samples/tree/master/16-nuget-package)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-110">If you prefer to proceed through the tutorial with a complete sample, download the [sample project template](https://github.com/dotnet/dotnet-template-samples/tree/master/16-nuget-package).</span></span> <span data-ttu-id="2a4d0-111">範例範本是專為 NuGet 發佈所設定。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-111">The sample template is configured for NuGet distribution.</span></span>

<span data-ttu-id="2a4d0-112">如果您希望使用下載的範例和檔案系統發佈，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-112">If you wish to use the downloaded sample with file system distribution, do the following:</span></span>

- <span data-ttu-id="2a4d0-113">將範例的 *content* 資料夾內容上移一層到 *GarciaSoftware.ConsoleTemplate.CSharp* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-113">Move the contents of the *content* folder of the sample up one level into the *GarciaSoftware.ConsoleTemplate.CSharp* folder.</span></span>
- <span data-ttu-id="2a4d0-114">刪除空白的 *content* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-114">Delete the empty *content* folder.</span></span>
- <span data-ttu-id="2a4d0-115">刪除 *nuspec* 檔案。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-115">Delete the *nuspec* file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a4d0-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="2a4d0-116">Prerequisites</span></span>

- <span data-ttu-id="2a4d0-117">安裝 [.NET Core 2.0 SDK](https://www.microsoft.com/net/core) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-117">Install the [.NET Core 2.0 SDK](https://www.microsoft.com/net/core) or later versions.</span></span>
- <span data-ttu-id="2a4d0-118">閱讀參考主題 [dotnet new 的自訂範本](../tools/custom-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-118">Read the reference topic [Custom templates for dotnet new](../tools/custom-templates.md).</span></span>

## <a name="create-a-template-from-a-project"></a><span data-ttu-id="2a4d0-119">從專案建立範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-119">Create a template from a project</span></span>

<span data-ttu-id="2a4d0-120">使用您已確認編譯和執行的現有專案，或在硬碟的資料夾中建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-120">Use an existing project that you've confirmed it compiles and runs, or create a new console app project in a folder on your hard drive.</span></span> <span data-ttu-id="2a4d0-121">本教學課程假設專案資料夾的名稱為 *GarciaSoftware.ConsoleTemplate.CSharp*，儲存在使用者設定檔的 *Documents/Templates*。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-121">This tutorial assumes that the name of the project folder is *GarciaSoftware.ConsoleTemplate.CSharp* stored at *Documents/Templates* in the user's profile.</span></span> <span data-ttu-id="2a4d0-122">教學課程專案範本名稱的格式為 \<公司名稱>.\<範本類型>.\<程式設計語言>，但是您可以依喜好隨意命名您的專案與範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-122">The tutorial project template name is in the format *\<Company Name>.\<Template Type>.\<Programming Language>*, but you're free to name your project and template anything you wish.</span></span>

1. <span data-ttu-id="2a4d0-123">將資料夾新增至 *.template.config* 專案的根目錄。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-123">Add a folder to the root of the project named *.template.config*.</span></span>
1. <span data-ttu-id="2a4d0-124">在 *.template.config* 資料夾中建立 *template.json* 檔案，以設定您的範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-124">Inside the *.template.config* folder, create a *template.json* file to configure your template.</span></span> <span data-ttu-id="2a4d0-125">如需 *template.json* 檔案的詳細資訊和成員定義，請參閱 [dotnet new 的自訂範本](../tools/custom-templates.md#templatejson)主題和 [JSON 結構描述存放區的 *template.json* 結構描述](http://json.schemastore.org/template)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-125">For more information and member definitions for the *template.json* file, see the [Custom templates for dotnet new](../tools/custom-templates.md#templatejson) topic and the [*template.json* schema at the JSON Schema Store](http://json.schemastore.org/template).</span></span>

```json
{
    "$schema": "http://json.schemastore.org/template",
    "author": "Catalina Garcia",
    "classifications": [ "Common", "Console" ],
    "identity": "GarciaSoftware.ConsoleTemplate.CSharp",
    "name": "Garcia Software Console Application",
    "shortName": "garciaconsole"
}
```

<span data-ttu-id="2a4d0-126">已完成範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-126">The template is finished.</span></span> <span data-ttu-id="2a4d0-127">此時，您有兩個範本發佈的選項。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-127">At this point, you have two options for template distribution.</span></span> <span data-ttu-id="2a4d0-128">若要繼續本教學課程，請在兩個路徑中選擇其中之一：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-128">To continue this tutorial, choose one path or the other:</span></span>

1. <span data-ttu-id="2a4d0-129">[NuGet 發佈](#use-nuget-distribution)：從 NuGet 或從本機 *nupkg* 檔案安裝範本，並使用已安裝的範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-129">[NuGet distribution](#use-nuget-distribution): install the template from NuGet or from the local *nupkg* file, and use the installed template.</span></span>
2. <span data-ttu-id="2a4d0-130">[檔案系統發佈](#use-file-system-distribution)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-130">[File system distribution](#use-file-system-distribution).</span></span>

## <a name="use-nuget-distribution"></a><span data-ttu-id="2a4d0-131">使用 NuGet 發佈</span><span class="sxs-lookup"><span data-stu-id="2a4d0-131">Use NuGet Distribution</span></span>

### <a name="pack-the-template-into-a-nuget-package"></a><span data-ttu-id="2a4d0-132">將範本封裝至 NuGet 套件中</span><span class="sxs-lookup"><span data-stu-id="2a4d0-132">Pack the template into a NuGet package</span></span>

1. <span data-ttu-id="2a4d0-133">建立 NuGet 套件的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-133">Create a folder for the NuGet package.</span></span> <span data-ttu-id="2a4d0-134">教學課程中使用 *GarciaSoftware.ConsoleTemplate.CSharp* 資料夾名稱，並在使用者設定檔的 *Documents/NuGetTemplates* 資料夾中建立此資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-134">For the tutorial, the folder name *GarciaSoftware.ConsoleTemplate.CSharp* is used, and the folder is created inside a *Documents/NuGetTemplates* folder in the user's profile.</span></span> <span data-ttu-id="2a4d0-135">在新的範本資料夾內建立名為「內容」的資料夾，保留專案檔。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-135">Create a folder named *content* inside of the new template folder to hold the project files.</span></span>
1. <span data-ttu-id="2a4d0-136">將專案資料夾的內容以及其 *.template.config/template.json* 檔案複製到您建立的 *content* 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-136">Copy the contents of your project folder, together with its *.template.config/template.json* file, into the *content* folder you created.</span></span>
1. <span data-ttu-id="2a4d0-137">在 *content* 資料夾的旁邊，新增 [*nuspec* 檔案](/nuget/create-packages/creating-a-package)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-137">Next to the *content* folder, add a [*nuspec* file](/nuget/create-packages/creating-a-package).</span></span> <span data-ttu-id="2a4d0-138">nuspec 檔案是 XML 資訊清單檔案，描述套件的內容及驅動建立 NuGet 套件的程序。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-138">The nuspec file is an XML manifest file that describes a package's contents and drives the process of creating the NuGet package.</span></span>
   
   ![目錄結構顯示 NuGet 套件的配置](./media/create-custom-template/nugetdirectorylayout.png)

1. <span data-ttu-id="2a4d0-140">在 *nuspec* 檔案的 **\<packageTypes>** 項目內，包含 `name` 屬性值為 `Template` 的 **\<packageType>** 項目。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-140">Inside of a **\<packageTypes>** element in the *nuspec* file, include a **\<packageType>** element with a `name` attribute value of `Template`.</span></span> <span data-ttu-id="2a4d0-141">*content* 資料夾和 *nuspec* 檔案都應該位於相同的目錄中。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-141">Both the *content* folder and the *nuspec* file should reside in the same directory.</span></span> <span data-ttu-id="2a4d0-142">下表顯示將範本製作為 NuGet 套件所需之最小的 *nuspec* 檔案項目。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-142">The table shows the minimum *nuspec* file elements required to produce a template as a NuGet package.</span></span>

   | <span data-ttu-id="2a4d0-143">項目</span><span class="sxs-lookup"><span data-stu-id="2a4d0-143">Element</span></span>            | <span data-ttu-id="2a4d0-144">類型</span><span class="sxs-lookup"><span data-stu-id="2a4d0-144">Type</span></span>   | <span data-ttu-id="2a4d0-145">說明</span><span class="sxs-lookup"><span data-stu-id="2a4d0-145">Description</span></span> |
   | ------------------ | ------ | ----------- |
   | <span data-ttu-id="2a4d0-146">**\<作者>**</span><span class="sxs-lookup"><span data-stu-id="2a4d0-146">**\<authors>**</span></span>     | <span data-ttu-id="2a4d0-147">字串</span><span class="sxs-lookup"><span data-stu-id="2a4d0-147">string</span></span> | <span data-ttu-id="2a4d0-148">以逗號分隔的套件作者清單，與 nuget.org 上的設定檔名稱相符。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-148">A comma-separated list of packages authors, matching the profile names on nuget.org.</span></span> <span data-ttu-id="2a4d0-149">這些作者會顯示在 nuget.org 的 NuGet 組件庫中，並用來交互參照相同作者的其他套件。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-149">Authors are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
   | <span data-ttu-id="2a4d0-150">**\<描述>**</span><span class="sxs-lookup"><span data-stu-id="2a4d0-150">**\<description>**</span></span> | <span data-ttu-id="2a4d0-151">字串</span><span class="sxs-lookup"><span data-stu-id="2a4d0-151">string</span></span> | <span data-ttu-id="2a4d0-152">UI 顯示中的套件詳細描述。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-152">A long description of the package for UI display.</span></span> |
   | <span data-ttu-id="2a4d0-153">**\<識別碼>**</span><span class="sxs-lookup"><span data-stu-id="2a4d0-153">**\<id>**</span></span>          | <span data-ttu-id="2a4d0-154">字串</span><span class="sxs-lookup"><span data-stu-id="2a4d0-154">string</span></span> | <span data-ttu-id="2a4d0-155">不區分大小寫的套件識別碼，在整個 nuget.org 或套件所在的任何組件庫都必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-155">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package will reside in.</span></span> <span data-ttu-id="2a4d0-156">識別碼可能不包含對 URL 而言無效的空格或字元，而且通常會遵循 .NET 命名空間規則。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-156">IDs may not contain spaces or characters that are not valid for a URL and generally follow .NET namespace rules.</span></span> <span data-ttu-id="2a4d0-157">如需指導方針，請參閱[選擇唯一的套件識別碼並設定版本號碼](/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-157">See [Choosing a unique package identifier and setting the version number](/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
   | <span data-ttu-id="2a4d0-158">**\<packageType>**</span><span class="sxs-lookup"><span data-stu-id="2a4d0-158">**\<packageType>**</span></span> | <span data-ttu-id="2a4d0-159">字串</span><span class="sxs-lookup"><span data-stu-id="2a4d0-159">string</span></span> | <span data-ttu-id="2a4d0-160">將此項目放在 **\<metadata>** 項目中的 **\<packageTypes>** 項目內。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-160">Place this element inside a **\<packageTypes>** element among the **\<metadata>** elements.</span></span> <span data-ttu-id="2a4d0-161">將 **\<packageType>** 項目的 `name` 屬性設定為 `Template`。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-161">Set the `name` attribute of the **\<packageType>** element to `Template`.</span></span> |
   | <span data-ttu-id="2a4d0-162">**\<版本>**</span><span class="sxs-lookup"><span data-stu-id="2a4d0-162">**\<version>**</span></span>     | <span data-ttu-id="2a4d0-163">字串</span><span class="sxs-lookup"><span data-stu-id="2a4d0-163">string</span></span> | <span data-ttu-id="2a4d0-164">套件版本，遵循 major.minor.patch 模式。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-164">The version of the package, following the major.minor.patch pattern.</span></span> <span data-ttu-id="2a4d0-165">版本號碼可以包含預先發行版本的後置詞，如[預先發行版本](/nuget/create-packages/prerelease-packages#semantic-versioning)中所述。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-165">Version numbers may include a pre-release suffix as described in [Pre-release versions](/nuget/create-packages/prerelease-packages#semantic-versioning).</span></span> |

   <span data-ttu-id="2a4d0-166">請參閱 [.nuspec 參考](/nuget/schema/nuspec)以取得完整的 *nuspec* 檔案結構描述。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-166">See the [.nuspec reference](/nuget/schema/nuspec) for the complete *nuspec* file schema.</span></span>

   <span data-ttu-id="2a4d0-167">教學課程的 *nuspec* 檔案名為 *GarciaSoftware.ConsoleTemplate.CSharp.nuspec*，且包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-167">The *nuspec* file for the tutorial is named *GarciaSoftware.ConsoleTemplate.CSharp.nuspec* and contains the following content:</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
     <metadata>
       <id>GarciaSoftware.ConsoleTemplate.CSharp</id>
       <version>1.0.0</version>
       <description>
         Creates the Garcia Software console app.
       </description>
       <authors>Catalina Garcia</authors>
       <packageTypes>
         <packageType name="Template" />
       </packageTypes>
     </metadata>
   </package>
   ```

1. <span data-ttu-id="2a4d0-168">使用 `nuget pack <PATH_TO_NUSPEC_FILE>` 命令[建立套件](/nuget/create-packages/creating-a-package#creating-the-package)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-168">[Create the package](/nuget/create-packages/creating-a-package#creating-the-package) using the `nuget pack <PATH_TO_NUSPEC_FILE>` command.</span></span> <span data-ttu-id="2a4d0-169">下列命令假設，保存 NuGet 資產的資料夾位於 *C:/Users/\<使用者>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp/*。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-169">The following command assumes that the folder that holds the NuGet assets is at *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp/*.</span></span> <span data-ttu-id="2a4d0-170">但無論資料夾放在系統上的任何位置，`nuget pack` 命令都接受 *nuspec* 檔案的路徑：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-170">But wherever you place the folder on your system, the `nuget pack` command accepts the path to the *nuspec* file:</span></span>

   ```console
   nuget pack C:/Users/<USER>/Documents/NuGetTemplates/GarciaSoftware.ConsoleTemplate.CSharp/GarciaSoftware.ConsoleTemplate.CSharp.nuspec
   ```

### <a name="publishing-the-package-to-nugetorg"></a><span data-ttu-id="2a4d0-171">將套件發佈至 nuget.org</span><span class="sxs-lookup"><span data-stu-id="2a4d0-171">Publishing the package to nuget.org</span></span>

<span data-ttu-id="2a4d0-172">若要發佈 NuGet 套件，請遵循[建立和發佈套件](/nuget/quickstart/create-and-publish-a-package#publish-the-package)主題中的指示。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-172">To publish a NuGet package, follow the instructions in the [Create and publish a package](/nuget/quickstart/create-and-publish-a-package#publish-the-package) topic.</span></span> <span data-ttu-id="2a4d0-173">不過，我們建議您不要將教學課程的範本發佈至 NuGet，因為它一旦發佈即永不刪除，只能取消列入。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-173">However, we recommend that you don't publish the tutorial template to NuGet as it can never be deleted once published, only delisted.</span></span> <span data-ttu-id="2a4d0-174">既然已有 *nupkg* 檔案形式的 NuGet 套件，建議您遵循下列指示直接從本機 *nupkg* 檔案安裝範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-174">Now that you have the NuGet package in the form of a *nupkg* file, we suggest that you follow the instructions below to install the template directly from the local *nupkg* file.</span></span>

### <a name="install-the-template-from-a-nuget-package"></a><span data-ttu-id="2a4d0-175">從 NuGet 套件安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-175">Install the template from a NuGet package</span></span>

#### <a name="install-the-template-from-the-local-nupkg-file"></a><span data-ttu-id="2a4d0-176">從本機 *nupkg* 檔案安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-176">Install the template from the local *nupkg* file</span></span>

<span data-ttu-id="2a4d0-177">若要從您製作的 *nupkg* 檔案安裝範本，請使用 `dotnet new` 命令搭配 `-i|--install` 選項，然後提供 *nupkg* 檔案的路徑：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-177">To install the template from the *nupkg* file that you produced, use the `dotnet new` command with the `-i|--install` option and provide the path to the *nupkg* file:</span></span>

```console
dotnet new -i C:/Users/<USER>/GarciaSoftware.ConsoleTemplate.CSharp.1.0.0.nupkg
```

#### <a name="install-the-template-from-a-nuget-package-stored-at-nugetorg"></a><span data-ttu-id="2a4d0-178">從儲存在 nuget.org 的 NuGet 套件安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-178">Install the template from a NuGet package stored at nuget.org</span></span>

<span data-ttu-id="2a4d0-179">如果您想要從儲存在 nuget.org 的 NuGet 套件安裝範本，請使用 `dotnet new` 命令搭配 `-i|--install` 選項，並提供 NuGet 套件的名稱：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-179">If you wish to install a template from a NuGet package stored at nuget.org, use the `dotnet new` command with the `-i|--install` option and supply the name of the NuGet package:</span></span>

```console
dotnet new -i GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> <span data-ttu-id="2a4d0-180">範例僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-180">The example is for demonstration purposes only.</span></span> <span data-ttu-id="2a4d0-181">nuget.org 沒有 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 套件，我們也不建議您發佈及使用來自 NuGet 的測試範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-181">There isn't a `GarciaSoftware.ConsoleTemplate.CSharp` NuGet package at nuget.org, and we don't recommend that you publish and consume test templates from NuGet.</span></span> <span data-ttu-id="2a4d0-182">如果您執行命令，不會安裝任何範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-182">If you run the command, no template is installed.</span></span> <span data-ttu-id="2a4d0-183">不過，您可以直接參考本機檔案系統上的 *nupkg* 檔案，安裝尚未發佈至 nuget.org 的範本，如上一節[從本機 nupkg 檔案安裝範本](#install-the-template-from-the-local-nupkg-file)中所示。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-183">However, you can install a template that hasn't been published to nuget.org by referencing the *nupkg* file directly on your local file system as shown in the previous section [Install the template from the local nupkg file](#install-the-template-from-the-local-nupkg-file).</span></span>

<span data-ttu-id="2a4d0-184">如果您想要如何從 nuget.org 的套件安裝範本的即時範例，您可以使用 [NUnit 3 template for dotnet-new](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/) (dotnet-new 的 NUnit 3 範本)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-184">If you'd like a live example of how to install a template from a package at nuget.org, you can use the [NUnit 3 template for dotnet-new](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/).</span></span> <span data-ttu-id="2a4d0-185">此範本會設定專案使用 NUnit 單元測試。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-185">This template sets up a project to use NUnit unit testing.</span></span> <span data-ttu-id="2a4d0-186">使用下列命令來安裝：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-186">Use the following command to install it:</span></span>

```console
dotnet new -i NUnit3.DotNetNew.Template
```

<span data-ttu-id="2a4d0-187">當您列出範本與 `dotnet new -l` 時，您會在範本清單中看到 *NUnit 3 測試專案*的簡短名稱 *nunit*。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-187">When you list the templates with `dotnet new -l`, you see the *NUnit 3 Test Project* with a short name of *nunit* in the template list.</span></span> <span data-ttu-id="2a4d0-188">您已準備好在下一節中使用範本。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-188">You're ready to use the template in the next section.</span></span>

![顯示與其他已安裝範本一起列出之 NUnit 範本的主控台視窗](./media/create-custom-template/nunit1.png)

### <a name="create-a-project-from-the-template"></a><span data-ttu-id="2a4d0-190">從範本建立專案</span><span class="sxs-lookup"><span data-stu-id="2a4d0-190">Create a project from the template</span></span>

<span data-ttu-id="2a4d0-191">從 NuGet 安裝範本之後，從放置範本引擎輸出的目錄執行 `dotnet new <TEMPLATE>` 命令來使用範本 (除非您要使用 `-o|--output` 選項來指定特定的目錄)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-191">After the template is installed from NuGet, use the template by executing the `dotnet new <TEMPLATE>` command from the directory where you want to the template engine's output placed (unless you're using the `-o|--output` option to specify a specific directory).</span></span> <span data-ttu-id="2a4d0-192">如需詳細資訊，請參閱[`dotnet new`選項](~/docs/core/tools/dotnet-new.md#options)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-192">For more information, see [`dotnet new` Options](~/docs/core/tools/dotnet-new.md#options).</span></span> <span data-ttu-id="2a4d0-193">直接將範本的簡短名稱提供給 `dotnet new` 命令。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-193">Supply the template's short name directly to the `dotnet new` command.</span></span> <span data-ttu-id="2a4d0-194">若要從 NUnit 範本建立專案，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-194">To create a project from the NUnit template, run the following command:</span></span>

```console
dotnet new nunit
```

<span data-ttu-id="2a4d0-195">主控台會顯示專案已建立，且專案套件已還原。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-195">The console shows that the project is created and that the project's packages are restored.</span></span> <span data-ttu-id="2a4d0-196">命令執行之後，專案即可供使用。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-196">After the command is run, the project is ready for use.</span></span>

![主控台視窗會在建立 NUnit 專案，以及還原專案相依性時，顯示 dotnet new 命令的輸出。](./media/create-custom-template/nunit2.png)

### <a name="to-uninstall-a-template-from-a-nuget-package-stored-at-nugetorg"></a><span data-ttu-id="2a4d0-198">從儲存在 nuget.org 的 NuGet 套件解除安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-198">To uninstall a template from a NuGet package stored at nuget.org</span></span>

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> <span data-ttu-id="2a4d0-199">範例僅供示範之用。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-199">The example is for demonstration purposes only.</span></span> <span data-ttu-id="2a4d0-200">nuget.org 沒有 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 套件，也未與 .NET Core SDK 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-200">There isn't a `GarciaSoftware.ConsoleTemplate.CSharp` NuGet package at nuget.org or installed with the .NET Core SDK.</span></span> <span data-ttu-id="2a4d0-201">如果執行命令，但未解除安裝套件/範本，且收到下列例外狀況：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-201">If you run the command, no package/template is uninstalled and you receive the following exception:</span></span>
> 
> > <span data-ttu-id="2a4d0-202">找不到稱為 'GarciaSoftware.ConsoleTemplate.CSharp' 要解除安裝的項目。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-202">Could not find something to uninstall called 'GarciaSoftware.ConsoleTemplate.CSharp'.</span></span>

<span data-ttu-id="2a4d0-203">如已安裝 [NUnit 3 template for dotnet-new](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/) (dotnet-new 的 NUnit 3 範本)，現在希望解除安裝，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-203">If you installed the [NUnit 3 template for dotnet-new](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/) and wish to uninstall it, use the following command:</span></span>

```console
dotnet new -u NUnit3.DotNetNew.Template
```

### <a name="uninstall-the-template-from-a-local-nupkg-file"></a><span data-ttu-id="2a4d0-204">從本機 nupkg 檔案解除安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-204">Uninstall the template from a local nupkg file</span></span>

<span data-ttu-id="2a4d0-205">當您想要解除安裝範本時，請勿嘗試使用 *nupkg* 檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-205">When you wish to uninstall the template, don't attempt to use the path to the *nupkg* file.</span></span> <span data-ttu-id="2a4d0-206">*嘗試使用 `dotnet new -u <PATH_TO_NUPKG_FILE>` 解除安裝範本失敗。*</span><span class="sxs-lookup"><span data-stu-id="2a4d0-206">*Attempting to uninstall a template using `dotnet new -u <PATH_TO_NUPKG_FILE>` fails.*</span></span> <span data-ttu-id="2a4d0-207">依套件的 `id` 參考套件：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-207">Reference the package by its `id`:</span></span>

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp.1.0.0
```

## <a name="use-file-system-distribution"></a><span data-ttu-id="2a4d0-208">使用檔案系統發佈</span><span class="sxs-lookup"><span data-stu-id="2a4d0-208">Use file system distribution</span></span>

<span data-ttu-id="2a4d0-209">若要發佈範本，請將專案範本資料夾放在網路上使用者能存取的位置。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-209">To distribute the template, place the project template folder in a location accessible to users on your network.</span></span> <span data-ttu-id="2a4d0-210">使用 `dotnet new` 命令搭配 `-i|--install` 選項，並指定範本資料夾的路徑 (包含專案的專案資料夾和 *.template.config* 資料夾)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-210">Use the `dotnet new` command with the `-i|--install` option and specify the path to the template folder (the project folder containing the project and the *.template.config* folder).</span></span>

<span data-ttu-id="2a4d0-211">教學課程假設專案範本是儲存在使用者設定檔的 *Documents/Templates* 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-211">The tutorial assumes the project template is stored in the *Documents/Templates* folder of the user's profile.</span></span> <span data-ttu-id="2a4d0-212">從該位置安裝範本，以下列命令取代 \<使用者> 和使用者的設定檔名稱：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-212">From that location, install the template with the following command replacing \<USER> with the user's profile name:</span></span>

```console
dotnet new -i C:/Users/<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp
```

### <a name="create-a-project-from-the-template"></a><span data-ttu-id="2a4d0-213">從範本建立專案</span><span class="sxs-lookup"><span data-stu-id="2a4d0-213">Create a project from the template</span></span>

<span data-ttu-id="2a4d0-214">從檔案系統安裝範本之後，從放置範本引擎輸出的目錄執行 `dotnet new <TEMPLATE>` 命令來使用範本 (除非您要使用 `-o|--output` 選項來指定特定的目錄)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-214">After the template is installed from the file system, use the template by executing the `dotnet new <TEMPLATE>` command from the directory where you want to the template engine's output placed (unless you're using the `-o|--output` option to specify a specific directory).</span></span> <span data-ttu-id="2a4d0-215">如需詳細資訊，請參閱[`dotnet new`選項](~/docs/core/tools/dotnet-new.md#options)。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-215">For more information, see [`dotnet new` Options](~/docs/core/tools/dotnet-new.md#options).</span></span> <span data-ttu-id="2a4d0-216">直接將範本的簡短名稱提供給 `dotnet new` 命令。</span><span class="sxs-lookup"><span data-stu-id="2a4d0-216">Supply the template's short name directly to the `dotnet new` command.</span></span>

<span data-ttu-id="2a4d0-217">從在 C:/Users/\<使用者>/Documents/Projects/MyConsoleApp 建立的新專案資料夾，建立來自 `garciaconsole` 範本的專案：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-217">From a new project folder created at *C:/Users/\<USER>/Documents/Projects/MyConsoleApp*, create a project from the `garciaconsole` template:</span></span>

```console
dotnet new garciaconsole
```

### <a name="uninstall-the-template"></a><span data-ttu-id="2a4d0-218">解除安裝範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-218">Uninstall the template</span></span>

<span data-ttu-id="2a4d0-219">如果在 C:/Users/\<使用者>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 的本機檔案系統上建立範本，請使用 `-u|--uninstall` 參數和範本資料夾路徑解除安裝它：</span><span class="sxs-lookup"><span data-stu-id="2a4d0-219">If you created the template on your local file system at *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp*, uninstall it with the `-u|--uninstall` switch and the path to the template folder:</span></span>

```console
dotnet new -u C:/Users/<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp
```

## <a name="see-also"></a><span data-ttu-id="2a4d0-220">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2a4d0-220">See also</span></span>

<span data-ttu-id="2a4d0-221">[dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki) (維基百科：dotnet/templating GitHub 存放庫)</span><span class="sxs-lookup"><span data-stu-id="2a4d0-221">[dotnet/templating GitHub repo Wiki](https://github.com/dotnet/templating/wiki)</span></span>  
<span data-ttu-id="2a4d0-222">[dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples) (dotnet/dotnet-template-samples GitHub 存放庫)</span><span class="sxs-lookup"><span data-stu-id="2a4d0-222">[dotnet/dotnet-template-samples GitHub repo](https://github.com/dotnet/dotnet-template-samples)</span></span>  
[<span data-ttu-id="2a4d0-223">如何建立您自己的 dotnet new 範本</span><span class="sxs-lookup"><span data-stu-id="2a4d0-223">How to create your own templates for dotnet new</span></span>](https://blogs.msdn.microsoft.com/dotnet/2017/04/02/how-to-create-your-own-templates-for-dotnet-new/)  
[<span data-ttu-id="2a4d0-224">JSON 結構描述保存區的 *template.json* 結構描述</span><span class="sxs-lookup"><span data-stu-id="2a4d0-224">*template.json* schema at the JSON Schema Store</span></span>](http://json.schemastore.org/template)  
