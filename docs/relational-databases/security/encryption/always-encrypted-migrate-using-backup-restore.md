---
title: Always Encrypted を使用したデータベースのバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9176052b413293d25acd7696701e4f118adba03f
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595727"
---
# <a name="backup-and-restore-databases-using-always-encrypted"></a>Always Encrypted を使用したデータベースのバックアップと復元 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) で保護された列を含むデータベースをバックアップおよび復元する方法について説明します。

データベースをバックアップすると、生成されるバックアップ ファイルには、Always Encrypted キーの暗号化された列に格納されている暗号化データとすべてのメタデータが含まれます。

データベースを復元するとき、Always Encrypted のすべての暗号化データとすべてのメタデータが復元されます。 

データベースを別のサーバー上で、または別の名前で復元した場合は、両方のデータベースのキーが同じであるため、ターゲット データベースの暗号化されたデータをアプリケーションでクエリできるようにするための特別な操作は必要ありません。

データベースのバックアップと復元を行う方法の詳細については、以下を参照してください。
- [バックアップの概要 (SQL Server)](../../backup-restore/backup-overview-sql-server.md)
- [データベースをマネージド インスタンスに復元する](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started-restore)

## <a name="next-steps"></a>Next Steps
- [SQL Server Management Studio で Always Encrypted を使用した列にクエリを実行する](always-encrypted-query-columns-ssms.md)
- [セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するアプリケーションの開発](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted を使用したデータベースのエクスポートとインポート](always-encrypted-migrate-using-bacpac.md)
- [SQL Server インポートおよびエクスポート ウィザードでの Always Encrypted を使用した列間でのデータの移行](always-encrypted-migrate-using-import-export-wizard.md)
- [Always Encrypted を使用した暗号化データの列への一括読み込み](migrate-sensitive-data-protected-by-always-encrypted.md)
