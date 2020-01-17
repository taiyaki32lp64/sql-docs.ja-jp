---
title: SQL Server のセキュリティ
description: SQL Server のセキュリティ機能の概要と、SQL Server を対象とした安全な ADO.NET アプリケーションを作成するためのアプリケーション シナリオについて説明します。
ms.date: 09/26/2019
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: bb9e02743122958cb567e01f5011fc9f8b3481e6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452006"
---
# <a name="sql-server-security"></a>SQL Server のセキュリティ

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server には、安全なデータベース アプリケーションの作成を支援するさまざまな機能が備わっています。  
  
データの盗難や破壊など、セキュリティに関する基本的な考慮事項は、使用している SQL Server のバージョンに関係なく当てはまります。 データの整合性は、セキュリティ上の問題と見なす必要もあります。 データが保護されていない場合、アドホックデータ操作が許可されていて、誤って間違った値を使用してデータが誤って、または完全に削除されていると、そのデータが使用できなくなる可能性があります。 また、機密情報を適切に保存するなど、遵守する必要がある法的要件もあります。 特定の管轄区域で適用される法律によっては、一部の種類の個人データを格納することはまったく規定ありません。  
  
SQL Server の各バージョンにはそれぞれ異なるセキュリティ機能があり、Windows と同様、新しいバージョンほど機能が強化されています。 セキュリティ機能だけでは、セキュリティで保護されたデータベースアプリケーションを保証できないことを理解しておくことが重要です。 各データベースアプリケーションは、要件、実行環境、配置モデル、物理的な場所、およびユーザーの作成において一意です。 スコープにローカルなアプリケーションの中には最小限のセキュリティしか必要としないものもありますが、インターネット経由で展開された他のローカルアプリケーションやアプリケーションでは、厳格なセキュリティ対策と継続的な監視と評価が必要になる場合があります。  
  
SQL Server データベース アプリケーションのセキュリティ要件は、事後的対策としてではなく設計時に考慮することが大切です。 開発サイクルの早い段階で脅威を評価することによって、脆弱性が検出された場合に潜在的な損害を軽減することができます。  
  
アプリケーションの初期設計が健全な場合でも、システムの進化に伴って新しい脅威が発生する可能性があります。 データベースに対して複数の防御線を作成することにより、セキュリティ侵害による悪影響を最小限に抑えることができます。 最初の防御策は、絶対に必要な権限よりも多くの権限を付与しないようにすることで、攻撃対象領域を削減することです。  
  
このセクションの各トピックでは、開発者に関係のある SQL Server のセキュリティ機能を簡単に説明します。SQL Server オンライン ブックの関連項目へのリンクのほか、より掘り下げて解説したリソースへのリンクも示しています。  
  
## <a name="in-this-section"></a>このセクションの内容  
[SQL Server での認証](authentication-sql-server.md)  
SQL Server のログインと認証について説明し、その他のリソースへのリンクを示します。 
  
[SQL Server におけるアプリケーション セキュリティのシナリオ](application-security-scenarios-sql-server.md)  
ADO.NET および SQL Server アプリケーションに該当するさまざまなセキュリティ シナリオを取り上げます。  
  
[SQL Server Express のセキュリティ](sql-server-express-security.md)  
SQL Server Express のセキュリティ上の考慮事項を説明します。  
  
## <a name="related-sections"></a>関連項目  
[SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
SQL Server と Azure SQL Database のセキュリティに関する考慮事項について説明します。

[SQL Server インストールにおけるセキュリティの考慮事項](../../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
SQL Server をインストールする前の考慮事項について説明します。

## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
