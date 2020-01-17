---
title: レプリケーション スナップショット フォルダーを構成する (既定以外のポート)
titleSuffix: SQL Server on Linux
description: Linux 上の SQL Server レプリケーションに対して、既定以外のポートでスナップショット フォルダーの共有を構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikerayW
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb715e2a0a056c18352361b58ce8ffd67e3da78e
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558597"
---
# <a name="configure-replication-with-non-default-ports-sql-server-linux"></a>既定以外のポートを使用してレプリケーションを構成する (SQL Server Linux)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux インスタンス上で、network.tcpport mssql-conf 設定を使用して構成された任意のポートをリッスンする SQL Server とのレプリケーションを構成できます。 次の条件に該当する場合は、構成時にポートをサーバー名に追加する必要があります。

1. レプリケーションのセットアップに、SQL Server on Linux のインスタンスが含まれる
2. すべてのインスタンス (Windows または Linux) が既定以外のポートをリッスンしている。 

インスタンスのサーバー名は、インスタンス上で @@servername を実行することで見つけることができます。

## <a name="examples"></a>例

'Server1' は、Linux 上でポート 1500 をリッスンします。 ディストリビューション用に 'Server1' を構成するには、`@distributor` を使用して `sp_adddistributor` を実行します。 次に例を示します。 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' は、Linux 上でポート 1500 をリッスンします。 ディストリビューターのパブリッシャーを構成するには、`@publisher` を使用して `sp_adddistpublisher` を実行します。 次に例を示します。

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' は、Linux 上でポート 6549 をリッスンします。 'Server2' をサブスクライバーとして構成するには、`@subscriber` を使用して `sp_addsubscription` を実行します。 次に例を示します。

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' は、Windows 上で、サーバー名 Server3、インスタンス名 MSSQL2017 を使用してポート 6549 をリッスンします。 'Server3' をサブスクライバーとして構成するには、`@subscriber` を使用して `sp_addsubscription` を実行します。 次に例を示します。

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>次のステップ

[概念:Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)

[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

