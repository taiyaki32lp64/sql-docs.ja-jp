---
title: .NET Framework 更新後の SQLCLR アセンブリのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b1a008cc-7e6b-4655-a869-bd429f986400
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: aa4cd8349846a5c00f62f6cbf115b4cc3a1614ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480476"
---
# <a name="upgrade-sqlclr-assemblies-after-net-framework-update"></a>.NET Framework 更新後の SQLCLR アセンブリのアップグレード
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) は、Microsoft .NET Framework 4 アセンブリを参照する SQL 共通言語ランタイム (SQLCR) ルーチンのコレクションです。 コンピューターの .NET Framework を更新し、それが参照先の .NET Framework アセンブリに影響した場合、グローバル アセンブリ キャッシュ (GAC) 内のアセンブリのモジュール バージョン ID (MVID) が変更されます。 これが起こると、GAC 内の参照先アセンブリと [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]内のアセンブリとの間で MVID の不一致が発生します。  
  
 .NET Framework の更新で [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの再起動が必要な場合は、影響を受ける SQLCLR アセンブリが自動的にアップグレードされて、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの再起動時に発生する MVID の不一致の問題が修正されます。 ただし、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターを再起動する必要のない .NET Framework の更新の場合は、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を使用して [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]に接続しようとすると、アセンブリの MVID の不一致によりエラーが発生します。  
  
```  
A new version of .NET was installed on this machine. In order to continue to work with DQS please run dqsinstaller.exe -upgradedlls.  
```  
  
 この問題を解決するには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 内の、影響を受ける SQLCLR アセンブリをアップグレードする必要があります。 これを行うには、 **upgradedlls** コマンド ライン パラメーターを使用して DQSInstaller.exe ファイルを実行することにより、DQS データベースの再作成をスキップし、影響を受けるアセンブリのアップグレードのみを行います。 これにより、ナレッジ ベース、データ品質プロジェクト、および DQS 内のその他すべてのデータが維持されます。  
  
## <a name="prerequisites"></a>前提条件  
  
-   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
-   Windows ユーザー アカウントが、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] がインストールされている SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
### <a name="to-upgrade-sqlclr-assemblies"></a>SQLCLR アセンブリをアップグレードするには  
  
1.  コマンド プロンプトを起動します。  
  
2.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスをインストールした場合、DQSInstaller.exe ファイルは C:\Program files \microsoft SQL Server\MSSQL12 でご利用いただけますになります。MSSQLSERVER\MSSQL\Binn:  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
    ```  
  
3.  コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    dqsinstaller.exe -upgradedlls  
    ```  
  
4.  残りの手順は、「 [Data Quality Server のインストールを完了するための DQSInstaller.exe の実行](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md#WindowsExplorer) 」の「 [[スタート] 画面、[スタート] メニュー、または Windows エクスプローラーから DQSInstaller.exe を実行する](run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)」の手順 2. ～ 6. と同じです。  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](install-data-quality-services.md)   
 [SQL Server 更新プログラムのインストール後の DQS データベース スキーマのアップグレード](upgrade-dqs-databases-schema-after-installing-sql-server-update.md)  
  
  
