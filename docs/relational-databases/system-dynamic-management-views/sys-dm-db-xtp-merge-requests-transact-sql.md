---
title: sys.dm_db_xtp_merge_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f522fde05ce951575d3e02b3cdc4d3336056bd4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026805"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (TRANSACT-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

データベースのマージ要求を追跡します。 マージ要求が SQL Server によって生成されたかを持つユーザーによって要求が行われる可能性がありますが[sys.sp_xtp_merge_checkpoint_files (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)します。

> [!NOTE]
> この動的管理ビュー (DMV)、Microsoft SQL Server 2014 まで sys.dm_db_xtp_merge_requests が存在します。
> この DMV を SQL Server 2016 以降が適用されなくなった。

## <a name="columns-in-the-report"></a>レポート内の列

| 列名 | データ型 | 説明 |
| :-- | :-- | :-- |
| request_state | TINYINT | マージ要求の状態。<br/>0 = 要求<br/>1 = 保留中<br/>2 = インストールされています。<br/>3 = 破棄 |
| request_state_desc | nvarchar(60) | 要求の現在の状態の意味があります。<br/><br/>要求のマージ要求が存在します。<br/>保留中のマージが処理中です。<br/>マージはインストールが完了しました。<br/>-破棄されたマージを完了できませんでした、おそらくストレージの容量不足が原因です。 |
| destination_file_id | GUID | ソース ファイルのマージ先のファイルの一意の識別子。 |
| lower_bound_tsn | BIGINT | マージ先ファイルの最小のタイムスタンプ。 マージするすべてのソース ファイルの最下位のトランザクションのタイムスタンプ。 |
| upper_bound_tsn | BIGINT | マージ先ファイルの最大のタイムスタンプ。 マージするすべてのソース ファイルの最上位のトランザクションのタイムスタンプ。 |
| collection_tsn | BIGINT | 現在の行の収集されたタイムスタンプです。<br/><br/>インストール済み状態の行は、checkpoint_tsn が collection_tsn より大きい場合に削除されます。<br/><br/>Abandoned 状態の行は、checkpoint_tsn が collection_tsn より小さいと削除されます。 |
| checkpoint_tsn | BIGINT | チェックポイントが開始された時刻。<br/><br/>この値より小さいタイムスタンプを持つトランザクションによって実施されたすべての削除は、新しいデータ ファイルに反映されます。 残りの削除は、ターゲットのデルタ ファイルに移動されます。 |
| sourcenumber_file_id | GUID | マージのソース ファイルを一意に識別する最大 16 個の内部ファイル Id。 |

## <a name="permissions"></a>アクセス許可

現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。

## <a name="see-also"></a>関連項目

[メモリ最適化テーブルの動的管理ビュー (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
