---
title: カスタム コンポーネントの複数バージョン対応のサポート | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 91524408998df8be0df4ee5d4ede0b641dbaa2a4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71287224"
---
# <a name="support-multi-targeting-in-your-custom-components"></a>カスタム コンポーネントの複数バージョン対応のサポート

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 SQL Server Data Tools (SSDT) で SSIS デザイナーを使用して、SQL Server 2016、SQL Server 2014、または SQL Server 2012 をターゲットとするパッケージを作成、管理、および実行できるようになりました。 Visual Studio 2015 用の SSDT を入手する方法については、「[最新の SQL Server Data Tools のダウンロード](../../ssdt/download-sql-server-data-tools-ssdt.md)」を参照してください。 

 ソリューション エクスプローラーで Integration Services プロジェクトを右クリックし、 **[プロパティ]** を選択すると、そのプロジェクトのプロパティ ページが開きます。 **[構成プロパティ]** の **[全般]** タブで、 **[TargetServerVersion]** プロパティを選択した後、[SQL Server 2016]、[SQL Server 2014]、または [SQL Server 2012] を選択します。  
   
 ![[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ](../../integration-services/media/targetserverversion2.png "[プロジェクトのプロパティ] ダイアログ ボックスの TargetServerVersion プロパティ")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>複数バージョンのサポートとカスタム コンポーネントの複数バージョン対応
 
SSIS カスタム拡張機能の 5 種類すべてで、複数バージョン対応がサポートされています。
-   接続マネージャー
-   処理手順
-   列挙子
-   ログ プロバイダー
-   データ フロー コンポーネント

マネージド拡張機能の場合、SSIS デザイナーが、指定されたターゲット バージョンの拡張機能のバージョンを読み込みます。 例:
-   対応バージョンが SQL Server 2012 の場合、デザイナーは、拡張機能の2012 バージョンを読み込みます。
-   対応バージョンが SQL Server 2016 の場合、デザイナーは、拡張機能の2016 バージョンを読み込みます。

COM 拡張機能は、複数バージョン対応はサポートしていません。 SSIS デザイナーは、指定した対応バージョンに関係なく、常に現在のバージョンの SQL Server の COM の拡張機能を読み込みます。

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>複数バージョンおよび複数バージョン対応の基本サポートの追加

基本的なガイダンスについては、「[Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)」 (SQL Server 2016 用 SSDT 2015 の複数バージョン サポートで SSIS カスタム拡張機能がサポートされるようにする) を参照してください。 このブログ投稿では、次の手順や要件について説明しています。

-   適切なフォルダーへのアセンブリの展開。

-   SQL Server 2014 以上のバージョン用の拡張マップ ファイルの作成。

## <a name="add-code-to-switch-versions"></a>バージョンを切り替えるためのコードの追加

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>カスタム接続マネージャー、タスク、列挙子、またはログ プロバイダーのバージョンを切り替える

カスタム接続マネージャー、タスク、列挙子、またはログ プロバイダーには、**SaveToXML** メソッドにダウングレード ロジックを追加します。

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>カスタム データ フロー コンポーネントでのバージョンの切り替え

カスタム接続マネージャー、タスク、列挙子、またはログ プロバイダーには、新しい **PerformDowngrade** メソッドにダウングレード ロジックを追加します。

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>一般的なエラー

### <a name="invalidcastexception"></a>InvalidCastException

**エラー メッセージ。** 型 'System.__ComObject' の COM オブジェクトをインターフェイス型 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100' にキャストできません。 IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' が指定されたインターフェイスの COM コンポーネント上での QueryInterface 呼び出しのときに次のエラーが発生したため、この操作に失敗しました: インターフェイスがサポートされていません。(HRESULT からの例外: 0x80004002 (E_NOINTERFACE))。 (Microsoft.SqlServer.DTSPipelineWrap)。

**解決方法。** カスタム拡張機能が、Microsoft.SqlServer.DTSPipelineWrap や Microsoft.SqlServer.DTSRuntimeWrap などの SSIS 相互運用機能アセンブリを参照する場合、 **[相互運用機能型の埋め込み]** プロパティの値を **False** に設定します。

![相互運用機能型の埋め込み](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>対応バージョンが SQL Server 2012 の場合、一部の型を読み込めない

この問題は、IErrorReportingService や IUserPromptService などの特定の型に影響します。

**エラー メッセージ (例)。** アセンブリ 'Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' から型 'Microsoft.DataWarehouse.Design.IErrorReportingService' を読み込めませんでした。

**回避策。** 対応バージョンが SQL Server 2012 の場合、これらのインターフェイスではなく、メッセージ ボックスを使用してください。

