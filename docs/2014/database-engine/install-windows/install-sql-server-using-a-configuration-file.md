---
title: Sql Server 2014 の構成ファイルの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: a832153a-6775-4bed-83f0-55790766d885
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 38cd8aeb157a94a28b1cfd831bcfacfb3e93ea6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775285"
---
# <a name="install-sql-server-2014-using-a-configuration-file"></a>構成ファイルを使用した SQL Server 2014 のインストール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップには、システムの既定値および実行時入力に基づいて構成ファイルを生成する機能が用意されています。 構成ファイルを使用すると、同じ構成の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を企業全体に配置できます。 また、Setup.exe を起動するバッチ ファイルを作成して、企業全体で手動によるインストールを標準化することもできます。  
  
 セットアップでは、コマンド プロンプトからのみ構成ファイルを使用できます。 以下に、構成ファイルを使用する際のパラメーターの処理順序について説明します。  
  
-   構成ファイルによって、パッケージの既定値が上書きされます。  
  
-   コマンド ライン値によって、構成ファイル内の値が上書きされます。  
  
 構成ファイルを使用すると、インストールごとにパラメーターおよび値を追跡できます。 したがって、インストールを確認および監査する場合に構成ファイルが役立ちます。  
  
## <a name="configuration-file-structure"></a>構成ファイルの構造  
 ConfigurationFile.ini ファイルは、パラメーター (名前と値のペア) と説明のコメントが含まれるテキスト ファイルです。  
  
 次に、ConfigurationFile.ini ファイルの例を示します。  
  
```  
; Microsoft SQL Server Configuration file  
[OPTIONS]  
; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE.   
; This is a required parameter.   
ACTION="Install"  
; Specifies features to install, uninstall, or upgrade.   
; The list of top-level features include SQL, AS, RS, IS, and Tools.   
; The SQL feature will install the database engine, replication, and full-text.   
; The Tools feature will install Management Tools, Books online,   
; SQL Server Data Tools, and other shared components.   
FEATURES=SQL,Tools  
```  
  
#### <a name="how-to-generate-a-configuration-file"></a>構成ファイルを生成する方法  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアを挿入します。 ルート フォルダーの Setup.exe をダブルクリックします。 ネットワーク共有からインストールするには、ネットワーク共有上のルート フォルダーに移動し、Setup.exe をダブルクリックします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition のセットアップでは、構成ファイルは自動的に作成されません。 次のコマンドを実行すると、セットアップが開始され、構成ファイルが作成されます。  
    >   
    >  SETUP.exe /UIMODE=Normal /ACTION=INSTALL  
  
2.  ウィザードに従って **[インストールの準備完了]** ページまで進みます。 構成ファイルのパスは、 **[インストールの準備完了]** ページの [構成ファイルのパス] セクションで指定します。 インストールする方法の詳細についての[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[インストール ウィザードからの SQL Server 2014 のインストール&#40;セットアップ&#41;](install-sql-server-from-the-installation-wizard-setup.md)します。  
  
3.  INI ファイルを生成するには、インストールを実際に完了しなくてもセットアップを取り消します。  
  
    > [!NOTE]  
    >  セットアップ インフラストラクチャは、パスワードなどの機密情報を除き、実行したアクションに対してすべての適切なパラメーターを書き出します。 /IAcceptSQLServerLicenseTerms パラメーターは構成ファイルに書き出されないので、構成ファイルに変更を加えるか、コマンド プロンプトで値を指定する必要があります。 詳細については、「[コマンド プロンプトからの SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)」を参照してください。 また、値が通常はコマンド プロンプトで指定されないブール型パラメーターの場合は、値が含まれます。  
  
## <a name="using-the-configuration-file-to-install-includessnoversionincludesssnoversion-mdmd"></a>構成ファイルを使用した SQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 コマンド ライン インストールでのみ構成ファイルを使用できます。  
  
> [!NOTE]  
>  構成ファイルに変更を加える必要がある場合は、コピーを作成して、コピーを変更することをお勧めします。  
  
#### <a name="how-to-use-a-configuration-file-to-install-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance"></a>構成ファイルを使用してスタンドアロンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスをインストールする方法  
  
-   コマンド プロンプトからインストールを実行し、 *ConfigurationFile* パラメーターを使用して ConfigurationFile.ini を指定します。  
  
#### <a name="how-to-use-a-configuration-file-to-prepare-and-complete-an-image-of-a-stand-alone-includessnoversionincludesssnoversion-mdmd-instance-sysprep"></a>構成ファイルを使用してスタンドアロン [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのイメージの準備と完了を行う方法 (SysPrep)  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つまたは複数のインスタンスを準備し、同じコンピューター上で構成するには、次の操作を行います。  
  
    -   [インストール センター] の **[詳細設定]** ページで、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスのイメージの準備]** を実行し、イメージ準備用構成ファイルをキャプチャします。  
  
    -   さらに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを準備するには、同じイメージ準備用構成ファイルをテンプレートとして使用します。  
  
    -   [インストール センター] の **[詳細設定]** ページで、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の準備済みスタンドアロン インスタンスのイメージの完了]** を実行し、コンピューター上で準備済みのインスタンスを構成します。  
  
