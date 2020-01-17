---
title: sp_cdc_cleanup_change_table (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: rothja
ms.author: jroth
ms.openlocfilehash: 51c0af34fb3158cc5032ee9ef53abce22d8ecc3a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909330"
---
# <a name="syssp_cdc_cleanup_change_table-transact-sql"></a>sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定された*low_water_mark*値に基づいて、現在のデータベースの変更テーブルから行を削除します。 このストアドプロシージャは、変更テーブルのクリーンアッププロセスを直接管理する必要があるユーザー向けに用意されています。 ただし、このプロシージャは、変更テーブルに含まれるデータのすべてのコンシューマーに影響を及ぼすため、使用する際は注意が必要です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>引数  
 [ @capture_instance = ] '*capture_instance*'  
 変更テーブルに関連付けられたキャプチャ インスタンスの名前を指定します。 *capture_instance* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
 *capture_instance*は、現在のデータベースに存在するキャプチャインスタンスに名前を指定する必要があります。  
  
 [ @low_water_mark = ] *low_water_mark*  
 *キャプチャインスタンス*の新しい低レベルのウォーターマークとして使用するログシーケンス番号 (LSN) を指定します。 *low_water_mark*は**binary (10)** ,、既定値はありません。  
  
 値が null 以外の場合は、 [lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)テーブル内の現在のエントリの start_lsn 値として表示される必要があります。 cdc.lsn_time_mapping の他のエントリが、新しい低レベルのウォーターマークで識別されたエントリと同じコミット時間を共有する場合、そのグループのエントリに関連付けられた最小 LSN が低レベルのウォーターマークとして選択されます。  
  
 値が明示的に NULL に設定されている場合、*capture_instance* の現在の*低レベルのウォーターマーク*は、クリーンアップ操作の上限を定義するために使用されます。  
  
 [ @threshold= ] '*delete threshold*'  
 クリーンアップで1つのステートメントを使用して削除できる削除エントリの最大数を指定します。 *delete_threshold*は**bigint**,、既定値は5000です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [InclusionThresholdSetting]  
  
## <a name="remarks"></a>Remarks  
 sys.sp_cdc_cleanup_change_table は次の操作を実行します。  
  
1.  @low_water_mark パラメーターが NULL でない場合は、*capture instance* の start_lsn の値を新しい*低レベルのウォーターマーク*に設定します。  
  
    > [!NOTE]  
    >  新しい低レベルのウォーターマークは、ストアド プロシージャ呼び出しで指定されている低レベルのウォーターマークと異なる場合があります。 cdc.lsn_time_mapping テーブルの他のエントリが同じコミット時間を共有する場合、そのグループのエントリで表される最小の start_lsn が、調整された低レベルのウォーターマークとして選択されます。 @low_water_mark パラメーターが NULL の場合、または現在の低レベルのウォーターマークが新しい lowwatermark より大きい場合、キャプチャインスタンスの start_lsn 値は変更されません。  
  
2.  変更テーブル エントリが持つ __$start_lsn の値が低レベルのウォーターマークより小さい場合は、その変更テーブル エントリが削除されます。 削除のしきい値は、1つのトランザクションで削除される行の数を制限するために使用されます。 エントリを正常に削除できなかった場合は、が報告されますが、呼び出しに基づいて作成されたキャプチャインスタンスの低レベルのウォーターマークに対する変更には影響しません。  

 sys.sp_cdc_cleanup_change_table は、次のような場合に使用します。  
  
-   クリーンアップエージェントジョブによって削除エラーが報告されます。  
  
     管理者は、このストアドプロシージャを明示的に実行して、失敗した操作を再試行できます。 特定の capture instance のクリーンアップを再試行するには、sp_cdc_cleanup_change_table を実行し、@low_water_mark パラメーターに NULL を指定します。  
  
-   クリーンアップエージェントジョブで使用される単純なリテンション期間に基づくポリシーは、十分ではありません。  
  
     このストアドプロシージャは、1つの capture instance に対してクリーンアップを実行するため、個々の capture instance に対するクリーンアップルールをカスタマイズするカスタムクリーンアップ戦略を作成するために使用できます。  
  
## <a name="permissions"></a>アクセス許可  
 db_owner 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;&#40;Transact-SQL&#41;   ](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [fn_cdc_get_min_lsn &#40;Transact-SQL&#41; ](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
