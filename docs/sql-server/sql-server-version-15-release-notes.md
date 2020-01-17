---
title: SQL Server 2019 リリース ノート | Microsoft Docs
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: f03c9999471f1f196263cfab43960008c7d26aaf
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096113"
---
# <a name="includesql-server-2019includessssqlv15-mdmd-release-notes"></a>[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] リリース ノート
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] の制限事項と既知の問題について説明します。 関連情報については、次を参照してください。

> [[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)

## [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] は、[!INCLUDE[SQL Server 2019](../includes/ssnoversion-md.md)] の最新のパブリック リリースです。

ライセンスの詳細については、インストール メディアの `License Terms` フォルダーをご覧ください。

## <a name="documentation"></a>ドキュメント

- **問題およびユーザーへの影響**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ドキュメントはバージョンによってフィルター処理できます。 各ドキュメント ページの左上にあるコントロールを使用し、要件に応じてフィルター処理してください。

## <a name="build-number"></a>ビルド番号

SQL Server 2019 の RTM ビルド番号は `15.0.2000.5` です。

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>SSMS 18.x がインストールされていると SQL Server のインストールが失敗する場合がある

- **問題およびユーザーへの影響**: 次のインストールをこの順序で実行すると、[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] のインストールが失敗します。
  1. SQL Server Management Studio (SSMS) バージョン 18.0、18.1、18.2、または 18.3 がサーバーにインストールされています。
  1. リムーバブル メディアから [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] のインストールを試みます。 たとえば、DVD などのインストール メディアです。

- **回避策**:
  1. SSMS 18.3.1 より古いバージョンの SSMS をすべてアンインストールします。
  1. 新しいバージョンの SSMS (18.3.1 以降) をインストールします。 最新のバージョンについては、[SSMS のダウンロード](../ssms/download-sql-server-management-studio-ssms.md)に関するページを参照してください。
  1. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] を普通にインストールします。

- **適用対象**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="utf-8-collations"></a>UTF-8 対応の照合順序

- **問題およびユーザーへの影響**:UTF-8 対応の照合順序は、次の機能では使用できません。
  - [インメモリ OLTP テーブル](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)
  - [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) (セキュリティで保護されたエンクレーブを使用しない場合、[Always Encrypted ](../relational-databases/security/encryption/always-encrypted-database-engine.md) では UTF-8 を使用できます)

  > [!WARNING]
  > 使用量が 4,000 バイトを超える [CHAR または VARCHAR](../t-sql/data-types/char-and-varchar-transact-sql.md) と定義されたテーブル列を含むデータベースの [bacpac](../relational-databases/data-tier-applications/data-tier-applications.md#bacpac) の作成は失敗します。
  
  > [!NOTE]
  > Azure Data Studio および SQL Server Data Tools (SSDT) では、UTF-8 対応の照合順序を選択するための UI は現在のところサポートされていません。 最新の [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) バージョン 18 では、UTF-8 対応の照合順序を UI で選択することができます。

- **適用対象**:[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="master-data-service-notification-email-contains-broken-link"></a>マスター データ サービスの通知電子メールに壊れたリンクが含まれる

- **問題およびユーザーへの影響**:マスター データ サービス (MDS) からの通知電子メールには、壊れたリンクが含まれています。 そのリンクでは、次のメッセージのようなエラーが返されるページに移動します。

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **回避策**:MDS ポータルを開き、リソースに手動で移動します。

- **適用対象**:[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RTM

## <a name="see-also"></a>参照

- [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

## <a name="machine-learning-services"></a>Machine Learning Services

SQL Server Machine Learning Services での問題については、「[SQL Server Machine Learning Services の既知の問題](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)」を参照してください。

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]
