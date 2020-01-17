---
title: SQL Server Express のセキュリティ
description: SQL Server Express のセキュリティ上の考慮事項を説明します。
ms.date: 09/26/2019
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 9d6b711109f7d94e3bca8d9cf2bda6d2c124c798
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452019"
---
# <a name="sql-server-express-security"></a>SQL Server Express のセキュリティ

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Microsoft SQL Server Express Edition (SQL Server Express) は Microsoft SQL Server をベースとしており、同データベース エンジンの多くの機能をサポートしています。 これは、重要ではない機能とネットワーク接続が既定でオフになるように設計されています。 これにより、悪意のあるユーザーによる攻撃を受ける可能性が低くなります。  
  
SQL Server Express は、通常、名前付きインスタンスとしてインストールされます。 インスタンスの既定の名前は `SQLExpress` です。 名前付きインスタンスは、コンピューターのネットワーク名と、インストール時に指定したインスタンス名によって識別されます。  
  
## <a name="network-access"></a>ネットワーク アクセス  
セキュリティ上の理由により、SQL Server Express では、ネットワーク プロトコルが既定で無効になっています。 これにより、SQL Server Express のインスタンスをホストするコンピューターを危険にさらす可能性がある外部ユーザーからの攻撃を防ぐことができます。 ネットワーク接続を明示的に有効にし、SQL Server Browser サービスを開始して、別のコンピューターから SQL Server Express インスタンスに接続する必要があります。  
  
ネットワーク接続を有効にすると、SQL Server Express インスタンスのセキュリティ要件は、SQL Server の他のエディションと同じになります。  
  
## <a name="user-instances"></a>ユーザー インスタンス  
ユーザーインスタンスは、SQL Server Express の親インスタンスによって生成される SQL Server Express データベースエンジンの個別のインスタンスです。 ユーザーインスタンスの主な目的は、最小特権のユーザーアカウントで Windows を実行しているユーザーが、ローカルコンピューターの SQL Server Express インスタンスに対するシステム管理者 (`sysadmin`) 特権を持つことができるようにすることです。 ユーザーインスタンスは、自分のコンピューターのシステム管理者であるユーザーを対象としていません。  
  
ユーザーインスタンスは、ユーザーに代わって SQL Server または SQL Server Express のプライマリインスタンスから生成されます。 サービスとしてではなく、ユーザーの Windows セキュリティコンテキストでユーザープロセスとして実行されます。 SQL Server ログインは許可されません。Windows ログインのみがサポートされています。 これにより、ユーザーがアクセス許可を持っていないシステム全体の変更が、ユーザーインスタンスで実行されないようにすることができます。 ユーザーインスタンスは子インスタンスまたはクライアントインスタンスとも呼ばれ、RANU 頭字語 ("通常のユーザーとして実行") を使用して参照されることがあります。  
  
各ユーザーインスタンスは、親インスタンスから分離されています。また、同じコンピューター上で実行されている他のユーザーインスタンスから分離されています。 ユーザーインスタンスにインストールされたデータベースは、シングルユーザーモードでのみ開かれます。複数のユーザーがそれらに接続することはできません。 ユーザーインスタンスでは、レプリケーション、分散クエリ、およびリモート接続が無効になっています。 ユーザーインスタンスに接続されている場合、ユーザーには親 SQL Server Express インスタンスに対する特別な権限がありません。  
  
## <a name="external-resources"></a>外部リソース  
SQL Server Express の詳細については、次のリソースを参照してください。  
  
|||  
|-|-|  
|[Microsoft SQL Server 2005 Express Edition オンライン ブック](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|SQL Server 2005 Express Edition の完全なドキュメント。|  
|「[管理者以外のユーザーのためのユーザー インスタンス](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100))」 (SQL Server オンライン ブック)|ユーザーインスタンスを作成して展開する方法について説明します。|  
|[SQL Server Express のユーザー インスタンス](sql-server-express-user-instances.md)|ADO.NET アプリケーションのユーザーインスタンス機能について説明します。 ユーザーインスタンスを有効にする方法、<xref:Microsoft.Data.SqlClient.SqlConnection> を使用してユーザーインスタンスに接続する方法、ユーザーインスタンスの有効期間、およびユーザーインスタンスのシナリオについて説明します。|  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のセキュリティ](sql-server-security.md)
- [SQL Server Express のユーザー インスタンス](sql-server-express-user-instances.md)
