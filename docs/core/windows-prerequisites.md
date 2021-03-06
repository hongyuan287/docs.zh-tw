---
title: "Windows 上 .NET Core 的必要條件 | Microsoft Docs"
description: "了解在 Windows 電腦上開發及執行 .NET Core 應用程式時，您需要哪些相依性。"
author: JRAlexander
ms.author: johalex
ms.date: 08/13/2017
ms.topic: article
ms.prod: .net-core
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 84f1eaf5fbfcdf8d1dd1b90545f9236e2daedd15
ms.contentlocale: zh-tw
ms.lasthandoff: 08/14/2017

---
# <a name="prerequisites-for-net-core-on-windows"></a>Windows 上 .NET Core 的必要條件

本文會說明在 Windows 開發 .NET Core 應用程式所需的相依性。 支援的作業系統版本和跟隨的相依性，適用於在 Windows 開發 .NET Core 應用程式的三種方式：

* [命令列](tutorials/using-with-xplat-cli.md)
* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* [Visual Studio Code](https://code.visualstudio.com/)

## <a name="net-core-supported-windows-versions"></a>.NET Core 支援的 Windows 版本

下列版本支援 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10、Windows 10 年度更新 (1607 版) 或更新版本
* Windows Server 2008 R2 SP1 (完整伺服器或 Server Core)
* Windows Server 2012 SP1 (完整伺服器或 Server Core)
* Windows Server 2012 R2 (完整伺服器或 Server Core)
* Windows Server 2016 (完整伺服器、Server Core 或 Nano Server)

如需 .NET Core 2.x 支援的作業系統完整清單，請參閱 [.NET Core 2.x - 支援的作業系統版本](https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md)。

如需 .NET Core 1.x 支援的作業系統完整清單，請參閱 [.NET Core 1.x 支援的作業系統版本](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md)。

## <a name="net-core-dependencies"></a>.NET Core 的相依性

在 Windows 10 和 Windows Server 2016 之前的 Windows 版本上執行時，.NET Core 需要 Visual C++ 可轉散發套件。 .NET Core 安裝程式會自動安裝此相依性。

必須手動安裝 [Microsoft Visual C++ 2015 可轉散發套件 Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=52685) 的時機：

   * 使用[安裝程式指令碼](./tools/dotnet-install-script.md)安裝 .NET Core。
   * 部署獨立的 .NET Core 應用程式。

> [!NOTE]
> <em>僅適用於 Windows 7 和 Windows Server 2008 電腦：</em><br>
> 確定您的 Windows 安裝為最新狀態，而且包含已透過 Windows Update 安裝的 Hotfix [KB2533623](https://support.microsoft.com/help/2533623)。

## <a name="prerequisites-with-visual-studio-2017"></a>使用 Visual Studio 2017 的必要條件

您可以使用任何編輯器來開發使用 .NET Core SDK 的 .NET Core 應用程式。  [Visual Studio 2017](#visual-studio-2017) 為 Windows 上的 .NET Core 應用程式提供整合式開發環境。

您可以在[版本資訊](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)中，進一步了解 Visual Studio 2017 的變更。
# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

若要在 Visual Studio 2017 中開發 .NET Core 2.x 應用程式：

 1. [下載並安裝 Visual Studio 2017 15.3.0 版本或更高版本](/visualstudio/install/install-visual-studio)，選取 [.NET Core 跨平台開發] 工作負載 (在 [其他工具組] 區段)。
![已選取 [.NET Core 跨平台開發] 工作負載的 Visual Studio 2017 安裝螢幕擷取畫面](./media/windows-prerequisites/vs-15-3-workloads.jpg)

安裝 **.NET Core 跨平台開發**工具集之後，Visual Studio 2017 預設使用 .NET Core 1.x。 安裝 .NET Core 2.x SDK 以取得 Visual Studio 2017 中的 .NET Core 2.x 支援。

 2. 安裝 [.NET Core 2.x SDK](https://www.microsoft.com/net/download/core)。
 3. 使用下列指示將現有或新的 .NET Core 1.x 專案目標重定到 .NET Core 2.x：
    * 在 [專案] 功能表上，選擇 [屬性]。 
    * 在 [目標 Framework] 選取功能表中，將值設為 **.NET Core 2.0**。

![螢幕擷取畫面：選取 ".NET Core 2.0" 目標 Framework 功能表項目的 Visual Studio 2017 應用程式專案屬性](./media/windows-prerequisites/Targeting-dotnetCore2.png)

一旦安裝 .NET Core 2.x SDK，Visual Studio 2017 預設會使用 .NET Core SDK 2.x，而且支援下列動作：

  * 開啟、建置及執行現有的 .NET Core 1.x 專案。
  * 將 .NET Core 1.x 專案重定目標至 .NET Core 2.x、建置和執行。
  * 建立新的 .NET Core 2.x 專案。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
若要使用 Visual Studio 開發 .NET Core 1.x 應用程式，請[下載並安裝 Visual Studio 2017 RTM (版本 15.0.26228.4) 或更高版本](/visualstudio/install/install-visual-studio)，選取 [.NET Core 跨平台開發] 工作負載 (在 [其他工具組] 區段)。
![已選取 [.NET Core 跨平台開發] 工作負載的 Visual Studio 2017 安裝螢幕擷取畫面](./media/windows-prerequisites/vs_workloads.jpg)
> [!IMPORTANT]
> 有可能使用 Visual Studio 2015 開發 .NET Core 1.x，但不建議為下列原因而如此做：
  > * .NET Core 工具是預覽版本，不受支援。
  > * 專案是以 project.json 為基礎，已被取代。
>
> 如需專案格式變更的詳細資訊，請參閱[變更的高階概觀](./tools/cli-msbuild-architecture.md)。
---

>[!TIP]
  > 確認 Visual Studio 2017 版本：
>
     > * 在 **[說明]** 功能表上，選擇 **[關於 Microsoft Visual Studio]**。
     > * 在 [關於 Microsoft Visual Studio] 對話方塊中，確認版本號碼。
>     * .NET Core 2.x 應用程式應為 Visual Studio 2017 版本 15.3 (26730.01) 或更高版本。
>     * .NET Core 1.x 應用程式應為 Visual Studio 2017 版本 15.0 (26228.04) 或更高版本。

---

# <a name="prerequisites-for-net-core-on-windows"></a>Windows 上 .NET Core 的必要條件

本文將說明您在 Windows 電腦上部署與執行 .NET Core 應用程式，以及使用 Visual Studio 來開發時，您需要哪些相依性。

## <a name="supported-windows-versions"></a>支援的 Windows 版本

下列 Windows 版本支援 .NET Core：

* Windows 7 SP1
* Windows 8.1
* Windows 10
* Windows Server 2008 R2 SP1 (完整伺服器或 Server Core)
* Windows Server 2012 SP1 (完整伺服器或 Server Core)
* Windows Server 2012 R2 SP1 (完整伺服器或 Server Core)
* Windows Server 2016 (完整伺服器、Server Core 或 Nano Server)

如需完整的支援作業系統，請參閱 [.NET Core 版本資訊](https://github.com/dotnet/core/blob/master/release-notes/1.1/1.1.md)。

## <a name="net-core-dependencies"></a>.NET Core 的相依性

在 Windows 10 和 Windows Server 2016 之前的 Windows 版本上執行時，.NET Core 需要 Visual C++ 可轉散發套件。 如果您使用 .NET Core 安裝程式，會自動為您安裝此相依性。 不過，如果您是透過[安裝程式指令碼 (英文)](https://docs.microsoft.com/en-us/dotnet/articles/core/tools/dotnet-install-script)安裝 .NET Core 或者部署獨立的 .NET Core 應用程式，您需要手動安裝[適用於 Visual Studio 2015 的 Visual C++ 可轉散發套件 (英文)](https://www.microsoft.com/en-us/download/details.aspx?id=48145)。

> [!NOTE]
> <em>僅適用於 Windows 7 和 Windows Server 2008 電腦：</em><br>
> 確定您的 Windows 安裝為最新狀態，而且包含已透過 Windows Update 安裝的 Hotfix [KB2533623](https://support.microsoft.com/en-us/kb/2533623)。

## <a name="prerequisites-with-visual-studio-2017"></a>使用 Visual Studio 2017 的必要條件

您可以使用 .NET Core SDK 以使用您選擇的任何編輯器來開發 .NET Core 應用程式。 不過，如果您想要在整合式開發環境中於 Windows 上開發 .NET Core 應用程式，您可以使用 [Visual Studio 2017](#visual-studio-2017)。

> [!IMPORTANT]
> 即使如此，您還是可以使用 Visual Studio 2015 搭配預覽版本的 .NET Core 工具來開發，但這些專案將以 *project.json* 為基礎，而這目前已被取代。 Visual Studio 2017 使用以 MSBuild 為基礎的專案檔案。 如需格式變更的詳細資訊，請參閱[變更的高階概觀](./tools/cli-msbuild-architecture.md)。

若要使用 Visual Studio 2017 開發 .NET Core 應用程式，您必須安裝最新版本的 Visual Studio 並選取 [.NET Core 跨平台開發] 工具組 (在 [其他工具組] 區段中)。
![已選取 [.NET Core 跨平台開發] 工作負載的 Visual Studio 2017 安裝螢幕擷取畫面](./media/windows-prerequisites/vs_workloads.jpg)

Visual Studio 2017 有許多種版本。 您可以免費下載 [Visual Studio Community 2017](https://www.visualstudio.com/downloads/) 開始使用。  若要深入了解 Visual Studio 安裝程序，請參閱 [Install Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/install/install-visual-studio) (安裝 Visual Studio 2017)。

若要確認您是否正在執行最新版本的 Visual Studio 2017，請執行下列動作︰

* 在 **[說明]** 功能表上，選擇 **[關於 Microsoft Visual Studio]**。
* 在 **[關於 Microsoft Visual Studio]** 對話方塊中，版本號碼應為 15.0.26228.4 或更高版本。

您可以在[版本資訊](https://www.visualstudio.com/en-us/news/releasenotes/vs2017-relnotes)中，進一步了解 Visual Studio 2017 的變更。

[sdk]: https://go.microsoft.com/fwlink/?LinkID=827546
