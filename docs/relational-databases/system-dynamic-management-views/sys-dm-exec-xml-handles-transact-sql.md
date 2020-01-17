---
title: sys.dm_exec_xml_handles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
author: pmasl
ms.author: pelopes
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 303ceed8cc7078e4025f160d25ce1474d1be6aed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936784"
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  によって開かれたアクティブ ハンドルに関する情報を返します**sp_xml_preparedocument**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>引数  
 *session_id* | 0,  
 セッションの ID を指定します。 場合*session_id*を指定すると、この関数は、指定したセッションで XML ハンドルに関する情報を返します。  
  
 0 を指定した場合、この関数ではすべてのセッションのすべての XML ハンドルに関する情報が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|この XML ドキュメントを保持しているセッションのセッション ID を処理します。|  
|**document_id**|**int**|によって返される XML ドキュメント ハンドル ID **sp_xml_preparedocument**します。|  
|**namespace_document_id**|**int**|3 番目のパラメーターとして渡された名前空間が関連付けられているドキュメントに使用される内部ハンドル ID **sp_xml_preparedocument**します。 名前空間ドキュメントがない場合は NULL になります。|  
|**sql_handle**|**varbinary(64)**|ハンドルが定義されている SQL コードのテキストへのハンドル。|  
|**statement_start_offset**|**int**|現在実行中に文字数のバッチまたはストアド プロシージャを**sp_xml_preparedocument**呼び出しが発生します。 組み合わせて使用することができます、 **sql_handle**、 **statement_end_offset**、および**sys.dm_exec_sql_text**動的管理関数を取得する、現在要求のステートメントを実行します。|  
|**statement_end_offset**|**int**|現在実行中に文字数のバッチまたはストアド プロシージャを**sp_xml_preparedocument**呼び出しが発生します。 組み合わせて使用することができます、 **sql_handle**、 **statement_start_offset**、および**sys.dm_exec_sql_text**動的管理関数を取得する、現在要求のステートメントを実行します。|  
|**creation_time**|**datetime**|タイムスタンプと**sp_xml_preparedocument**が呼び出されました。|  
|**original_document_size_bytes**|**bigint**|(バイト単位)、未解析の XML ドキュメントのサイズ。|  
|**original_namespace_document_size_bytes**|**bigint**|(バイト単位)、未解析の XML 名前空間ドキュメントのサイズ。 名前空間ドキュメントがない場合は NULL になります。|  
|**num_openxml_calls**|**bigint**|このドキュメント ハンドルを OPENXML 呼び出しの数。|  
|**row_count**|**bigint**|このドキュメント ハンドルに対する前のすべての OPENXML 呼び出しによって返される行の数。|  
|**dormant_duration_ms**|**bigint**|OPENXML の最後の呼び出し以降のミリ秒数。 OPENXML が呼び出されていない場合は、以降のミリ秒数を返します、 **sp_xml_preparedocumen**t 呼び出し。|  
  
## <a name="remarks"></a>コメント  
 有効期間**sql_handle**への呼び出しを実行する SQL テキストを取得するために使用**sp_xml_preparedocument**クエリを実行するために使用するキャッシュされたプランよりも長くなります。 クエリ テキストがキャッシュ内で使用できない場合は、関数の結果に示された情報を使用してデータを取得することはできません。 これは、多くの大きなバッチを実行している場合に発生します。  
  
## <a name="permissions"></a>アクセス許可  
 すべてのセッションまたはセッション Id が、呼び出し元が所有していないを確認するサーバーの VIEW SERVER STATE 権限が必要です。 呼び出し元が、自分の現在のセッション ID のデータを常に表示します。      
  
## <a name="examples"></a>使用例  
 次の例では、アクティブ ハンドルをすべて選択します。  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>関連項目  
 <br>[動的管理ビューおよび関数 (TRANSACT-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
 <br>[実行関連の動的管理ビューおよび関数 (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
 <br>[sp_xml_preparedocument (TRANSACT-SQL)](../system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[sp_xml_removedocument (TRANSACT-SQL)](../system-stored-procedures/sp-xml-removedocument-transact-sql.md)


 
  
  
