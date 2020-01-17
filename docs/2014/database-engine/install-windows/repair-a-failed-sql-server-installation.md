---
title: SQL Server 2014 のインストールの修復 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 90c11b28-892b-44d6-978e-0eee48c75b7d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d9486134e0a9103239853d8378e29aea688c7fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "67046663"
---
# <a name="drop-a-sql-server-2014-installation"></a>SQL Server 2014 のインストールの削除
  修復操作は、以下のシナリオで使用できます。  
  
-   適切にインストールした後に壊れた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを修復する。  
  
-   新たにアップグレードされたインスタンスにインスタンス名がマップされた後、アップグレード操作のキャンセルまたは失敗が生じた場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを修復する。  
  
    -   概要ログに次のメッセージが表示されている場合は、失敗したアップグレード インスタンスを修復できます。  
  
         "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレードに失敗しました。 続行するには、失敗の理由を調べて問題を修正し、インストールされたシステムを修復します。"  
  
    -   概要ログに次のメッセージが表示されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアンインストールして、再度インストールする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを修復することはできません。  
  
         "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアップグレードに失敗しました。 続行するには、失敗の理由を調べて問題を修正します。"  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを修復すると、次のようになります。  
  
-   欠落または破損していたすべてのファイルが差し替わります。  
  
-   欠落または破損していたすべてのレジストリ キーが差し替わります。  
  
-   欠落または破損していたすべての構成値が既定値に設定されます。  
  
 続行する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターに関して、次の重要な情報を確認してください。  
  
-   修復は個々のクラスター ノードで実行する必要があります。  
  
-   準備操作に失敗した後でフェールオーバー クラスター ノードを修復するには、 **[ノードの削除]** を使用してから準備手順をもう一度実行します。 詳細については、「[SQL Server フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)」をご覧ください。  
  
### <a name="to-repair-a-failed-installation-of-includessnoversionincludesssnoversion-mdmd-from-the-installation-center"></a>インストール センターから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の失敗したインストールを修復するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール メディアから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラム (setup.exe) を起動します。  
  
2.  必須コンポーネントのインストールとシステムの検証が実行された後、セットアップ プログラムによって [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール センター] ページが表示されます。  
  
3.  左側のナビゲーション領域の **[メンテナンス]** をクリックし、 **[修復]** をクリックして修復操作を開始します。  
  
    > [!TIP]  
    >  [スタート] メニューを使用してインストール センターを起動した場合は、この時点で、インストール メディアの場所を指定する必要があります。  
  
4.  セットアップ サポート ルールおよびセットアップ サポート ファイルのルーチンが実行されて、システムに必須コンポーネントがインストールされていること、およびコンピューターがセットアップの検証ルールに合格していることが確認されます。 続行するには、 **[OK]** または **[インストール]** をクリックします。  
  
5.  [インスタンスの選択] ページで、修復するインスタンスを選択し、 **[次へ]** をクリックします。  
  
6.  修復ルールが実行され、操作が検証されます。 続行するには、 **[次へ]** をクリックします。  
  
7.  [修復の準備完了] ページで、操作を続行する準備ができたことが示されます。 続行するには、 **[修復]** をクリックします。  
  
8.  [修復の進行状況] ページに、修復操作の進行状況が表示されます。 [完了] ページでは、操作が完了したことが示されます。  
  
### <a name="to-repair-a-failed-installation-of-includessnoversionincludesssnoversion-mdmd-using-command-prompt"></a>コマンド プロンプトを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の失敗したインストールを修復するには  
  
1.  コマンド プロンプトで次のコマンドを実行します。  
  
    ```  
    Setup.exe /q /ACTION=Repair /INSTANCENAME=instancename  
    ```  
  
## <a name="see-also"></a>参照  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](view-and-read-sql-server-setup-log-files.md)   
 [インストール方法に関するトピック](../../sql-server/install/installation-how-to-topics.md)  
  
  
