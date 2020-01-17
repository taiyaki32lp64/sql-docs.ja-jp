---
title: クエリとプロジェクト内の接続との関連付け | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server Management Studio], query associations
- projects [SQL Server Management Studio], connections
- projects [SQL Server Management Studio], query connections
- query associations [SQL Server Management Studio]
ms.assetid: c9625ae0-29c1-4179-a709-51b7e2f9e23d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 247258298acbe8af4a68c0cd0b981cd04deb26ba
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68258142"
---
# <a name="associate-a-query-with-a-connection-in-a-project"></a>クエリとプロジェクト内の接続との関連付け
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
クエリを接続の指定なしで作成した場合、またはクエリを別のプロジェクトに移動する場合は、そのクエリは現在のプロジェクト内の接続に関連付けられません。  
  
### <a name="to-associate-a-query-with-a-connection-in-a-project"></a>クエリをプロジェクト内の接続に関連付けるには  
  
1.  クエリをクエリ エディターで開いている場合は、クエリ エディターの空白部分を右クリックして **[接続]** をポイントし、 **[接続]** をクリックします。 クエリが開いていない場合は、ソリューション エクスプローラーでクエリをダブルクリックし、クエリを接続します。  
  
2.  **[データベース エンジンへの接続]** ダイアログ ボックスで、接続情報を入力します。 接続情報が既存の接続に一致すると、クエリはその接続に関連付けられます。  
  
## <a name="see-also"></a>参照  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[クエリに関連付けられた接続の変更](../../ssms/solution/change-the-connection-associated-with-a-query.md)  
[プロジェクト内の接続のプロパティを表示または変更する方法](../../ssms/solution/view-or-change-the-properties-of-a-connection-in-a-project.md)  
  
