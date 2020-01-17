---
title: dm_pdw_exec_requests (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 15d27881378a88c8f4ae6d65640be6218ecd3530
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632763"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>dm_pdw_exec_requests (Transact-sql)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]で現在または最近アクティブになっているすべての要求に関する情報を保持します。 要求/クエリごとに1行が一覧表示されます。  
  
|列名|[データ型]|説明|範囲|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|このビューのキー。 要求に関連付けられている一意の数値 ID。|システム内のすべての要求間で一意です。|  
|session_id|**nvarchar(32)**|このクエリが実行されたセッションに関連付けられている一意の数値 ID。 「 [Sys. dm_pdw_exec_sessions &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)」を参照してください。||  
|ステータス|**nvarchar(32)**|要求の現在の状態。|' Running '、' 中断 '、' Completed '、' Canceled '、' Failed '。|  
|submit_time|**datetime**|要求が実行のために送信された時刻。|有効な**datetime**が、現在の時刻と start_time の値以下である。|  
|start_time|**datetime**|要求の実行が開始された時刻。|キューに置かれた要求の場合は NULL です。それ以外の場合は、有効な**datetime**が現在の時刻以下であることを指定します。|  
|end_compile_time|**datetime**|エンジンが要求のコンパイルを完了した時刻。|まだコンパイルされていない要求の場合は NULL です。それ以外の場合は、有効な**datetime**が start_time 未満で現在の時刻以下であることを指定します。|
|end_time|**datetime**|要求の実行が完了、失敗、または取り消された時刻。|キューに置かれた要求またはアクティブな要求の場合は Null です。それ以外の場合は、有効な**datetime**が現在の時刻以下であることを指定します。|  
|total_elapsed_time|**int**|要求が開始されてから経過した時間 (ミリ秒単位)。|0 ~ start_time と end_time の差。</br></br> Total_elapsed_time が整数の最大値を超えた場合、total_elapsed_time は引き続き最大値になります。 この条件により、"最大値を超えました。" という警告が生成されます。</br></br> ミリ秒単位の最大値は、24.8 日と同じです。|  
|ラベル●らべる○|**nvarchar (255)**|いくつかの SELECT クエリステートメントに関連付けられているオプションのラベル文字列。|' A-z '、' A-z '、' 0-9 '、' _ ' を含む任意の文字列。|  
|error_id|**nvarchar (36)**|要求に関連付けられているエラーの一意の ID (存在する場合)。|「 [Sys. dm_pdw_errors &#40;&#41;transact-sql」を](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)参照してください。エラーが発生しなかった場合は、NULL に設定します。|  
|database_id|**int**|明示的なコンテキストによって使用されるデータベースの識別子 (たとえば、DB_X を使用します)。|「 [Sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」の「ID」を参照してください。|  
|command|**nvarchar (4000)**|ユーザーによって送信された要求の完全なテキストを保持します。|任意の有効なクエリまたは要求テキスト。 4000バイトを超えるクエリは切り捨てられます。|  
|resource_class|**nvarchar (20)**|この要求に使用するワークロードグループ。 |静的リソース クラス</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>動的リソース クラス</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|要求を実行するときの重要度を設定します。  これは、このワークロードグループでの要求の相対的な重要度であり、共有リソースの複数のワークロードグループにまたがっています。  分類子で指定された重要度は、ワークロードグループの重要度の設定よりも優先されます。</br>適用対象: Azure SQL Data Warehouse|NULL</br>low</br>below_normal</br>標準 (既定値)</br>above_normal</br>high|
|group_name|**sysname** |リソースを利用する要求の場合、group_name は、要求が実行されているワークロードグループの名前です。  要求でリソースが使用されない場合、group_name は null になります。</br>適用対象: Azure SQL Data Warehouse|
|classifier_name|**sysname**|リソースを利用する要求の場合、リソースの割り当てに使用される分類子の名前と重要度。||
|resource_allocation_percentage|**decimal (5, 2)**|要求に割り当てられたリソースの割合。</br>適用対象: Azure SQL Data Warehouse|
|result_set_cache|**bit**|完了したクエリの結果がキャッシュヒット (1) であるかどうか、またはそれ以外 (0) であるかどうかを詳細に説明します。 </br>適用対象: Azure SQL Data Warehouse|0、1|
||||
  
 このビューで保持される最大行数の詳細については、「[容量制限](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)」トピックの「メタデータ」セクションを参照してください。
  
## <a name="permissions"></a>アクセス許可

 VIEW SERVER STATE 権限が必要です。  
  
## <a name="security"></a>セキュリティ

 dm_pdw_exec_requests は、データベース固有のアクセス許可に従ってクエリ結果をフィルター処理しません。 VIEW SERVER STATE 権限を持つログインは、すべてのデータベースの結果のクエリ結果を取得できます。  
  
>[!WARNING]  
>攻撃者は、dm_pdw_exec_requests を使用して、VIEW SERVER STATE 権限を持ち、データベース固有の権限がないことで、特定のデータベースオブジェクトに関する情報を取得できます。  
  
## <a name="see-also"></a>参照

 [SQL Data Warehouse および並列データウェアハウスの動的管理&#40;ビュー transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