2.  Windows SysPrep ツールを使用して、未構成の準備済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを含むオペレーティング システムのイメージを準備するには、次の操作を行います。  
  
    -   [インストール センター] の [詳細設定] ページで、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスのイメージの準備]** を実行し、イメージ準備用構成ファイルをキャプチャします。  
  
    -   [インストール センター] の **[詳細設定]** ページで、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の準備済みスタンドアロン インスタンスのイメージの完了]** を実行します。ただし、完了用構成ファイルをキャプチャしたら、 **[イメージの完了の準備]** ページで処理をキャンセルしてください。  
  
    -   イメージ完了用構成ファイルは、準備済みのインスタンスの構成を自動化するために、Windows イメージと共に保存できます。  
  
#### <a name="how-to-install-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>構成ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールする方法  
  
1.  統合インストール方法は次のとおりです (ノードに単一ノードのフェールオーバー クラスターを作成し、追加ノードでは AddNode を実行します)。  
  
    -   [フェールオーバー クラスターをインストールする] オプションを実行して、すべてのインストール設定の一覧を示す構成ファイルをキャプチャします。  
  
    -   *ConfigurationFile* パラメーターを指定して、コマンド ライン フェールオーバー クラスターのインストールを実行します。  
  
    -   追加するノードで、AddNode を実行して既存のフェールオーバー クラスターに適用できる ConfigurationFile.ini ファイルをキャプチャします。  
  
    -   同じ構成ファイルを指定して ConfigurationFile パラメーターを使用することによって、フェールオーバー クラスターを結合するすべての追加ノードでコマンド ライン AddNode を実行します。  
  
2.  詳細なインストール方法は次のとおりです (すべてのフェールオーバー クラスター ノードでフェールオーバー クラスターを準備し、次にすべてのノードを準備した後、共有ディスクを所有するノードで完了操作を実行します)。  
  
    -   いずれかのノードで **[準備]** を実行して、ConfigurationFile.ini ファイルをキャプチャします。  
  
    -   準備するフェールオーバー クラスターのすべてのノードで、設定する同じ ConfigurationFile.ini ファイルを指定します。  
  
    -   すべてのノードを準備した後、共有ディスクを所有するノードでフェールオーバー クラスターの完了操作を実行して、ConfigurationFile.ini ファイルをキャプチャします。  
  
    -   この ConfigurationFile.ini ファイルを指定すると、フェールオーバー クラスターを完了できます。  
  
#### <a name="how-to-add-or-remove-a-node-to-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>構成ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターにノードを追加または削除する方法  
  
-   フェールオーバー クラスターにノードを追加したり、フェールオーバー クラスターからノードを削除したりするために以前使用した構成ファイルがある場合は、同じファイルを再利用してノードの追加や削除を実行できます。  
  
#### <a name="how-to-upgrade-a-includessnoversionincludesssnoversion-mdmd-failover-cluster-using-the-configuration-file"></a>構成ファイルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアップグレードする方法  
  
1.  パッシブ ノードでアップグレードを実行して、ConfigurationFile.ini ファイルをキャプチャします。 それには、実際のアップグレードを実行するか、または実際のアップグレードを実行しないで最後に終了します。  
  
2.  アップグレードするすべての追加ノードで、ConfigurationFile.ini ファイルを指定して処理を完了します。  
  
## <a name="sample-syntax"></a>サンプル構文  
 次に、構成ファイルの使用方法の例をいくつか示します。  
  
-   コマンド プロンプトで構成ファイルを指定するには  
  
```  
Setup.exe /ConfigurationFile=MyConfigurationFile.INI  
```  
  
-   構成ファイルの代わりにコマンド プロンプトでパスワードを指定するには  
  
```  
Setup.exe /SQLSVCPASSWORD="************" /AGTSVCPASSWORD="************" /ASSVCPASSWORD="************" /ISSVCPASSWORD="************" /RSSVCPASSWORD="************" /ConfigurationFile=MyConfigurationFile.INI  
```  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトから SQL Server 2014 をインストールします。](install-sql-server-from-the-command-prompt.md)   
 [SQL Server フェールオーバー クラスターのインストール](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)   
 [SQL Server フェールオーバー クラスターのアップグレード](../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
