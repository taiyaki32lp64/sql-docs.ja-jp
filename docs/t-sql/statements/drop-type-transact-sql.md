---
title: DROP TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP TYPE
- DROP_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [SQL Server], deleting
- UDTs [SQL Server], deleting
- alias data types [SQL Server], removing
- DROP TYPE statement
ms.assetid: 11bf83f9-0718-4238-a835-83d2eb14ae7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 00659f76da827bf5e00df72d966b32ec56e1f7ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072111"
---
# <a name="drop-type-transact-sql"></a>DROP TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベースから、別名データ型または共通言語ランタイム (CLR) ユーザー定義型を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
DROP TYPE [ IF EXISTS ] [ schema_name. ] type_name [ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
  
 条件付きでは既に存在する場合にのみ、型を削除します。  
  
 *schema_name*  
 別名データ型またはユーザー定義型が属するスキーマの名前を指定します。  
  
 *type_name*  
 削除する別名データ型またはユーザー定義型の名前を指定します。  
  
## <a name="remarks"></a>Remarks  
 次のいずれかに当てはまる場合には、DROP TYPE ステートメントは実行されません。  
  
-   別名データ型またはユーザー定義型の列を含むテーブルがデータベースにある場合。 別名型またはユーザー定義型の列の情報は、[sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) カタログ ビューまたは [sys.column_type_usages](../../relational-databases/system-catalog-views/sys-column-type-usages-transact-sql.md) カタログ ビューをクエリすることによって取得できます。  
  
-   計算列、CHECK 制約、スキーマ バインド ビュー、およびスキーマ バインド関数の中には、別名型またはユーザー定義型への参照を含む定義を持つものもあります。 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) カタログ ビューに対してクエリを実行することによって、これらの参照についての情報を取得できます。  
  
-   データベースに関数、ストアド プロシージャ、またはトリガーが作成されていて、それらのルーチンが、削除しようとしている別名データ型またはユーザー定義型の変数やパラメーターを使用している場合。 別名型またはユーザー定義型のパラメーターについての情報は、[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) カタログ ビューまたは [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md) カタログ ビューに対するクエリを実行することによって取得できます。  
  
## <a name="permissions"></a>アクセス許可  
 *type_name* に対する CONTROL 権限、または *schema_name* に対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`ssn` という名前の型が現在のデータベースに既に作成されていることを前提としています。  
  
```  
DROP TYPE ssn ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
