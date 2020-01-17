---
title: SQL Server 2019 on Linux の新機能
description: この記事では、SQL Server 2019 on Linux の新機能について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: bb56808dd81890df4f45636b600aaf3269c374f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72890561"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux の新機能

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上で実行される SQL Server 2019 で使用できる主な機能とサービスについて説明します。 パッケージのダウンロードと既知の問題については、[リリース ノート](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15)のページをご覧ください。

## <a name="updates"></a>Updates

SQL Server 2019 on Linux では、次の更新が行われています。

| 新機能または更新 | 詳細 |
|:-----|:-----|
|レプリケーションのサポート |[Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)
|Microsoft 分散トランザクション コーディネーター (MSDTC) のサポート |[Linux で MSDTC を構成する方法](sql-server-linux-configure-msdtc.md) |
|サード パーティの AD プロバイダーに対する OpenLDAP のサポート |[チュートリアル: SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md) |
|Linux 上の Machine Learning |[Linux に Machine Learning を構成する](sql-server-linux-setup-machine-learning.md) |
|`tempdb` の強化機能 | 既定では、Linux 上に SQL Server を新しくインストールすると、論理コアの数に基づいて複数の `tempdb` データ ファイルが作成されます (最大で 8 個のデータ ファイル)。 これは、マイナー バージョンまたはメジャー バージョンのインプレース アップグレードには適用されません。 各 `tempdb` ファイルは 8 MB で、64 MB まで自動拡張されます。 この動作は、Windows への SQL Server の既定のインストールに似ています。 |
| Linux での PolyBase | 非 Hadoop コネクタ向けに Linux に [PolyBase をインストール](../relational-databases/polybase/polybase-linux-setup.md)します。<br/><br/>[PolyBase 型のマッピング](../relational-databases/polybase/polybase-type-mapping.md) |
| 変更データ キャプチャ (CDC) のサポート | SQL Server 2019 では、変更データ キャプチャ (CDC) が Linux でサポートされるようになりました。 |
| Microsoft Container Registry | [Microsoft Container Registry](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/) では、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] など、Microsoft の新しい公式コンテナー イメージのために Docker Hub が取り替えられます。 |
| ルート以外のコンテナー | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、既定でルート以外のユーザーとして [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] を起動することで、より安全なコンテナーを作成できるようになりました。 詳細については、「[非ルート ユーザーとして SQL Server コンテナーを作成して実行する](sql-server-linux-configure-docker.md#buildnonrootcontainer)」を参照してください。 |

## <a name="next-steps"></a>次の手順

SQL Server on Linux をインストールするには、次のチュートリアルのいずれかを使用します。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Docker 上での実行](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。 SQL Server 2019 で導入されたその他の改善点については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)に関する記事をご覧ください。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
