---
title: バインドされたテキスト列と Image 列にバインドされていない |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf8ac0cf868394d9aa8063220939feee69ac2f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62626585"
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>バインドされたtext、image 型の列とバインドされない text、image 型の列
  サーバー カーソルを使用する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにバインドされていないため、データを転送しないように最適化された**テキスト**、 **ntext**、または**イメージ**列で、時間**SQLFetch**が実行されます。 **テキスト**、 **ntext**、または**イメージ**データは実際には取得されません、サーバーからアプリケーションの問題まで[SQLGetData](../native-client-odbc-api/sqlgetdata.md)用、列です。  
  
 多くのアプリケーションを作成できるようにありません**テキスト**、 **ntext**、または**イメージ**中に、ユーザーがカーソル内を上下スクロール単にデータが表示されます。 アプリケーションが呼び出すことができますし、ユーザーは、詳細を表示する行を選択するときに**SQLGetData**を取得する、**テキスト**、 **ntext**、または**イメージ**データ。 これにより、送信、**テキスト**、 **ntext**、または**イメージ**ユーザーの選択、およびことができますがない行のいずれかのデータが非常に大きな転送を防ぐ大量のデータ。  
  
## <a name="see-also"></a>関連項目  
 [テキストとイメージの列の管理](managing-text-and-image-columns.md)   
 [カーソル動作](../native-client-odbc-cursors/cursor-behaviors.md)  
  
  
