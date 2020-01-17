---
title: .NET Framework の更新後に SQLCLR アセンブリをアップグレードする
description: .NET framework を更新した後に SQL Server Data Quality Services (DQS) で使用される SQLCLR アセンブリを更新する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 623fbf69ef49ceb7dfea7f2d9c6e96b7520ded3e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558090"
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>.NET framework の更新後に SQLCLR アセンブリをアップグレードする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) は、Microsoft .NET Framework 4 アセンブリを参照する SQL 共通言語ランタイム (SQLCR) ルーチンのコレクションです。 コンピューターの .NET Framework を更新し、それが参照先の .NET Framework アセンブリに影響した場合、グローバル アセンブリ キャッシュ (GAC) 内のアセンブリのモジュール バージョン ID (MVID) が変更されます。 これが起こると、GAC 内の参照先アセンブリと [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]内のアセンブリとの間で MVID の不一致が発生します。  
  
 .NET Framework の更新で [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの再起動が必要な場合は、影響を受ける SQLCLR アセンブリが自動的にアップグレードされて、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの再起動時に発生する MVID の不一致の問題が修正されます。 ただし、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターを再起動する必要のない .NET Framework の更新の場合は、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を使用して [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]に接続しようとすると、アセンブリの MVID の不一致によりエラーが発生します。  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe -upgradedlls.  
```  
  
 この問題を解決するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 内の、影響を受ける SQLCLR アセンブリをアップグレードする必要があります。 これを行うには、 **upgradedlls** コマンド ライン パラメーターを使用して DQSInstaller.exe ファイルを実行することにより、DQS データベースの再作成をスキップし、影響を受けるアセンブリのアップグレードのみを行います。 これにより、ナレッジ ベース、データ品質プロジェクト、および DQS 内のその他すべてのデータが維持されます。  
  
## <a name="prerequisites"></a>前提条件  
  
-   
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
-   Windows ユーザー アカウントが、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] がインストールされている SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>SQLCLR アセンブリをアップグレードするには  
  
1.  コマンド プロンプトを起動します。  
  
2.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスをインストールした場合、DQSinstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn に格納されます。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  残りの手順は、「 [Data Quality Server のインストールを完了するための DQSInstaller.exe の実行](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) 」の「 [[スタート] 画面、[スタート] メニュー、または Windows エクスプローラーから DQSInstaller.exe を実行する](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)」の手順 2. ～ 6. と同じです。  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [SQL Server 更新プログラムのインストール後の DQS データベース スキーマのアップグレード](../../data-quality-services/install-windows/upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  
