---
title: Stretch Database
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: bd061c463afc55ab103646dcd1e0cc5994f43ed1
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844601"
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database は、コールド データを透過的かつ安全に Microsoft Azure クラウドに移行します。  
  
 Stretch Database を今すぐ開始する必要がある場合は、「 [まずはデータベースのストレッチの有効化ウィザードを実行する](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)」を参照してください。  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Stretch Database の利点  
 Stretch Database には次のような利点があります。  
  
 **コールド データでコスト効果の高い可用性を実現**  
 ウォーム トランザクション データとコールド トランザクション データを、SQL Server Stretch Database を使用して、SQL Server から Microsoft Azure に動的にストレッチします。 一般的なコールド データ ストレージとは異なり、データは常にオンラインで、クエリで使用することができます。 また、顧客注文履歴など、大規模テーブルのコストを抑えながら、データ保有期間のタイムラインを長くできます。 高価なオンプレミス ストレージを拡張するのではなく、低コストの Azure をご利用ください。 Azure ポータルでは価格レベルを選択し、設定を構成することで価格とコストを制御し、 必要に応じてスケールアップまたはスケールダウンできます。 詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) 」を参照してください。  
  
 **クエリまたはアプリケーションへの変更が不要**  
 オンプレミスでも、クラウドに拡張されていても、SQL Server データにはシームレスにアクセスできます。  データの格納場所を決定するポリシーはユーザーが設定し、データ移動は SQL Server によってバックグラウンドで処理されます。 テーブル全体が常にオンラインなので、いつでもクエリを実行できるほか、 Stretch Database では既存のクエリまたはアプリケーションに変更を加える必要がありません。データの場所は、アプリケーションに対して完全に透過的になっています。  
  
 **オンプレミスのデータ メンテナンスを効率化**  
 オンプレミスのデータ メンテナンスとストレージの作業が軽減されます。 オンプレミス データのバックアップはさらに迅速になり、メンテナンス期間内に完了します。 データのクラウド部分のバックアップは自動的に行われ、 オンプレミス ストレージのニーズは大幅に減少し、 Azure ストレージのコストは、オンプレミスの SSD を追加した場合のコストよりも 80% 少なくなっています。  
  
 **移行中もデータを保護**  
 移行中も重要なアプリケーションのセキュリティは確保されるため安心です。 SQL Server の Always Encrypted では、移動中のデータが暗号化されます。 行レベルのセキュリティ (RLS) などの高度な SQL Server セキュリティ機能も Stretch Database で動作し、データを保護します。  
  
## <a name="what-does-stretch-database-do"></a>Stretch Database の機能  
 SQL Server インスタンスおよびデータベースに対して Stretch Database を有効にして、1 つ以上のテーブルを選択すると、Stretch Database からコールド データの Azure への移行が確認メッセージなしで開始されます。  
  
-   コールド データを別のテーブルに保存している場合は、そのテーブル全体を移行できます。  
  
-   テーブルにホット データとコールド データの両方が含まれている場合は、移行する行を選択するフィルター関数を指定できます。

**既存のクエリとクライアント アプリを変更する必要はありません。** データの移行中でも、ローカル データとリモート データの両方に引き続きシームレスにアクセスできます。 リモート クエリについては多少の待機時間がありますが、この待機時間が発生するのは、コールド データのクエリを実行するときに限られます。

移行中にエラーが発生しても、**Stretch Database により、データが失われることがなくなります。** また、この Stretch Database には、移行中に発生する可能性のある接続の問題に対処する再試行ロジックも用意されています。 移行の状態は動的管理ビューに表示されます。

**データの移行を一時停止して** 、ローカル サーバーで発生した問題をトラブルシューティングしたり、使用可能なネットワーク帯域幅を最大化したりできます。  
  
 ![Stretch Database の概要](../../sql-server/stretch-database/media/stretch-overview.png "Stretch Database の概要")  
  
## <a name="is-stretch-database-for-you"></a>Stretch Database を使用する状況  
 次に当てはまる場合は、Stretch Database がニーズへの対応と問題解決に役立つ可能性があります。  
  
|意思決定者の場合|DBA の場合|  
|--------------------------------|---------------------|  
|長期にわたってトランザクション データを保持しなければならない。|テーブルのサイズを制御しきれない。|  
|コールド データにクエリを実行することがある。|コールド データにアクセスしたいが、めったに使用することはない、とユーザーが言っている。|  
|更新したくないアプリ (古いアプリを含む) がある。|ストレージを購入および追加し続けなければならない。|  
|ストレージのコストを節約する方法を見つけたい。|SLA 内でこのような大きなテーブルをバックアップまたは復元できない。|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>Stretch Database の候補となるデータベースとテーブル  
 Stretch Database は、通常は少数のテーブルに格納されている、大きなサイズのコールド データが含まれるトランザクション データベースを対象としています。 これらのテーブルには、10 億を超える行が含まれている場合があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のテンポラル テーブル機能を使用する場合は、Stretch Database を使用して、関連付けられている履歴テーブル全体または一部を、Azure のコスト効果の高いストレージに移行します。 詳細については、「 [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)」を参照してください。  
  
 Stretch Database 用のデータベースとテーブルを特定するには、SQL Server 2016 Upgrade Advisor の機能、Stretch Database Advisor を使用してください。 詳細については、「 [Stretch Database Advisor を実行して Stretch Database のデータベースとテーブルを特定する](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)」をご覧ください。 潜在的なブロッキングの問題の詳細については、「 [Stretch Database の制限事項](../../sql-server/stretch-database/limitations-for-stretch-database.md)」を参照してください。  

## <a name="test-drive-stretch-database"></a>Stretch Database の試用  
 **AdventureWorks サンプル データベースでの Stretch Database の試用。** AdventureWorks サンプル データベースを入手するには、 [こちら](https://www.microsoft.com/download/details.aspx?id=49502)から最小限のデータベース ファイルとサンプルおよびスクリプト ファイルをダウンロードしてください。 SQL Server 2016 のインスタンスにサンプル データベースを復元したら、サンプル ファイルを解凍し、Stretch DB フォルダーから Stretch DB サンプルのファイルを開きます。 このファイルのスクリプトを実行し、Stretch Database を有効にする前と後にデータで使用する領域を確認したり、データ移行の進行状況を追跡したり、引き続き既存のデータにクエリを実行し、データの移行中と移行後の両方で新しいデータを挿入できることを確認します。  
  
## <a name="next-step"></a>次の手順  
 **Stretch Database の候補となるデータベースとテーブルを特定する。** SQL Server 2016 Upgrade Advisor をダウンロードし、Stretch Database Advisor を実行して、Stretch Database の候補となるデータベースとテーブルを特定します。 Stretch Database Advisor はブロックの問題も特定します。 詳細については、「 [Stretch Database Advisor を実行して Stretch Database のデータベースとテーブルを特定する](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)」をご覧ください。  
  
  
