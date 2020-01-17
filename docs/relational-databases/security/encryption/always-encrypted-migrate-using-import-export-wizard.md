---
title: SQL Server インポートおよびエクスポート ウィザードで Always Encrypted を使用して列間でデータを移行する | Microsoft Docs
ms.custom: ''
ms.date: 10/31/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c8e23b3f5f291d120a099cae7f3e3e057db8da95
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595787"
---
# <a name="migrate-data-to-or-from-columns-using-always-encrypted-with-sql-server-import-and-export-wizard"></a>SQL Server インポートおよびエクスポート ウィザードで Always Encrypted を使用して列間でデータを移行する 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[SQL Server インポートおよびエクスポート ウィザード](../../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)は、ソースから宛先にデータをコピーするためのツールです。 このドキュメントでは、ソースまたは宛先が [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) で保護された列を含む SQL Server データベースである場合に、SQL Server インポートおよびエクスポート ウィザードを使用する方法について説明します。

## <a name="migration-scenarios"></a>移行シナリオ
SQL Server インポートおよびエクスポート ウィザードを使用すると、暗号化された列との間でデータを移行するための次のシナリオを実装できます。

### <a name="encrypt-plaintext-data-on-migration"></a>移行時にプレーンテキスト データを暗号化する
ご利用のデータ ソースにプレーンテキスト データが含まれていて、宛先が暗号化された列を含む SQL Server データベースである場合は、SQL Server インポートおよびエクスポート ウィザードを使用して、ソースからプレーンテキスト データを取得し、それを暗号化し、暗号化されたデータ (暗号化テキスト) を宛先データベース内の暗号化された列にコピーすることができます。 この移行シナリオでは、データ ソースを、SQL Server インポートおよびエクスポート ウィザードでサポートされている任意のデータ ストアとすることができます。 たとえば、ファイル、SQL Server データベース、別のデータベース システム内のデータベース ファイルなどです。

