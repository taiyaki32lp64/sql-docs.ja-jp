---
title: SQL Server Native Client | を使用した Azure SQL Database への接続Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f154e32b5a7782a083db73de1deef327f44e3ee2
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175407"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client を使用した Azure SQL Database への接続
  Native Client を[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に接続する方法を示すサンプルについ[ては、「開発:操作方法に関するトピック (Azure SQL Database](https://msdn.microsoft.com/library/ee621787.aspx))。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL データベースに接続するときの既知の問題  
 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続する場合、次のような既知の問題があります。  
  
-   各段階で `SQLBrowseConnect` が使用されている場合、`SQLBrowseConnect` との接続が拒否される可能性がある。  たとえば、最初の通話でドライバー名が送信され、サーバーと資格情報 (ユーザー名とパスワード) が 2 番目の通話で送信されて接続が確立し、データベース名と言語が 3 番目の通話で送信されたとします。  3 番目の通話によって、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は USE ステートメントを発行してデータベースを変更します。 しかし、USE ステートメントは [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ではサポートされないため、次のエラーが生成されます。  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client を使用したアプリケーションのビルド](building-applications-with-sql-server-native-client.md)  
  
  
