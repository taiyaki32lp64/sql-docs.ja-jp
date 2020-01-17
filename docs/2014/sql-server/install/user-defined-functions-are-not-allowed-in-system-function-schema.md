---
title: ユーザー定義関数は system_function_schema では許可されません |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- system functions [SQL Server]
- user-defined functions [SQL Server], system
ms.assetid: 3cb54053-ef65-4558-ae96-8686b6b22f4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 10813b7bc0a97f0ba8a81f3f48447142659cd596
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091329"
---
# <a name="user-defined-functions-are-not-allowed-in-systemfunctionschema"></a>system_function_schema でユーザー定義関数が許可されない
  アップグレード アドバイザーは、文書化されていないユーザーによって所有されているユーザー定義関数を検出しました。 **system_function_schema**します。 このユーザーを指定してユーザー定義のシステム関数を作成することはできません。 **System_function_schema**ユーザー名が存在しないため、この名前に関連付けられているユーザー ID (UID = 4) に予約されている、 **sys**スキーマと、内部使用のみに制限されます。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 システム オブジェクトの格納とアクセスが次のように変更されました。  
  
-   システム オブジェクトは、読み取り専用に格納されている**リソース**データベース、およびダイレクトのシステム オブジェクトの更新は許可されていません。  
  
     システム オブジェクトに論理的に表示される、 **sys**すべてのデータベースのスキーマ。 これにより、1 つの要素で構成される関数名を指定してデータベースからシステム関数を呼び出す機能が維持されます。 たとえば、ステートメント `SELECT * FROM fn_helpcollations()` はどのデータベースからでも実行できます。  
  
-   文書化されていないユーザー **system_function_schema**が削除されました。  
  
-   ID に関連付けられているユーザー **system_function_schema** (UID = 4) に予約されている、 **sys**スキーマと、内部使用のみに制限されます。  
  
 これらの変更によって、ユーザー定義のシステム関数には次の影響があります。  
  
-   データ定義言語 (DDL) ステートメントを参照する**system_function_schema**は失敗します。 たとえば、ステートメント`CREATE FUNCTION system`_`function` \_ `schema.fn` \_ `MySystemFunction` .成功しません。  
  
-   アップグレードした後[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、既存のオブジェクトによって所有されている**system_function_schema**でのみに含まれている、 **sys**のスキーマ、**マスター**データベース。 これらの関数を変更または削除するシステム オブジェクトが変更されることはできません、ためはことはありません、**マスター**データベース。 また、これらの関数は、1 つの要素だけで構成される関数名を指定して他のデータベースから呼び出すこともできません。  
  
## <a name="corrective-action"></a>修正措置  
 アップグレードする前に、以下の作業を完了してください。  
  
1.  既存のユーザー定義関数の所有権を変更**dbo**を使用して、 **sp_changeobjectowner**システム ストアド プロシージャ。  
  
2.  プレフィックス 'fn_' を使用しないように関数名を変更することを検討します。 これにより、現在または今後のシステム関数で名前の競合が発生するのを防ぐことができます。  
  
3.  変更した関数のコピーを、その関数を使用するすべてのデータベースに追加します。  
  
4.  参照を置き換える**system_function_schema**で**dbo**でユーザー定義関数 DDL ステートメントが含まれているすべてのスクリプト。  
  
5.  2 つの部分名 dbo を使用するこれらの関数を呼び出すスクリプトを変更して **.** _function_name_、または 3 つの部分名_database_name_ **.** dbo します。*function_name*します。  
  
 詳細については、SQL Server オンライン ブックの次のトピックを参照してください。  
  
-   "sp_changeobjectowner"  
  
-   「ユーザーとスキーマの分離」  
  
-   Resource データベース  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)   
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [システム オブジェクトを変更するステートメントを削除します。](../../../2014/sql-server/install/remove-statements-that-modify-system-objects.md)   
 [システム オブジェクトを破棄するステートメントを削除する](../../../2014/sql-server/install/remove-statements-that-drop-system-objects.md)  
  
  
