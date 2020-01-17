---
title: アセンブリの削除 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- assemblies [CLR integration], removing
- dropping assemblies
ms.assetid: 03481034-dc91-4488-ab24-ba44243e2690
author: rothja
ms.author: jroth
ms.openlocfilehash: f28f51f73faca8a72bdea3b8af70e14046d73f8d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074345"
---
# <a name="dropping-an-assembly"></a>アセンブリの削除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  CREATE ASSEMBLY ステートメントを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に登録された各アセンブリは、そのアセンブリで提供される機能が不要になれば削除できます。 アセンブリを削除すると、アセンブリと、デバッグ ファイルなどこれに関連するファイルがすべて、データベースから削除されます。 アセンブリを削除するには、DROP ASSEMBLY ステートメントを次の構文で使用します。  
  
```  
DROP ASSEMBLY MyDotNETAssembly  
```  
  
 DROP ASSEMBLY は、現在実行中のアセンブリを参照するコードに影響を与えることはありませんが、DROP ASSEMBLY を実行後は、アセンブリ コードを起動しようとすると失敗します。  
  
 アセンブリがデータベースに存在する別のアセンブリにより参照されている場合、または、アセンブリが現在のデータベースで共通言語ランタイム (CLR) 関数、プロシージャ、トリガー、ユーザー定義型 (UDT)、ユーザー定義集計 (UDA) により使用されている場合、DROP ASSEMBLY はエラーを返します。 まず、DROP AGGREGATE、DROP FUNCTION、DROP PROCEDURE、DROP TRIGGER、および DROP TYPE ステートメントを使用して、アセンブリに含まれるすべてのマネージド データベース オブジェクトを削除します。  
  
## <a name="removing-a-udt-from-the-database"></a>データベースからの UDT の削除  
 DROP TYPE ステートメントを使用すると、現在のデータベースから UDT が削除されます。 UDT を削除すると、DROP ASSEMBLY ステートメントを使用してデータベースからアセンブリを削除できます。  
  
 次の状況のように、オブジェクトが UDT に依存している場合、DROP TYPE ステートメントは失敗します。  
  
-   UDT を使用して定義した列を含むデータベース内のテーブル。  
  
-   WITH SCHEMABINDING 句を使用してデータベースに作成した UDT の変数またはパラメーターを使用する関数、ストアド プロシージャ、またはトリガー。  
  
### <a name="finding-udt-dependencies"></a>UDT 依存関係の検出  
 最初にすべての依存オブジェクトを削除してから、DROP TYPE ステートメントを実行する必要があります。 次[!INCLUDE[tsql](../../../includes/tsql-md.md)]クエリは、すべての列とで UDT を使用するパラメーターを検索、 **AdventureWorks**データベース。  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;   
```  
  
## <a name="see-also"></a>関連項目  
 [CLR 統合アセンブリの管理](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [アセンブリの変更](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [アセンブリを作成します。](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [DROP AGGREGATE &#40;TRANSACT-SQL&#41;](../../../t-sql/statements/drop-aggregate-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-function-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-procedure-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-trigger-transact-sql.md)   
 [ドロップ タイプ&#40;TRANSACT-SQL&#41;](../../../t-sql/statements/drop-type-transact-sql.md)  
  
  
