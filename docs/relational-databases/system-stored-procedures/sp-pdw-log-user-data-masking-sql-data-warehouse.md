---
title: sp_pdw_log_user_data_masking (SQL データ ウェアハウス) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 18798dece1c801ad0cc4854b7fccc15529a56d5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056452"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL データ ウェアハウス)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_log_user_data_masking**ユーザーのデータのマスキングを有効にする[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。 ユーザー データのマスキングでは、アプライアンス上のすべてのデータベースでのステートメントに影響します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログを受ける**sp_pdw_log_user_data_masking**特定は[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。 **sp_pdw_log_user_data_masking**データベースのトランザクション ログには影響しませんまたは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラー ログ。  
  
 **背景知識:** 既定の構成で[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログが完全に含む[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメント、およびによってなどの操作に含まれるユーザー データを含める**挿入**、 **UPDATE**と**選択**ステートメント。 アプライアンス上の問題が発生した場合は、問題を再現するがなくても問題の原因となった状況の分析を許可します。 ユーザー データが書き込まれることを防ぐために[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ、顧客は、このストアド プロシージャを使用してユーザー データのマスキングを有効にすることを選択できます。 ステートメントが引き続きに書き込まれます[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]動作状況のログがいくつかの定義済みの定数値に置き換えられます; ユーザー データを含む可能性のあるステートメント内のリテラルを隠蔽することができます。  
  
 アプライアンスの透過的なデータ暗号化が有効な場合は、内のユーザー データのマスキング[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログが自動的にオンにします。  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>パラメーター  
`[ @masking_mode = ] masking_mode` 透過的なデータ暗号化ログ ユーザー データのマスキングが有効になっているかどうかを判断します。 *masking_mode*は**int**値は次のいずれかを指定できます。  
  
-   0 = 無効、ユーザーに表示されるデータ、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。  
  
-   1 = 有効、ユーザーがデータのステートメントでの表示、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログは、ユーザー データはマスクされています。  
  
-   2 = ステートメントにユーザー データを含むは書き込まれません、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。  
  
 実行**sp_pdw log_user_data_masking**パラメーターでは、TDE ログ ユーザー データのマスキングの現在の状態を返すスカラーの結果セットとしてアプライアンス上なくです。  
  
## <a name="remarks"></a>コメント  
 ユーザーのデータのマスキング[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティで定義済みの定数値を持つリテラルの置換を有効をログ**選択**や DML ステートメントでは、ユーザー データを含めることができるようにします。 設定*masking_mode*を 1 にマスクしません、列名またはテーブル名などのメタデータ。 設定*masking_mode* 2 列名またはテーブル名などのメタデータを持つステートメントを削除します。  
  
 ユーザーのデータのマスキング[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログは、次のように実装されます。  
  
-   TDE とユーザー データのマスキング[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログは既定でオフにします。 ステートメントは自動的にマスクされないアプライアンスでデータベースの暗号化が有効でない場合。  
  
-   ユーザー データのマスキング アプライアンスで TDE を自動的に有効にするオン[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。  
  
-   TDE を無効にした場合、ユーザーのデータのマスキングは影響しません[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログ。  
  
-   ユーザー データのマスキングでは、明示的に有効に[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]アクティビティ ログを使用して、 **sp_pdw_log_user_data_masking**プロシージャ。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定データベース ロール、または**CONTROL SERVER**権限。  
  
## <a name="example"></a>例  
 次の例では、TDE のログ ユーザー データが、アプライアンスのマスクを有効します。  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
