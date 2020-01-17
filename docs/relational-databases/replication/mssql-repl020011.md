---
title: MSSQL_REPL020011 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL020011 error
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 348300256bfb6c208cbc3aade0f75a87024ab597
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770081"
---
# <a name="mssqlrepl020011"></a>MSSQL_REPL020011
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20011|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|プロセスは、'%1' を '%2' で実行できませんでした。|  
  
## <a name="explanation"></a>説明  
 このエラーは、ログ リーダー エージェントが **sp_replcmds** を実行したとき (プロセスは、'sp_replcmds' を \<ServerName> で実行できませんでした) や **sp_repldone** を実行したとき (プロセスは、'sp_repldone' を \<ServerName> で実行できませんでした) など、トランザクション レプリケーション処理中のさまざまな状況で発生する可能性があります。  
  
## <a name="user-action"></a>ユーザーの操作  
 バックアップから復元したばかりのデータベースでこのエラーが発生した場合、 **sp_replrestart** の実行 (該当する場合) も含めて、バックアップおよび復元のマニュアルに概説されている手順に従っているかどうかを確認してください。 詳細については、「 [スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)」を参照してください。  
  
 このエラーは内部処理エラーであり、復元以外の状況で発生した場合は、一般的にレプリケーションを削除して再構成する必要があることを示しています。 レプリケーションを削除できない場合は、カスタマー サポートにお問い合わせください。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  
