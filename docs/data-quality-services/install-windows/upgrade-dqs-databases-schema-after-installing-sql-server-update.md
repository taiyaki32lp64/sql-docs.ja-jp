---
title: SQL Server 更新プログラムのインストール後に DQS データベーススキーマをアップグレードする
description: 修正プログラム、修正プログラム、または累積的な更新プログラムによって SQL Server が更新された後に、DQSInstaller を使用して Data Quality Services (DQS) インスタンスをアップグレードする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: c8f3fbae-02c4-464d-a35c-7108f48c58cb
author: swinarko
ms.author: sawinark
ms.openlocfilehash: db5009ef7f5c9ff2a57022d30b2eb9f009fb6ab8
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558065"
---
# <a name="upgrade-dqs-databases-schema-after-installing-sql-server-update"></a>SQL Server 更新プログラムのインストール後に DQS データベーススキーマをアップグレードする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  あらかじめ構成された DQS インスタンスに SQL Server の更新プログラム (パッチ、修正プログラム、または累積的な更新プログラム) をインストールした後、 **upgrade** コマンド ライン パラメーターを指定して DQSInstaller.exe ファイルを実行し、DQS データベース スキーマをアップグレードする必要がある場合があります。 アップグレードしなかった場合、Data Quality Client を使用して Data Quality Server に接続しようとすると、次のエラーが表示されることがあります。  
  
```  
An error occurred in the Microsoft .NET Framework while trying to load assembly id 65581.  
```  
  
 DQS データベース スキーマのアップグレードは、DQS データベース内の既存のデータ (ナレッジ ベース、データ品質プロジェクト、DQS_STAGING_DATA データベース内にエクスポートされた結果) には影響しません。 ただし、スキーマのアップグレード中に誤ってデータが削除されることを防ぐため、DQS データベース スキーマをアップグレードする前に DQS データベースをバックアップしておく必要があります。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
  
> [!NOTE]  
>  SQL Server の更新プログラムのほとんどで、DQS データベース スキーマのアップグレードが必要になります。 DQS データベース スキーマのアップグレードが必要になる SQL Server 更新プログラムの詳細については、「 [Upgrade DQS: Installing Cumulative Updates or Hotfix Patches on Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565)」(DQS のアップグレード: Data Quality Services への累積的な更新プログラムまたは修正プログラムのインストール) の手順 1.A にある表を参照してください。  
  
## <a name="prerequisites"></a>前提条件  
  
-   
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コンピューターの Administrators グループのメンバーとしてログオンする必要があります。  
  
-   Windows ユーザー アカウントが、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] がインストールされている SQL Server インスタンスの sysadmin 固定サーバー ロールのメンバーであることが必要です。  
  
### <a name="to-upgrade-dqs-databases-schema"></a>DQS データベース スキーマをアップグレードするには  
  
1.  (推奨) スキーマのアップグレードを実行する前に、DQS データベースをバックアップします。 DQS データベースのバックアップの詳細については、「 [DQS データベースのバックアップと復元](../../data-quality-services/backing-up-and-restoring-dqs-databases.md)」を参照してください。  
  
2.  コマンド プロンプトを起動します。  
  
3.  コマンド プロンプトで、DQSInstaller.exe が格納されている場所にディレクトリを変更します。 SQL Server の既定のインスタンスをインストールした場合、DQSinstaller.exe ファイルは C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn に格納されます。  
  
    ```  
    cd C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn  
    ```  
  
4.  コマンド プロンプトに次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    dqsinstaller.exe -upgrade  
    ```  
  
5.  処理を続ける前に DQS データベースをバックアップするように求められます。 既に DQS データベースをバックアップしている場合は「 **Y** 」または「 **Yes** 」と入力して Enter キーを押し、アップグレードを続行します。  
  
6.  DQS データベース スキーマのアップグレードが正常に完了すると、完了のメッセージが表示されます。  
  
## <a name="next-steps"></a>次の手順  
 Data Quality Client アプリケーションから、アップグレードされた Data Quality Server にログオンします。  
  
 SQL Server の更新プログラムをインストールしてからの DQS データベース スキーマのアップグレードの詳細、および関連するトラブルシューティング手順については、「 [Upgrade DQS: Installing Cumulative Updates or Hotfix Patches on Data Quality Services](https://go.microsoft.com/fwlink/?LinkID=251565)」(DQS のアップグレード: Data Quality Services への累積的な更新プログラムまたは修正プログラムのインストール) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Data Quality Services のインストール](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [.NET Framework 更新後の SQLCLR アセンブリのアップグレード](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)  
  
  
