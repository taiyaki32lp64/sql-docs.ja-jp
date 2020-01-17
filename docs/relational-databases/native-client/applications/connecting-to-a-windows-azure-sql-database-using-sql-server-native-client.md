---
title: Native Client、Azure SQL DB への接続
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67185f91fa89e84a8733299409b19b2a191fe9bf
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244213"
---
# <a name="connecting-to-an-azure-sql-database-using-sql-server-native-client"></a>SQL Server Native Client を使用した Azure SQL データベースへの接続
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Native Client を[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]使用して[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に接続する方法を示すサンプルについては、「[開発: 操作方法に関するトピック (Azure SQL Database)](https://msdn.microsoft.com/library/ee621787.aspx)」を参照してください。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>SQL データベースに接続するときの既知の問題  
 
  [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続する場合、次のような既知の問題があります。  
  
-   **SQLBrowseConnect**がステージで使用されている場合、 **SQLBrowseConnect**を使用した接続は拒否されることがあります。  たとえば、最初の通話でドライバー名が送信され、サーバーと資格情報 (ユーザー名とパスワード) が 2 番目の通話で送信されて接続が確立し、データベース名と言語が 3 番目の通話で送信されたとします。  3 番目の通話によって、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は USE ステートメントを発行してデータベースを変更します。 しかし、USE ステートメントは [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ではサポートされないため、次のエラーが生成されます。  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client を使用したアプリケーションの構築](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
