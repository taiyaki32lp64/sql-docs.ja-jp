---
title: Linux 上の SQL Server レプリケーション
description: この記事では、Linux 上の SQL Server レプリケーションについて説明します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: f0e1acd5af76f5b0b075879fc1c5122713caed55
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2019
ms.locfileid: "75002042"
---
# <a name="sql-server-replication-on-linux"></a>Linux 上の SQL Server レプリケーション

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) 以降では、SQL Server on Linux のインスタンス用の SQL Server レプリケーションがサポートされています。

SQL Server Management Studio (SSMS) の[レプリケーション ストアド プロシージャ](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)を使用して、Linux 上でレプリケーションを構成します。

SQL Server インスタンスは、任意のレプリケーション ロールに参加できます。

* Publisher
* ディストリビューター
* サブスクライバー (Subscriber)

レプリケーション スキーマでは、オペレーティング システムのプラットフォームを混在させて一致させることができます。 たとえば、レプリケーション スキーマにパブリッシャーとディストリビューターの SQL Server on Linux インスタンスを含めることができ、サブスクライバーに Windows 上と Linux 上の SQL Server インスタンスを含めることができます。

Linux 上の SQL Server インスタンスは、任意の種類のレプリケーションに参加できます。

* トランザクション
* スナップショット

レプリケーションの詳細については、[SQL Server レプリケーションのドキュメント](../relational-databases/replication/sql-server-replication.md)を参照してください。

## <a name="supported-features"></a>サポートされている機能

次のレプリケーション機能がサポートされています。

* スナップショット レプリケーション
* トランザクション レプリケーション
* 既定以外のポートを使用するレプリケーション <!--Add link to explanation-->
* AD 認証を使用するレプリケーション
* Windows と Linux 間でのレプリケーションの構成
* トランザクション レプリケーションの即時更新

## <a name="limitations"></a>制限事項

次の機能はサポートされていません。

* マージ レプリケーション
* ピア ツー ピア レプリケーション
* Oracle パブリッシュ

## <a name="next-steps"></a>次のステップ

[Linux 上で SQL Server レプリケーションを構成する](sql-server-linux-replication-tutorial-tsql.md)

[サンプル:Linux 上で SQL Server レプリケーションを構成する](sql-server-linux-replication-configure.md)