SQL Server インポートおよびエクスポート ウィザードでデータを確実に暗号化できるようにするには、宛先データベース接続に対して Always Encrypted を有効にすると共に、宛先データベース列内のデータを保護するキーへのアクセス権を持っている必要があります。 詳細については、「[データベース接続に対して Always Encrypted を有効または無効にする](#enable-and-disable-always-encrypted-for-a-database-connection)」および「[移行中にデータを暗号化または暗号化解除するためのアクセス許可](#permissions-for-encrypting-or-decrypting-data-during-migration)」を参照してください。

### <a name="decrypt-encrypted-data-on-migration"></a>暗号化されたデータを移行時に暗号化解除する
SQL Server データベース内の暗号化されたデータベース列に格納されているデータを移行する場合は、データの暗号化を解除してから、その暗号化が解除された (プレーンテキスト) データを宛先にコピーするように SQL Server インポートおよびエクスポート ウィザードを構成できます。宛先は、ファイル、SQL Server データベース、または別のデータベース システム内のデータベースなど、SQL Server インポートおよびエクスポート ウィザードでサポートされている任意のデータ ストアとすることができます。

SQL Server インポートおよびエクスポート ウィザードでデータの暗号化の解除を確実に行えるようにするには、ソース データベース接続に対して Always Encrypted を有効にすると共に、宛先データベース列内のデータを保護するキーへのアクセス権を持っている必要があります。 詳細については、「[データベース接続に対して Always Encrypted を有効または無効にする](#enable-and-disable-always-encrypted-for-a-database-connection)」および「[移行中にデータを暗号化または暗号化解除するためのアクセス許可](#permissions-for-encrypting-or-decrypting-data-during-migration)」を参照してください。

### <a name="re-encrypt-data-on-migration"></a>移行時にデータを再暗号化する
ソース SQL Server データベース内の暗号化された列から、同じまたは別の SQL Server データベース内の暗号化された列にデータをコピーする場合は、ソースからデータを取得した後にデータの暗号化を解除し、そしてそのデータを宛先データベース内の暗号化された列に挿入する前に再暗号化するように、SQL Server インポートおよびエクスポート ウィザードを構成することができます。 ターゲット列のスキーマ (たとえば、列のデータ型、暗号化の種類、列の暗号化キー) がソース列のスキーマと異なる場合は、この手法を使用します。

SQL Server インポートおよびエクスポート ウィザードでデータの暗号化と暗号化の解除を確実に行えるようにするには、ソース データベース接続と宛先データベース接続の両方に対して Always Encrypted を有効にすると共に、ソース データベース列内のデータとターゲット データベース列内のデータの両方を保護するキーへのアクセス権を持っている必要があります。 詳細については、「[データベース接続に対して Always Encrypted を有効または無効にする](#enable-and-disable-always-encrypted-for-a-database-connection)」および「[移行中にデータを暗号化または暗号化解除するためのアクセス許可](#permissions-for-encrypting-or-decrypting-data-during-migration)」を参照してください。

### <a name="keep-data-encrypted-during-migration"></a>移行時にデータを暗号化したままにする
ソース SQL Server データベース内の暗号化された列から、同じまたは別の SQL Server データベース内の暗号化された列にデータをコピーするときに、ターゲット列で、ソース列と**厳密に**同じスキーマ (データ型、暗号化の種類、列暗号化キーなど) が使用されている場合は、ソース列から暗号化テキストを取得し、その暗号化されたデータ (暗号化テキスト) をターゲット SQL Server データベース内の暗号化された列に挿入するように、SQL Server インポートおよびエクスポート ウィザードを構成することができます。 

このシナリオでは、SQL Server をサポートする任意のデータ プロバイダーを使用して、ソースまたは宛先の SQL Server データベースに接続できます。 Always Encrypted をサポートするプロバイダーを使用して宛先データベースに接続する場合は、そのデータベース接続に対して Always Encrypted が無効になっていることを確認する必要があります。 詳細については、「[データベース接続に対して Always Encrypted を有効または無効にする](#enable-and-disable-always-encrypted-for-a-database-connection)」を参照してください。

また、SQL Server インポートおよびエクスポート ウィザードが宛先データベースに接続するために使用するデータベース プリンシパル (ユーザー) が、`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS` オプションを `ON` に設定して構成されていることを確認する必要もあります。 このオプションをオンにすると、一括コピー操作時にサーバーに対する暗号化メタデータ チェックが抑制されます。これにより、ウィザードではデータの暗号化を解除せずに暗号化されたデータを宛先データベースに一括挿入することができます。 詳細については、[Always Encrypted によって保護された列への暗号化されたデータの一括読み込み](migrate-sensitive-data-protected-by-always-encrypted.md)に関するページを参照してください。

## <a name="enable-and-disable-always-encrypted-for-a-database-connection"></a>データベース接続に対して Always Encrypted を有効または無効にする
ご利用の移行シナリオにおいて、SQL Server インポートおよびエクスポート ウィザードを使用してデータの暗号化および/または暗号化の解除を行えるようにすることが求められている場合は、Always Encrypted をサポートするデータ プロバイダーを使用して、ソース SQL Server データベース接続および/または宛先 SQL Server データベース接続を構成する必要があります。 また、ソース データベース接続および/または宛先データベース接続に対して Always Encrypted を有効にする必要もあります。

接続上でデータの暗号化または暗号化の解除をウィザードで行う必要がない場合は、その接続に対して任意のデータ プロバイダーを使用することができます。

SQL Server インポートおよびエクスポート ウィザード内の次のデータ プロバイダーでは、Always Encrypted がサポートされています。

- .NET Framework Data Provider for SQL Server
  - ウィザードが実行されているコンピューターで .NET Framework 4.6.1 以降が使用されていることを確認します。
  - 接続に対して Always Encrypted を有効にするには、接続プロパティ内の `Column Encryption Setting` を `Enabled` に設定します。 Always Encrypted を無効にするには、`Column Encryption Setting` を `Disabled` に設定します。 詳細については、「[.NET Framework Data Provider for SQL Server を使用して SQL Server に接続する](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-net-framework-data-provider-for-sql-server)」および「[アプリケーション クエリで Always Encrypted を有効にする](develop-using-always-encrypted-with-net-framework-data-provider.md#enabling-always-encrypted-for-application-queries)」を参照してください。
- .NET Framework Data Provider for ODBC
  - Microsoft ODBC Driver 13.1 以降をインストールします。
    - 接続に対して Always Encrypted を有効にするには、接続プロパティ内の `Column Encryption` を `Enabled` に設定します。 Always Encrypted を無効にするには、`Column Encryption` を `Disabled` に設定します。 詳細については、「[SQL Server 用 ODBC ドライバーを使用して SQL Server に接続する](../../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md#connect-to-sql-server-with-the-odbc-driver-for-sql-server)」および「[ODBC アプリケーションで Always Encrypted を有効にする](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-in-an-odbc-application)」を参照してください。

## <a name="permissions-for-encrypting-or-decrypting-data-during-migration"></a>移行中にデータを暗号化または暗号化解除するためのアクセス許可

SQL Server のソース データベースまたは宛先データベースに格納されたデータを暗号化または暗号化解除するには、ソース データベースで *VIEW ANY COLUMN MASTER KEY DEFINITION* 権限と *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 権限が必要です。

暗号化または暗号化解除するデータを格納する列に対して構成された列マスター キーへのアクセス権も必要です。

- **証明書ストア – ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対する _get_、_unwrapKey_、および _verify_ の権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際に入力を求められる可能性がある必要な権限と資格情報は、ストアと KSP の構成によって異なります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際に入力を求められる可能性がある必要な権限と資格情報は、ストアと CSP の構成によって異なります。
詳細については、 [列マスター キーの作成と格納 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) を参照してください。

## <a name="next-steps"></a>Next Steps
- [SQL Server Management Studio で Always Encrypted を使用した列にクエリを実行する](always-encrypted-query-columns-ssms.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照
- [Always Encrypted](always-encrypted-database-engine.md)
- [Always Encrypted を使用したデータベースのエクスポートとインポート](always-encrypted-migrate-using-bacpac.md)
- [Always Encrypted を使用したデータベースのバックアップと復元](always-encrypted-migrate-using-backup-restore.md)
- [Always Encrypted を使用した暗号化データの列への一括読み込み](migrate-sensitive-data-protected-by-always-encrypted.md)