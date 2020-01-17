---
title: SQL Server セットアップ ログ ファイルの表示と読み取り | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6a81258e87bf2422f3ae5a55afc5eb6429856b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774324"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>SQL Server セットアップ ログ ファイルの表示と読み取り
  セットアップを実行するたびにログ ファイルは %programfiles% に新しいタイムスタンプ ログ フォルダーに作成されますが作成されます\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\します。 タイムスタンプ付きのログ フォルダーの名前形式は YYYYMMDD_hhmmss です。 セットアップを自動モードで実行した場合は、% temp%\sqlsetup*.log にログが作成されます。 ログ フォルダー内のログ ファイルはすべて、それぞれのログ フォルダー内で Log\*.cab ファイルにアーカイブされます。  
  
 一般的なセットアップの要求では、次の 3 つの実行フェーズを経由します。  
  
1.  グローバル ルールのテキスト  
  
2.  コンポーネントの更新  
  
3.  ユーザーが要求した操作  
  
 各フェーズでは、セットアップが詳細ログと概要ログを生成するほか、必要に応じて追加のログ ファイルも生成されます。 セットアップは、ユーザーが要求したセットアップ操作ごとに最低 3 回呼び出されます。  
  
 データストア ファイルにはセットアップ処理で記録されるすべての構成オブジェクトの状態を示すスナップショットが含まれており、構成エラーのトラブルシューティングに便利です。 実行フェーズごとに、データストア オブジェクトに対して XML ファイル ダンプが作成されます。 これらの XML ファイル ダンプは、次に示すタイムスタンプ付きのログ フォルダー内にある独自のログ サブフォルダーに保存されます。  
  
-   Datastore_GlobalRules  
  
-   Datastore_ComponentUpdated  
  
-   Datastore  
  
 次のセクションでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップのログ ファイルを説明します。  
  
## <a name="summary-text"></a>概要テキスト  
  
### <a name="overview"></a>概要  
 このファイルは、セットアップ時に検出された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント、オペレーティング システム環境、指定されているコマンド ライン パラメーター値、および実行された各 MSI/MSP の全体的な状態を示します。  
  
 ログは次の各セクションに整理されています。  
  
-   実行全体の要約  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップが実行されたコンピューターのプロパティと構成  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] そのコンピューターに以前にインストールされていた製品の機能  
  
-   インストールされたバージョンとインストール パッケージのプロパティ  
  
-   インストール時に提供されたランタイム入力設定  
  
-   構成ファイルの場所  
  
-   実行結果の詳細  
  
-   グローバル ルール  
  
-   そのインストール シナリオ独自のルール  
  
-   失敗したルール  
  
-   ルール レポート ファイルの場所  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\します。  
  
 概要テキスト ファイル内でエラーを見つけるには、"エラー" や "失敗" をキーワードにして検索できます。  
  
## <a name="summaryengine-baseyyyymmddhhmmsstxt"></a>Summary_engine-base_YYYYMMDD_HHMMss.txt  
  
### <a name="overview"></a>概要  
 summary_engine の基本的なファイルは概要ファイルに似ていますが、メイン ワークフロー内で生成されます。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="summaryengine-baseyyyymmddhhmmsscomponentupdatetxt"></a>Summary_engine-base_YYYYMMDD_HHMMss_ComponentUpdate.txt  
  
### <a name="overview"></a>概要  
 コンポーネントの更新概要ファイルは概要ファイルに似ていますが、コンポーネント更新ワークフロー内で生成されます。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="summaryengine-baseversionnumbermmddhhmmssglobalrulestxt"></a>Summary_engine-base_\<VersionNumber>MMDD_HHMMss_GlobalRules.txt  
  
### <a name="overview"></a>概要  
 グローバル ルール概要ファイルは概要ファイルに似ていますが、グローバル ルール ワークフロー内で生成されます。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="detailtxt"></a>Detail.txt  
  
### <a name="overview"></a>概要  
 Detail.txt はインストールやアップグレードなど、メイン ワークフロー内で生成され、実行の詳細を示します。 このファイル内のログは、インストールで各アクションが呼び出された時刻に基づいて生成され、アクションが実行された順序とその依存関係を示します。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup  
  
 Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 セットアップ過程でエラーが発生すると、実行やエラーはこのファイルの終わりに記録されます。 このファイル内でエラーを見つけるには、まずファイルの終わりを調べてから、「エラー」や「例外」をキーワードにして検索します。  
  
## <a name="detailcomponentupdatetxt"></a>Detail_ComponentUpdate.txt  
  
### <a name="overview"></a>概要  
 Detail_ComponentUpdate.txt ファイルはコンポーネント更新ワークフローに対して生成され、Detail.txt に似ています。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="detailglobalrulestxt"></a>Detail_GlobalRules.txt  
  
### <a name="overview"></a>概要  
 Detail_GlobalRules.txt ファイルはグローバル ルール実行のために生成され、Detail.txt ファイルに似ています。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="msi-log-files"></a>MSI ログ ファイル  
  
### <a name="overview"></a>概要  
 MSI ログ ファイルはパッケージ インストール過程の詳細を提供します。 各パッケージのインストール時に、MSIEXEC によって生成されるログ ファイルです。  
  
 MSI ログ ファイルの種類  
  
-   \<機能>_\<アーキテクチャ>\_\<相互作用>.log  
  
-   \<機能>_\<アーキテクチャ>\_\<言語>\_\<相互作用>.log  
  
-   \<機能>_\<アーキテクチャ>\_\<相互作用>\_\<ワークフロー>.log  
  
### <a name="location"></a>場所  
 MSI ログ ファイルは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\< 名前\>。 ログ。  
  
 ファイルの終わりに実行の概要があり、成功したかどうかとプロパティを示します。 MSI ファイル内でエラーを見つけるには、"value 3" を検索します。通常、エラーはその文字列の近くで見つかります。  
  
## <a name="configurationfileini"></a>ConfigurationFile.ini  
  
### <a name="overview"></a>概要  
 構成ファイルにはインストール時に使用される入力の設定が含まれています。 手動で設定を入力しなくてもインストールを再起動できるようにするときに使用できます。 ただし、パスワード、PID、およびパラメーターの一部は構成ファイルには保存されません。 設定はファイルに追加できますが、コマンドラインまたはセットアップのインターフェイスを使って供給することもできます。 詳細については、次を参照してください。 [SQL Server 2014 を使用したインストール、構成ファイル](install-sql-server-using-a-configuration-file.md)します。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="systemconfigurationcheckreporthtm"></a>SystemConfigurationCheck_Report.htm  
  
### <a name="overview"></a>概要  
 システム構成チェッカーのレポートには、実行された各ルールの簡単な記述と、実行ステータスが含まれています。  
  
### <a name="location"></a>場所  
 これは %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\します。  
  
## <a name="see-also"></a>参照  
 [インストール方法に関するトピック](../../sql-server/install/installation-how-to-topics.md)   
 [SQL Server 2014 のインストール](install-sql-server.md)  
  
  
