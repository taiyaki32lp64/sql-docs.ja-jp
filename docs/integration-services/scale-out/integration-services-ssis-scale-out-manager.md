---
title: SQL Server Integration Services Scale Out Manager | Microsoft Docs
description: この記事では、SSIS Scale Out の管理に使用できる Scale Out Manager ツールについて説明します
ms.custom: performance
ms.date: 12/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 06708cc6770779f22bea45eddacba5a5d29f9092
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082135"
---
# <a name="integration-services-scale-out-manager"></a>Integration Services Scale Out Manager

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out Manager は、1 つのアプリから SSIS Scale Out トポロジ全体を管理できる管理ツールです。 管理タスクを減らし、複数のコンピューターで Transact-SQL コマンドを実行するという負担をなくします。

## <a name="open-scale-out-manager"></a>Scale Out Manager を開く

Scale Out Manager は 2 つの方法で開くことができます。

### <a name="1-open-scale-out-manager-from-sql-server-management-studio"></a>1.SQL Server Management Studio から Scale Out Manager を開く
SQL Server Management Studio (SSMS) を開き、Scale Out Master の SQL Server インスタンスに接続します。

オブジェクト エクスプローラーで、 **[SSISDB]** を右クリックして、 **[スケール アウトの管理]** を選択します。

![スケール アウトの管理](media/manage-scale-out.PNG)

> [!NOTE]
> SSMS は管理者として実行することをお勧めします。Scale Out Worker の追加など、一部のスケール アウト管理操作には管理者特権が必要になるためです。

### <a name="2-open-scale-out-manager-by-running-managementtoolexe"></a>2.ManagementTool.exe を実行して Scale Out Manager を開く

`%SystemDrive%\Program Files (x86)\Microsoft SQL Server\150\DTS\Binn\Management` の下で `ManagementTool.exe` を見つけます。 **ManagementTool.exe** を右クリックし、 **[管理者として実行]** を選択します。 

Scale Out Manager を開いたら、Scale Out Master の SQL Server インスタンス名を入力し、それに接続し、スケール アウト環境を管理します。

![ポータルの接続](media/portal-connect-new.png)

## <a name="tasks-available-in-scale-out-manager"></a>Scale Out Manager で利用できるタスク
Scale Out Manager で、次の操作を実行できます。

### <a name="enable-scale-out"></a>スケール アウトの有効化
SQL Server に接続した後で、Scale Out が有効になっていない場合、 **[有効]** を選択して有効にできます。

![ポータルで Scale Out を有効にする](media/portal-enable-scale-out-new.PNG) 

### <a name="view-scale-out-master-status"></a>Scale Out Master の状態を表示する
Scale Out Master の状態は、 **[ダッシュボード]** ページに表示されます。

![ポータルのダッシュボード](media/portal-dashboard-new.PNG)

### <a name="view-scale-out-worker-status"></a>Scale Out Worker の状態を表示する
Scale Out Worker の状態は、 **[ワーカー マネージャー]** ページに表示されます。 各ワーカーを選択すると、個別の状態を表示できます。

![ポータルのワーカー マネージャー](media/portal-worker-manager-new.PNG)

### <a name="add-a-scale-out-worker"></a>Scale Out Worker を追加する
Scale Out Worker を追加するには、Scale Out Worker リストの下部にある **[+]** を選択します。 

追加する Scale Out Worker のコンピューター名を入力し、 **[検証]** をクリックします。 Scale Out Manager によって、現在のユーザーが Scale Out Master と Scale Out Worker のコンピューター上の証明書ストアにアクセスできるかどうかがチェックされます。

![ワーカーの接続](media/connect-worker-new.PNG)

検証に合格すると、Scale Out Manager はワーカーのサーバー構成ファイルを読み取り、ワーカーの証明書のサムプリントを取得します。 詳細については、[Scale Out Worker](integration-services-ssis-scale-out-worker.md) に関するページを参照してください。 Scale Out Manager がワーカー サービス構成ファイルを読み取れない場合、ワーカー証明書を提供するための 2 つの代替方法があります。 

- ワーカー証明書のサムプリントを直接入力するか、

    ![ワーカー証明書 1](media/portal-cert1-new.PNG)

- 証明書ファイルを提供します。

    ![ワーカー証明書 2](media/portal-cert2-new.PNG)

情報を収集すると、実行されるアクションの説明が Scale Out Manager に表示されます。 実行されるアクションには通常、証明書のインストール、ワーカー サービス構成ファイルの更新、ワーカー サービスの再開などがあります。

![ポータルの追加の確認 1](media/portal-add-confirm1-new.PNG)

ワーカー設定にアクセスできない場合は、それを手動で更新してからワーカー サービスを再起動する必要があります。

![ポータルの追加の確認 2](media/portal-add-confirm2-new.PNG)

**[確認]** チェックボックスを選択し、 **[OK]** を選択し、Scale Out Worker の追加を開始します。

### <a name="delete-a-scale-out-worker"></a>Scale Out Worker を削除する
Scale Out Worker を削除するには、Scale Out Worker を選択し、Scale Out Worker リストの下部にある **[-]** を選択します。

### <a name="enable-or-disable-a-scale-out-worker"></a>Scale Out Worker を有効または無効にする
Scale Out Worker を有効または無効にするには、Scale Out Worker を選択し、 **[ワーカーの有効化]** または **[ワーカーの無効化]** を選択します。 ワーカーがオフラインではない場合、Scale Out Manager に表示されるワーカーの状態が適宜変更されます。

## <a name="edit-a-scale-out-worker-description"></a>Scale Out Worker の説明を編集する
Scale Out Worker の説明を編集するには、Scale Out Worker を選択し、 **[編集]** を選択します。 説明の編集が終わったら、 **[保存]** を選択します。

![ポータルのワーカーの保存](media/portal-save-worker-new.PNG)

## <a name="next-steps"></a>次の手順
詳細については、次の記事をご覧ください。
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
