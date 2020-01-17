---
title: 'トランザクション: 可用性グループとデータベース ミラーリング'
descripton: Learn about cross-database and distributed transaction support for SQL Server Always On availability groups and database mirroring.
ms.custom: seo-lt-2019
ms.date: 12/11/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 407e477be98f386adc27fc965b1d099d1dec4dfa
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251231"
---
# <a name="transactions---availability-groups-and-database-mirroring"></a>トランザクション - 可用性グループとデータベース ミラーリング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクションのサポートについて説明します。  

## <a name="support-for-distributed-transactions"></a>分散トランザクションのサポート

SQL Server 2017 では、可用性グループのデータベースに対して分散トランザクションがサポートされています。 このサポートには、SQL Server の同じインスタンス上のデータベース、または SQL Server の異なるインスタンス上のデータベースが含まれています。 分散トランザクションは、データベース ミラーリング用に構成されたデータベースではサポートされていません。

> [!NOTE]
> [!INCLUDE[SQL Server 2016](../../../includes/sssql15-md.md)] Service Pack 2 以降では、可用性グループでの分散トランザクションが完全にサポートされます。 
> 
> [!INCLUDE[SQL Server 2016](../../../includes/sssql15-md.md)] Service Pack 2 より前のバージョンでは、可用性グループ内のデータベースに関連する複数データベースにまたがる分散トランザクション (つまり、同じ SQL Server インスタンスのデータベースを使用するトランザクション) はサポートされません。

分散トランザクション対応の可用性グループの構成については、「[Configure Availability Group for Distributed Transactions](configure-availability-group-for-distributed-transactions.md)」 (分散トランザクション対応の可用性グループを構成する)」を参照してください。

詳細については、次を参照してください。

- [DTC 管理ガイド](https://msdn.microsoft.com/library/ms681291.aspx)
- [DTC 開発者ガイド](https://msdn.microsoft.com/library/ms679938.aspx)
- [DTC プログラマ リファレンス](https://msdn.microsoft.com/library/ms686108.aspx)

## <a name="sql-server-2016-sp1-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 SP1 以前:同じ SQL Server インスタンス内での複数データベースにまたがるトランザクションのサポート  

SQL Server 2016 SP1 以前では、可用性グループに対して、同じ SQL Server インスタンス内での複数データベースにまたがるトランザクションはサポートされていません。 いずれかまたは両方のデータベースが可用性グループにある場合は、同じ SQL Server インスタンスで複数データベースにまたがるトランザクションの 2 つのデータベースをホストできない可能性があります。 この制限は、これらのデータベースが同じ可用性グループの一部である場合でも適用されます。  
  
複数のデータベースにまたがるトランザクションは、データベース ミラーリングでもサポートされていません。  
  
##  <a name="dtcsupport"></a> SQL Server 2016 SP1 以前:分散トランザクションのサポート  
複数のデータベースがそれぞれ異なる SQL Server インスタンスでホストされている場合は、可用性グループで分散トランザクションがサポートされます。 これは、SQL Server インスタンスと DTC に準拠した別のサーバー間の分散トランザクションにも当てはまります。  
 
Microsoft 分散トランザクション コーディネーター (MSDTC または DTC) は、分散システムのトランザクション インフラストラクチャを提供する Windows サービスです。 MSDTC では、クライアント アプリケーションに対して、1 つのトランザクションに複数のデータ ソースを含め、その後、トランザクションに含まれるすべてのサーバーにコミットすることを許可します。 たとえば、MSDTC を使用して、さまざまなサーバーの複数のデータベースにわたるトランザクションを調整することができます。

SQL Server 2016 では、トランザクションの 1 つ以上のデータベースが可用性グループに含まれる場合、分散トランザクションを使用する機能を導入します。 SQL Server 2016 より前の分散トランザクションでは、可用性グループのデータベースはサポートされていませんでした。 SQL Server 2016 では、データベースごとにリソース マネージャーを登録できます。 この新機能を使用すると、分散トランザクションでデータベースを可用性グループに含めることができます。
  
 次の要件が満たされる必要があります。  
  
-   可用性グループは、Windows Server 2012 R2 以降で実行されている必要があります。 Windows Server 2012 R2 の場合は、[https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973) で入手できる KB3090973 の更新プログラムをインストールする必要があります。  
  
-   可用性グループは、**CREATE AVAILABILITY GROUP** コマンドと **WITH DTC\_SUPPORT = PER_DB** 句を使って作成する必要があります。 現在、既存の可用性グループを変更することはできません。  

- 可用性グループに参加するすべての SQL Server インスタンスは、SQL Server 2016 以降である必要があります。
 
 ## <a name="non-support-for-distributed-transactions"></a>分散トランザクションの非サポート
 次の場合、分散トランザクションはサポートされません。
 
 - SQL Server 2016 SP1 以前で、トランザクションに関係する複数のデータベースが同じ可用性グループに含まれる場合。
 
 - SQL Server 2016 SP1 以前で、少なくとも 1 つのデータベースが可用性グループにあり、別のデータベースが同じ SQL Server インスタンスにある場合。 
 
 - 分散トランザクションを有効にして可用性グループが作成されなかった場合。
 
 - データベース ミラーリング
 
 > [!IMPORTANT]
 > ご利用の環境で DTC が解決できないトランザクションの適切な既定の結果を判断します。  既定の結果の構成方法については、「 [in-doubt xact resolution サーバー構成オプション](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md)」を参照してください。
  
## <a name="example-scenario-with-database-mirroring"></a>データベース ミラーリングのサンプル シナリオ  
 次に示すデータベース ミラーリングの例では、論理的な不一致が発生するしくみについて説明します。 この例では、アプリケーションは複数データベースにまたがるトランザクションを使用して 2 行のデータを挿入します。一方の行は、ミラー化されたデータベース A 内のテーブルに挿入され、もう一方の行は、別のデータベース B 内のテーブルに挿入されます。データベース A は、自動フェールオーバーを伴う高い安全性モードでミラー化されています。 トランザクションがコミットされている間、データベース A は使用できなくなり、ミラーリング セッションはデータベース A のミラーに自動的にフェールオーバーされます。  
  
 フェールオーバー後、複数データベースにまたがるトランザクションは、データベース B では正常にコミットされますが、フェールオーバーされたデータベースではコミットされない場合があります。 たとえば、障害発生前に、複数データベースにまたがるトランザクションのログがデータベース A の元のプリンシパル サーバーからミラー サーバーに送信されなかった場合です。 フェールオーバー後、そのトランザクションは新しいプリンシパル サーバーに存在しなくなります。 データベース B に挿入されたデータはそのまま保たれますが、データベース A に挿入されたデータは失われているため、データベース A と B は一致しなくなります。  
  
 同様の状況は、MS DTC トランザクションを使用する際に発生する場合があります。 たとえば、フェールオーバー後、新しいプリンシパルが MS DTC にアクセスします。 ただし、MS DTC は、新しいプリンシパル サーバーを認識せず、"コミットの準備が整った" トランザクションを終了します。これらのトランザクションは、他のデータベースでコミットされていると見なされます。  
  
> [!NOTE]  
>  この記事で承認されていない DTC とデータベース ミラーリングの使用や DTC と可用性グループの使用はサポートされていません。  これは、DTC に関係しない部分はサポートされないことを意味するものではありません。ただし、分散トランザクションの不適切な使用により発生する問題はサポートされません。  
  
## <a name="next-steps"></a>次のステップ  
 [Always On 可用性グループ:相互運用性 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  
