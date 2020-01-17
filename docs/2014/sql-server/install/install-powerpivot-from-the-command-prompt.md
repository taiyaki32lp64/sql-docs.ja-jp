---
title: コマンドプロンプトからの PowerPivot のインストール |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 7f1f2b28-c9f5-49ad-934b-02f2fa6b9328
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8959b1ca4ea719ce571cb8609b817bba965185bd
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798331"
---
# <a name="install-powerpivot-from-the-command-prompt"></a>コマンド プロンプトからの PowerPivot のインストール
  コマンド ラインからセットアップを実行して、SQL Server PowerPivot for SharePoint をインストールすることができます。 コマンドには `/ROLE` パラメーターを含め、`/FEATURES` パラメーターを除外する必要があります。  
  
## <a name="prerequisites"></a>Prerequisites  
 SharePoint Server 2010 Enterprise Edition Service Pack 1 (SP1) をインストールする必要があります。  
  
 Analysis Services を準備するには、ドメイン アカウントを使用する必要があります。  
  
 コンピューターが SharePoint ファームと同じドメインに参加する必要があります。  
  
##  <a name="Commands"></a>/ROLE ベースのインストールオプション  
 PowerPivot for SharePoint の配置では `/ROLE` パラメーターの代わりに `/FEATURES` パラメーターが使用されます。 有効な値は次のとおりです。  
  
-   `SPI_AS_ExistingFarm`  
  
-   `SPI_AS_NewFarm`  
  
 どちらのロールを指定しても、アプリケーション、構成、および配置のファイルがインストールされて、SharePoint ファームで PowerPivot for SharePoint を実行できるようになります。 指定したロールに基づいて、SharePoint 統合のハードウェアおよびソフトウェアの要件がチェックされます。  
  
 既存のファーム オプションでは、SharePoint ファームが既に存在することが想定されます。 新しいファームのオプションでは、新しいファームを作成することを前提としています。データベースエンジンインスタンスをファームのデータベースサーバーとして使用できるように、コマンドライン構文にデータベースエンジンインスタンスを追加する機能がサポートされています。  
  
 以前のリリースとは異なり、すべてのサーバー構成タスクはインストール後のタスクとして実行されます。 インストールと構成の手順を自動化している場合は、PowerShell を使用してサーバーを構成できます。 詳細については、「 [Windows PowerShell を使用した PowerPivot の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)」を参照してください。  
  
## <a name="example-commands"></a>コマンドの例  
 次の例では、各オプションの使用方法を示します。 例1は `SPI_AS_ExistingFarm`を示しています。  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 例 2 は `SPI_AS_NewFarm` を示します。 データベース エンジンを準備するパラメーターが含まれています。  
  
```cmd
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_NewFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/SQLSVCACCOUNT=<DomainName\UserName> /SQLSVCPASSWORD=<StrongPassword> /SQLSYSADMINACCOUNTS=<DomainName\UserName> /AGTSVCACCOUNT=<DomainName\UserName> /AGTSVCPASSWORD=<StrongPassword> /ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
##  <a name="Join"></a>コマンドの構文の変更  
 次の手順に従って、コマンド構文の例を変更します。  
  
1.  次のコマンドをコピーして、メモ帳に貼り付けます。  
  
    ```cmd
    Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /ROLE=SPI_AS_ExistingFarm /INSTANCENAME=PowerPivot /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
    ```  
  
     `/q` パラメーターは、セットアップを非表示モードで実行します。この場合、ユーザー インターフェイスは表示されません。  
  
     `/IAcceptSQLServerLicenseTerms` は、自動インストールのために `/q` パラメーターまたは `/qs` パラメーターを指定する場合に必要です。  
  
     `/action` パラメーターは、インストールを実行するようにセットアップに命令します。  
  
     `/role` パラメーターは、PowerPivot for SharePoint に必要な Analysis Services のプログラム ファイルと構成ファイルをインストールするようにセットアップに命令します。 また、既存のファーム接続情報を検出し、それを使用して SharePoint 構成データベースにアクセスします。 このパラメーターは必須です。 `/features` パラメーターの代わりにこのパラメーターを使用して、インストールするコンポーネントを指定します。  
  
     `/instancename` パラメーターは、名前付きインスタンスとして 'PowerPivot' を指定します。 この値はハードコードされていて変更できません。 ここでは、サービスのインストール方法を示すために指定されています。  
  
     `/indicateprogress` パラメーターは、コマンド プロンプト ウィンドウで進行状況を監視できるようにします。  
  
2.  ここでは、`PID` パラメーターが省略されているため、Evaluation Edition がインストールされます。 Enterprise Edition をインストールする場合は、セットアップ コマンドに PID を追加して、有効なプロダクト キーを指定します。  
  
    ```  
    /PID=<product key for an Enterprise installation>  
    ```  
  
3.  \<domain\username > と \<StrongPassword > のプレースホルダーを、有効なユーザーアカウントとパスワードに置き換えます。  
  
     `/assvaccount` と **/assvcpassword**パラメーターは、アプリケーションサーバーで [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスを構成するために使用されます。 これらのプレースホルダーを有効なアカウント情報に置き換えます。  
  
     **/Assysadminaccounts**パラメーターは、SQL Server セットアップを実行しているユーザーの id に設定する必要があります。 システム管理者を少なくとも 1 人指定する必要があります。 SQL Server セットアップでは、あらかじめ登録された Administrators グループのメンバーに対して sysadmin 権限が自動的に付与されなくなったことに注意してください。  
  
4.  改行を削除します。  
  
5.  コマンド全体を選択し、編集 メニューの **コピー** をクリックします。  
  
6.  管理者のコマンド プロンプトを開きます。 これを行うには、 **[スタート]** ボタンをクリックし、コマンドプロンプトを右クリックして、 **[管理者として実行]** を選択します。  
  
7.  SQL Server のインストール メディアを含むドライブまたは共有フォルダーに移動します。  
  
8.  編集済みのコマンドをコマンド ラインに貼り付けます。 これを行うには、コマンドプロンプトウィンドウの左上隅にあるアイコンをクリックし、 **[編集]** をポイントして、 **[貼り付け]** をクリックします。  
  
9. **Enter**キーを押してコマンドを実行します。 セットアップが完了するまで待ちます。 コマンド プロンプト ウィンドウでセットアップの進行状況を監視できます。  
  
10. インストールを確認するには、\Program Files\SQL Server\120\Setup Bootstrap\Log にある summary.txt ファイルを調べます。 サーバーがエラーなしでインストールされていれば、最終結果が "Passed" になっています。  
  
11. サーバーを構成します。 少なくとも、ソリューションを配置し、サービス アプリケーションを作成して、各サイト コレクションで PowerPivot 機能を有効化する必要があります。 詳細については、「サーバーの全体管理での[PowerPivot for SharePoint &#40;2010 powerpivot 構成ツール&#41; ](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)または[powerpivot サーバーの管理と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)の構成または修復」を参照してください。  
  
## <a name="see-also"></a>参照  
 [PowerPivot サービスアカウントの構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
