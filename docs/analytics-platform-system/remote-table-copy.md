---
title: リモート テーブルのコピー
description: Analytics Platform System Parallel Data Warehouse でのリモートテーブルコピーの使用。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ecbbdced731e940de46dbde4a65adc486f602c2f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400480"
---
# <a name="remote-table-copy"></a>リモートテーブルのコピー
リモートテーブルのコピー機能を使用して、SQL Server PDW データベースからリモート (アプライアンス以外) の SMP SQL Server データベースにテーブルをコピーする方法について説明します。 リモートテーブルのコピーを使用して、SQL Server PDW のハブアンドスポークシナリオを有効にします。  
  
## <a name="BasicsPDE"></a>SQL Server PDW のリモートテーブルのコピーについて  
リモートテーブルコピーは SQL Server PDW の機能です。この機能を使用すると、SQL SELECT ステートメントの結果を SMP データベースのテーブルにコピーすることによって、ハブとスポークのシナリオを有効にすることができます。 リモートテーブルのコピーは、 [CREATE REMOTE table AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md)ステートメントを使用して開始されます。  
  
## <a name="BasicsPrerequisites"></a>リモートテーブルのコピーを使用するための要件  
リモートテーブルコピーを使用すると、これらの条件が満たされた場合に SQL Server PDW から SQL Server データベースにテーブルをコピーできます。  
  
-   転送先データベースは、microsoft® SQL Server®のインスタンスである必要があります。このインスタンスは、SQL Server PDW アプライアンスに接続できるが、アプライアンス内のサーバー上には存在しない Microsoft Windows®システム上で実行されています。 リモート SQL Server は、InfiniBand ネットワークまたはイーサネットネットワークを使用して SQL Server PDW に接続できます。  
  
-   コピーされるデータは、1つの有効な SQL Server PDW [select](../t-sql/queries/select-transact-sql.md)ステートメントを使用して選択できる必要があります。  
  
-   転送先サーバーは、非アプライアンス サーバーである必要があります。 このトピックの手順に従って、データを1つのアプライアンスから別のアプライアンスに直接コピーすることはできません。  
  
-   移行先サーバーには、アプライアンスの Infiniband ネットワーク上のすべてのノードからアクセスできる必要があります。  
  
## <a name="ConfigureRemote"></a>リモートテーブルのコピーの構成  
リモートテーブルのコピーを使用するには、Windows server を購入して構成し、Windows server で SQL Server を構成して、SQL Server PDW を構成する必要があります。 これら3つの構成手順を実行するには、次のリンクを使用します。  
  
1.  [InfiniBand を使用してリモートテーブルコピーを受信するように外部 Windows システムを構成する](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md)  
  
2.  [リモートテーブルコピーを受信するための外部 SMP SQL Server の構成](configure-an-external-smp-sql-server-to-receive-remote-table-copies.md)  
  
3.  [リモートテーブルコピーの SQL Server PDW を構成する](configure-sql-server-pdw-for-remote-table-copies.md)  
  
## <a name="PerformRemote"></a>リモートテーブルのコピーを実行する  
リモートテーブルのコピーを実行するには、 [CREATE REMOTE TABLE AS SELECT](../t-sql/statements/create-remote-table-as-select-parallel-data-warehouse.md) SQL ステートメントを使用します。 例は、リモートテーブルの作成に関するトピックに含まれています。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
