---
title: "dotnet pack 命令 - .NET Core CLI"
description: "dotnet pack 命令會建立 .NET Core 專案的 NuGet 套件。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 8594c863d67baf0237b63e61f28ca9ee315eeddf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-pack"></a>dotnet pack

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet pack` - 將程式碼封裝到 NuGet 套件。

## <a name="synopsis"></a>概要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet pack [<PROJECT>] [-c|--configuration] [--force] [--include-source] [--include-symbols] [--no-build] [--no-dependencies] [--no-restore] [-o|--output] [--runtime] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet pack [<PROJECT>] [-c|--configuration] [--include-source] [--include-symbols] [--no-build] [-o|--output] [-s|--serviceable] [-v|--verbosity] [--version-suffix]
dotnet pack [-h|--help]
```
---

## <a name="description"></a>說明

`dotnet pack` 命令會建置專案，並建立 NuGet 套件。 此命令的結果是 NuGet 套件。 如果有 `--include-symbols` 選項，會建立另一個包含偵錯符號的套件。

封裝專案的 NuGet 相依性會新增至 *.nuspec* 檔案，因此在安裝套件時可以正確地解析它們。 專案對專案參考不會封裝到專案內。 目前，如果您有專案對專案相依性，則必須一個專案各一個套件。

`dotnet pack` 預設會先建置專案。 如果您想要避免這種行為，請傳遞 `--no-build` 選項。 這通常適用於您知道先前剛建立程式碼的持續整合 (CI) 組建案例。 

## <a name="arguments"></a>引數

`PROJECT`

要封裝的專案。 它可以是 [csproj 檔案](csproj.md)或目錄的路徑。 如果省略，則會預設為目前目錄。

## <a name="options"></a>選項

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`。

`--force`：即使最後的還原成功，仍強制解析所有相依性。 這相當於刪除 *project.assets.json* 檔案。

`-h|--help`

印出命令的簡短說明。

`--include-source`

將原始程式檔納入 NuGet 套件。 原始程式檔包含在 `nupkg` 中的 `src` 資料夾。

`--include-symbols`

產生符號 `nupkg`。

`--no-build`

不會在封裝前建置專案。

`--no-dependencies`

忽略專案對專案參考，並且只還原根專案。

`--no-restore`

執行命令時，不執行隱含的還原。

`-o|--output <OUTPUT_DIRECTORY>`

將已建置的套件放置在指定的目錄中。

`-r|--runtime <RUNTIME_IDENTIFIER>`

指定要還原套件的目標執行階段。 如需執行階段識別項 (RID) 清單，請參閱 [RID 目錄](../rid-catalog.md)。

`-s|--serviceable`

在套件中設定可提供服務的旗標。 如需詳細資訊，請參閱 [.NET 部落格︰.NET 4.5.1 支援適用於 .NET NuGet 程式庫的 Microsoft 安全性更新 (英文)](https://aka.ms/nupkgservicing)。

`--version-suffix <VERSION_SUFFIX>`

在專案中定義 `$(VersionSuffix)` MSBuild 屬性的值。

`-v|--verbosity <LEVEL>`

設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`。

`-h|--help`

印出命令的簡短說明。

`--include-source`

將原始程式檔納入 NuGet 套件。 原始程式檔包含在 `nupkg` 中的 `src` 資料夾。

`--include-symbols`

產生符號 `nupkg`。

`--no-build`

不會在封裝前建置專案。

`-o|--output <OUTPUT_DIRECTORY>`

將已建置的套件放置在指定的目錄中。

`-s|--serviceable`

在套件中設定可提供服務的旗標。 如需詳細資訊，請參閱 [.NET 部落格︰.NET 4.5.1 支援適用於 .NET NuGet 程式庫的 Microsoft 安全性更新 (英文)](https://aka.ms/nupkgservicing)。

`--version-suffix <VERSION_SUFFIX>`

在專案中定義 `$(VersionSuffix)` MSBuild 屬性的值。

`-v|--verbosity <LEVEL>`

設定命令的詳細資訊層級。 允許的值為 `q[uiet]`、`m[inimal]`、`n[ormal]`、`d[etailed]` 和 `diag[nostic]`。

---

## <a name="examples"></a>範例

封裝目前目錄中的專案：

`dotnet pack`

封裝 `app1` 專案：

`dotnet pack ~/projects/app1/project.csproj`
    
封裝目前目錄中的專案，並將產生的套件放置到 `nupkgs` 資料夾中：

`dotnet pack --output nupkgs`

將目前目錄中的專案封裝到 `nupkgs` 資料夾，並略過建置步驟︰

`dotnet pack --no-build --output nupkgs`

在 *.csproj* 檔案中將專案的版本尾碼設定為 `<VersionSuffix>$(VersionSuffix)</VersionSuffix>`，封裝目前的專案並使用指定尾碼更新產生的套件版本︰

`dotnet pack --version-suffix "ci-1234"`
