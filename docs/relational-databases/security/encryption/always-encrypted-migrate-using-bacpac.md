---
title: Always Encrypted を使用したデータベースのエクスポートとインポート | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1f2f44a6cf1172b779160d4ee17e584c7a7b2452
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595807"
---
# <a name="export-and-import-databases-using-always-encrypted"></a>Always Encrypted を使用したデータベースのエクスポートとインポート 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) で保護された列を含むデータベースをエクスポートおよびインポートする方法について説明します。

データベースをエクスポートすると、暗号化された列に格納されているすべてのデータが暗号化された形式 (ciphertext) でデータベースから取得され、結果として生成された [BACPAC](../../data-tier-applications/data-tier-applications.md) に入れられます。 生成された BACPAC には、Always Encrypted キーのメタデータも含まれます。

BACPAC をデータベースにインポートすると、BACPAC からの暗号化されたデータがデータベースに読み込まれ、Always Encrypted キーのメタデータが再び作成されます。 

ソース データベース (エクスポートしたデータベース) に格納されている暗号化された列にクエリを実行するように構成されたアプリケーションがある場合、特別なことをしなくても、そのアプリケーションでターゲット データベース内の暗号化されたデータに対してクエリを実行することができます。これは両方のデータベースのキーが同じであるためです。

データベースのエクスポートおよびインポート方法の詳細については、以下をご覧ください。
- [データ層アプリケーションのエクスポート](../../data-tier-applications/export-a-data-tier-application.md)
- [BACPAC ファイルのインポートによる新しいユーザー データベースの作成](../../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)
- [Azure SQL データベースを BACPAC ファイルにエクスポートする](https://docs.microsoft.com/azure/sql-database/sql-database-export)
- [BACPAC ファイルを Azure SQL Database のデータベースにインポートする](https://docs.microsoft.com/azure/sql-database/sql-database-import)
- [SqlPackage.exe](../../../tools/sqlpackage.md)

## <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>暗号化された列を含むデータベースを移行するためのアクセス許可

ソース データベースに対して *ALTER ANY COLUMN MASTER KEY* および *ALTER ANY COLUMN ENCRYPTION KEY* 権限が必要です。 ターゲット データベースに対して *ALTER ANY COLUMN MASTER KEY*、*ALTER ANY COLUMN ENCRYPTION KEY*、*VIEW ANY COLUMN MASTER KEY DEFINITION*、および *VIEW ANY COLUMN ENCRYPTION* が必要です。

暗号化された列に対して構成されている列マスター キーへのアクセス権は必要ありません。エクスポートおよびインポート操作中にデータが暗号化された状態になるためです。

## <a name="next-steps"></a>Next Steps
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted を使用したデータベースのバックアップと復元](always-encrypted-migrate-using-backup-restore.md)
- [SQL Server インポートおよびエクスポート ウィザードでの Always Encrypted を使用した列間でのデータの移行](always-encrypted-migrate-using-import-export-wizard.md)
- [Always Encrypted を使用した暗号化データの列への一括読み込み](migrate-sensitive-data-protected-by-always-encrypted.md)