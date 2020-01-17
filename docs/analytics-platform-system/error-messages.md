---
title: エラー メッセージ
description: 並列データウェアハウス (PDW) のエラーメッセージは、PDW コンポーネントによって発生したエラーと問題を報告します。また、PDW によって表示される SQL Server エラーを含めることもできます。 これらのエラーメッセージは、一貫した構文を使用して情報を提示します。 この構文を理解することで、問題を特定して修正することができます。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401163"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>並列データウェアハウスのエラーメッセージ

並列データウェアハウス (PDW) のエラーメッセージは、PDW コンポーネントによって発生したエラーと問題を報告します。また、PDW によって表示される SQL Server エラーを含めることもできます。 これらのエラーメッセージは、一貫した構文を使用して情報を提示します。 この構文を理解することで、SQL Server PDW に関する問題を特定し、修正することができます。  
  
## <a name="Basics"></a>エラーメッセージの基本  
返されるエラーメッセージは、同じ構文に従います。  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
各フィールドに指定できる値は次のとおりです。  
  
|フィールド|説明|例|  
|---------|---------------|-----------|  
|*Error_Indicator*|"エラー" またはその他のテキストは、ユーザーに問題を警告します。|ERROR|  
|*SQL_State_Code*|ODBC 仕様に準拠した SQL 状態コード。 ドライバーは、アプリケーションにメッセージを返すたびに、適切な SQL 状態コードを生成します。 "Microsoft" というテキストは、エラーの原因を示します。|42000|  
|*Driver_Details*|ドライバー依存の詳細 (使用するドライバーの種類など)。|ODBC SQL Server 2008 R2 並列データウェアハウスドライバー|  
|*QueryID*|クエリの一意の識別子。 クエリの処理に関連する追加情報を検索するには、この値を使用します。 たとえば、クエリの実行の詳細は、管理コンソールでクエリ ID を使用して見つけることができます。 詳細については、「[管理コンソールを使用してアプライアンスを監視する](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。<br /><br />QueryID が適用されない場合は、"Internal" というテキストがユーザーに返されます。|QID2377|  
|*Message_String*|人間が判読できるエラーまたは問題の説明。 SQL Server エラーを返すと、SQL Server メッセージテキストになります。|UPDATE ステートメントの set リストには、同一の代入のみを含めることができます。|  
  
これらの例の値は、次のようにユーザーに表示されます。  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[管理コンソールのアラートについて](understanding-admin-console-alerts.md)  
  
