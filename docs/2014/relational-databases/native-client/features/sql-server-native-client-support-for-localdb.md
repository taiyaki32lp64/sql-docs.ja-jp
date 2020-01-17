---
title: SQL Server Native Client Support for LocalDB |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a3f5a8214c2966b1958c3a4ea08edbee5af6a2d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225485"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client における LocalDB のサポート
  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降、SQLServer の簡易バージョンである LocalDB を使用できるようになります。 ここでは、LocalDB インスタンス内のデータベースに接続する方法について説明します。  
  
## <a name="remarks"></a>コメント  
 LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、以下を参照してください。  
  
-   [SQL Server Express LocalDB リファレンス](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 要約すると、LocalDB では次の操作を実行できます。  
  
-   `sqllocaldb.exe i` を使用して既定のインスタンスの名前を検出できます。  
  
-   `AttachDBFilename` 接続文字列キーワードを使用して、サーバーをアタッチするデータベース ファイルを指定できます。 使用する場合`AttachDBFilename`でデータベースの名前を指定しない場合は、**データベース**接続文字列キーワードでは、アプリケーションを閉じるときに、LocalDB インスタンスからデータベースが削除されます。  
  
-   接続文字列では、次のように LocalDB インスタンスを指定します。  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 必要に応じて、sqllocaldb.exe を使用して LocalDB インスタンスを作成できます。 また、sqlcmd.exe を使用して、LocalDB インスタンスのデータベースの追加と変更を実行できます。 たとえば、`sqlcmd -S (localdb)\v11.0` のようにします。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)  
  
  
