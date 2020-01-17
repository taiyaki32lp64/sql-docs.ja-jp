---
title: マスターのものと一致し、model データベースの照合順序のユーザー定義データベースの設定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c686446f-dae1-4b05-a3df-837b3422988d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dfb00b1cc1a9930f7a374403b40e2c0d793eb090
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773315"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-those-of-the-master-and-model-databases"></a>ユーザー定義データベースの照合順序が master データベースおよび model データベースの照合順序と一致するように設定
  このルールでは、ユーザー定義データベースの定義に使用されたデータベース照合順序と master または model の照合順序が一致しているかどうかを確認します。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 ユーザー定義データベースの照合順序と master または model データベースの照合順序を一致させることをお勧めします。 照合順序が一致していない場合、照合順序の競合が発生してコードが実行されなくなる可能性があります。 たとえば、ストアド プロシージャによってあるテーブルを一時テーブルに結合すると、ユーザー定義のデータベースと model データベースの照合順序が異なる場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ではバッチが終了し、照合順序の競合エラーが返されることがあります。 この現象は、一時テーブルが tempdb に作成されることが原因で発生します。tempdb の照合順序は、model データベースの照合順序に基づいています。  
  
 照合順序の競合エラーが発生した場合は、次のいずれかの解決策を検討してください。  
  
-   データをユーザー データベースからエクスポートし、照合順序が master データベースおよび model データベースと同じ新しいテーブルにインポートします。  
  
-   ユーザー データベースの照合順序と一致する照合順序を使用するようにシステム データベースを再構築します。 システム データベースを再構築する方法の詳細については、次を参照してください。[システム データベースの再構築](../relational-databases/databases/system-databases.md)します。  
  
-   ユーザー テーブルを tempdb 内のテーブルに結合するストアド プロシージャを、ユーザー データベースの照合順序を使用して tempdb にテーブルを作成するように変更します。 これを行うには、次の例に示すように、一時テーブルの列定義に `COLLATE database_default` 句を追加します。  
  
    ```  
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )  
    ```  
  
## <a name="for-more-information"></a>詳細情報  
 [データベースの照合順序の設定または変更](../relational-databases/collations/set-or-change-the-database-collation.md)  
  
 [列の照合順序の設定または変更](../relational-databases/collations/set-or-change-the-column-collation.md)  
  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [Microsoft Knowledge Base article 325335](https://go.microsoft.com/fwlink/?linkid=117751)  
  
 [方法:コマンド プロンプトから SQL Server 2008 をインストールします。](https://go.microsoft.com/fwlink/?LinkId=81585)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
