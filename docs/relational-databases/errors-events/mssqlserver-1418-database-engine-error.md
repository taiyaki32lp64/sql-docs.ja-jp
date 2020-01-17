---
title: MSSQLSERVER_1418 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1418 (Database Engine error)
ms.assetid: 6e9c7241-0201-44e0-9f8b-b3c4e293f0f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c8f238589f0f9b6641095a4ccb65a4665300a28b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023175"
---
# <a name="mssqlserver1418"></a>MSSQLSERVER_1418
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|1418|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBM_PARTNERNOTFOUND|  
|メッセージ テキスト|サーバー ネットワーク アドレス "%.*ls" にアクセスできないか、このアドレスが存在しません。 ネットワーク アドレス名と、ローカル エンドポイントおよびリモート エンドポイントのポートが操作可能であることを確認してください。|  
  
## <a name="explanation"></a>説明  
指定されたサーバー ネットワーク アドレスにアクセスできないか、このアドレスが存在しないため、サーバー ネットワーク エンドポイントが応答しませんでした。  
  
> [!NOTE]  
> 既定では、すべてのポートが [!INCLUDE[msCoName](../../includes/msconame-md.md)] オペレーティング システムによってブロックされます。  
  
## <a name="user-action"></a>ユーザーの操作  
ネットワーク アドレス名が正しいかどうかを確認して、コマンドを再発行します。  
  
場合によっては、両方のパートナーで修正措置を行う必要があります。 たとえば、プリンシパル サーバー インスタンスで SET PARTNER を実行しようとしたときにこのメッセージが表示された場合、ミラー サーバー インスタンスでのみ修正措置を実行するよう指示されます。 しかし、実際には、両方のパートナーで修正措置を行う必要があります。  
  
### <a name="additional-corrective-actions"></a>その他の修正措置  
  
-   ミラー データベースがミラーリングできる状態であることを確認します。  
  
-   ミラー サーバー インスタンスの名前およびポートが正しいことを確認します。  
  
-   対象となるミラー サーバー インスタンスがファイアウォールの背後に配置されていないことを確認します。  
  
-   プリンシパル サーバー インスタンスがファイアウォールの背後に配置されていないことを確認します。  
  
-   **sys.database_mirroring_endpoints** カタログ ビューの **state** または **state_desc** 列を使用して、両方のパートナーでエンドポイントが開始されていることを確認します。 いずれかのエンドポイントが開始されていない場合は、ALTER ENDPOINT ステートメントを実行して開始します。  
  
-   プリンシパル サーバー インスタンスがデータベース ミラーリング エンドポイントに割り当てられているポートでリッスンし、ミラー サーバー インスタンスがミラー サーバー インスタンスのポートでリッスンしていることを確認します。 詳細については、このトピックの「ポートの可用性の検証」を参照してください。 パートナーが割り当てられたポートでリッスンしていない場合は、データベース ミラーリング エンドポイントを変更して、別のポートでリッスンするようにします。  
  
    > [!IMPORTANT]  
    > セキュリティ構成が不適切な場合、一般的なセットアップ エラー メッセージが表示されることがあります。 通常、サーバー インスタンスは無効な接続要求に応答せず、破棄してしまいます。 呼び出し元には、ミラー データベースの状態が正しくない、ミラー データベースが存在しない、権限が不適切など、別のさまざまな理由でセキュリティ構成エラーが発生したように示される場合があります。  
  
### <a name="using-the-error-log-file-for-diagnosis"></a>診断のためのエラー ログ ファイルの使用  
調査のために利用できるのがエラー ログ ファイルだけである場合があります。 その場合は、エラー ログを参照し、データベース ミラーリング エンドポイントの TCP ポートに対するエラー メッセージ 26023 が含まれていないかどうかを調べます。 重大度 16 のこのエラーは、データベース ミラーリング エンドポイントが開始されていないことを示している可能性があります。 これは、**sys.database_mirroring_endpoints** でエンドポイントの状態が開始済みと示されている場合でも発生します。  
  
発生している問題をすべて解決した後、プリンシパル サーバーで ALTER DATABASE *database_name* SET PARTNER ステートメントを再度実行します。  
  
### <a name="verifying-port-availability"></a>ポートの可用性の検証  
データベース ミラーリング セッションのネットワークを構成する際、各サーバー インスタンスのデータベース ミラーリング エンドポイントがデータベース ミラーリング プロセスでのみ使用されていることを確認します。 データベース ミラーリング エンドポイントに割り当てられたポートで別のプロセスがリッスンしている場合、他のサーバー インスタンスのデータベース ミラーリング プロセスはそのエンドポイントに接続できません。  
  
Windows ベースのサーバーがリッスンしているすべてのポートを表示するには、**netstat** コマンド プロンプト ユーティリティを使用します。 **netstat** の構文は、Windows オペレーティング システムのバージョンによって異なります。 詳細については、オペレーティング システムのマニュアルを参照してください。  
  
#### <a name="windows-server-2003-service-pack-1-sp1"></a>Windows Server 2003 Service Pack 1 (SP1)  
リッスンしているポートおよびそれらのポートを開いているプロセスを一覧表示するには、Windows コマンド プロンプトで次のコマンドを入力します。  
  
**netstat -abn**  
  
#### <a name="windows-server-2003-pre-sp1"></a>Windows Server 2003 (SP1 適用前)  
リッスンしているポートおよびそれらのポートを開いているプロセスを確認するには、次の手順に従います。  
  
1.  プロセス ID を取得します。  
  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのプロセス ID を調べるには、そのインスタンスに接続し、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT SERVERPROPERTY('ProcessID')   
    ```  
  
    詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「SERVERPROPERTY (Transact-SQL)」を参照してください。  
  
2.  取得したプロセス ID と、次の **netstat** コマンドの出力とを照合します。  
  
    **netstat -ano**  
  
## <a name="see-also"></a>参照  
[ALTER ENDPOINT &#40;Transact-SQL&#41;](~/t-sql/statements/alter-endpoint-transact-sql.md)  
[データベース ミラーリング エンドポイント &#40;SQL Server&#41;](~/database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](~/t-sql/functions/serverproperty-transact-sql.md)  
[サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](~/database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)  
[データベース ミラーリング構成のトラブルシューティング &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
