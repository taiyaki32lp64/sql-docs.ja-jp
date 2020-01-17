---
title: Always Encrypted のキー管理の概要 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 07a305b1-4110-42f0-b7aa-28a4e32e912a
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 50411ab35801dea8db00dcea6f6d0109be954a02
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594108"
---
# <a name="overview-of-key-management-for-always-encrypted"></a>Always Encrypted のキー管理の概要
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) は、2 種類の暗号化キーを使用します。1 つはデータを暗号化するキーと、もう 1 つはデータを暗号化するキーを暗号化するキーです。 列暗号化キーはデータを暗号化し、列マスター キーは列暗号化キーを暗号化します。 この記事では、これらの暗号化キーを管理するための詳細な概要を提供します。  

Always Encrypted キーとキーの管理について説明するときは、実際の暗号化キーと、キーを *記述* するメタデータ オブジェクトとの違いを理解することが重要です。 実際の暗号化キーを指す **列暗号化キー** と **列マスター キー** という用語と、データベース内の Always Encrypted キーの **説明** を指す **列暗号化キーのメタデータ** と *列マスター キーのメタデータ* という用語を使用します。

- ***列暗号化キー*** は、データを暗号化するために使用される内容暗号化キーです。 名前が示すように、列暗号化キーはデータベースの列内のデータを暗号化するために使用します。 同じ列暗号化キーで 1 つ以上の列を暗号化することも、ご使用のアプリケーションの要件に応じて複数の列暗号化キーを使用することもできます。 列暗号化キーは自体が暗号化され、列暗号化キーの暗号化された値だけが (列暗号化キーのメタデータの一部として) データベースに格納されます。 列暗号化キーのメタデータは、 [sys.column_encryption_keys (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) と [sys.column_encryption_key_values (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) カタログ ビューに格納されます。 AES-256 アルゴリズムで使用される列暗号化キーは 256 ビット長です。


- ***列マスター キー*** は、列暗号化キーの暗号化に使用される保護キーです。 列マスター キーは、Windows 証明書ストア、Azure Key Vault、またはハードウェア セキュリティ モジュールなどの信頼できるキー ストアに格納する必要があります。 データベースには、列マスター キーに関するメタデータ (キー ストアの種類と場所) のみが含まれます。 列マスター キーのメタデータは、 [sys.column_master_keys (TRANSACT-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md) カタログ ビューに格納されています。  

データベース システム内のキー メタデータには、プレーンテキストの列マスター キーまたはプレーンテキストの列暗号化キーは含まれていないことに注意してください。 データベースには、列マスター キーの種類と場所に関する情報と、列暗号化キーの暗号化された値のみが含まれます。 これは、プレーンテキストのキーはデータベース システムに決して公開されないので、データベース システムが侵害された場合でも、Always Encrypted を使用して保護されているデータの安全性が保証されることを意味します。 データベース システムがプレーンテキストのキーにアクセスできないようにするため、キー管理ツールは、データベースをホストしているコンピューターとは異なるコンピューターで必ず実行します。詳細については、後述の「 [キー管理のセキュリティに関する考慮事項](#security-considerations-for-key-management) 」でご確認ください。

データベースには (Always Encrypted で保護された列内の) 暗号化されたデータだけが含まれ、プレーン テキストのキーにアクセスできないため、データを復号化することはできません。 つまり、Always Encrypted 列に対してクエリを実行しても、暗号化された値が返されるだけなので、保護されたデータを暗号化または復号化する必要があるクライアント アプリケーションは、列マスター キーと関連する列暗号化キーにアクセスできる必要があります。 詳しくは、「[Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)」をご覧ください。



## <a name="key-management-tasks"></a>キー管理タスク

キー管理のプロセスは、次の高度なタスクに分類できます。

- **キーのプロビジョニング** - 信頼できるキー ストア (たとえば、Windows 証明書ストア、Azure Key Vault、またはハードウェア セキュリティ モジュール) に物理キーを作成し、列マスター キーで列暗号化キーを暗号化し、両方の種類のメタデータをデータベースに作成します。

- **キーの交換** -既存のキーを定期的に新しいキーに交換します。 キーが侵害された場合や、暗号化キーを定期的に交換することを定めた組織のポリシーまたはコンプライアンス規定に準拠するために、キーを交換する必要があります。 


## <a name="KeyManagementRoles"></a> キー管理の役割

Always Encrypted キーを管理するユーザーには、セキュリティ管理者とデータベース管理者 (DBA) の 2 つの異なる役割があります。

- **セキュリティ管理者** – 列暗号化キーと列マスター キーを生成し、列マスター キーを含むキー ストアを管理します。 これらのタスクを実行するには、セキュリティ管理者がキーとキー ストアにアクセスできる必要がありますが、データベースへのアクセスは必要ありません。
- **DBA** - データベース内のキーに関するメタデータを管理します。 キー管理タスクを実行するには、DBA がデータベース内のキー メタデータを管理できる必要がありますが、キーまたは列マスター キーを保持しているキー ストアにアクセスする必要はありません。

上記の役割を考慮すると、Always Encrypted のキー管理タスクを実行するには、 *役割の分離を使用する*場合と *役割の分離を使用しない*場合の 2 つの異なる方法があります。 組織のニーズに応じて、要件に最適なキー管理プロセスを選択できます。

## <a name="managing-keys-with-role-separation"></a>役割の分離を使用したキー管理
役割の分離を使用して Always Encrypted キーを管理する場合、組織内の別々の人がセキュリティ管理者の役割と DBA の役割を担当します。 役割の分離を使用したキー管理プロセスには、キーまたは実際のキーを保持するキー ストアへのアクセス権はありません。また、セキュリティ管理者には機密データを含むデータベースへのアクセス権はありません。 組織内の DBA が機密データにアクセスできないようにすることが目的の場合は、役割の分離を使用してキーを管理することをお勧めします。 

**注:** セキュリティ管理者はプレーンテキストのキーを生成して使用するため、データベース システムをホストしているのと同じコンピューター上、または DBA やその他の敵対する可能性のある人物がアクセスできるコンピューター上でタスクを決して実行しないようにする必要があります。 

## <a name="managing-keys-without-role-separation"></a>役割の分離を使用しないキー管理
役割の分離を使用せずに Always Encrypted キーを管理する場合、1 人でセキュリティ管理者の役割と DBA の役割の両方を担当することができます。これは、その人がキー/キー ストアとキーのメタデータの両方にアクセスして管理できる必要があることを意味します。 DevOps モデルを使用している組織、またはデータベースがクラウドでホストされていて、(オンプレミスの DBA ではなく) クラウドの管理者の機密データへのアクセスを制限することが主な目的の場合は、役割の分離を使用せずにキーを管理することをお勧めします。



## <a name="tools-for-managing-always-encrypted-keys"></a>Always Encrypted キーを管理するためのツール

Always Encrypted キーは、 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms174173.aspx) と [PowerShell](../../scripting/sql-server-powershell.md)を使用して管理できます。

- **SQL Server Management Studio (SSMS)** は、キー ストアのアクセスとデータベース のアクセスに関するタスクを組み合わせるダイアログとウィザードを提供しています。そのため、SSMS では役割の分離をサポートしていませんが、キーの構成を容易にします。 SSMS を使用したキー管理の詳細については、以下を参照してください。
    - [SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)
    - [SQL Server Management Studio を使用して Always Encrypted キーを交換する](rotate-always-encrypted-keys-using-ssms.md)

- **SQL Server PowerShell** - 役割の分離を使用または使用せずに Always Encrypted キーを管理するためのコマンドレットが含まれます。 詳細については、以下をご覧ください。
    - [PowerShell を使用して Always Encrypted キーを構成する](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
    - [PowerShell を使用して Always Encrypted キーをローテーションする](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)


## <a name="security-considerations-for-key-management"></a>キー管理でのセキュリティに関する考慮事項

Always Encrypted の主な目的は、データベース システムまたはそのホスティング環境が侵害された場合でも、データベースに格納されている機密データの安全を保証することです。 Always Encrypted が機密データの漏えい防止に役立つ、セキュリティ攻撃の例を次に示します。

- 高い特権を持つ悪意のあるデータベース ユーザー (DBA など)が、機密性の高いデータ列に対してクエリを実行する。
- SQL Server インスタンスをホストするコンピューターの悪意のある管理者が、SQL Server プロセスのメモリ、または SQL Server プロセスのダンプ ファイルをスキャンする。
- 悪意のあるデータ センター オペレーターが、顧客データベースにクエリを実行する、SQL Server のダンプ ファイルを調べる、またはクラウド内の顧客データをホストするコンピューターのメモリを調べる。
- データベースをホストしているコンピューター上でマルウェアが実行されている。

この種の攻撃を防ぐうえで Always Encrypted を効果的にするには、キー管理プロセスで、列マスター キーと列暗号化キー、および列マスター キーを含むキー ストアの資格情報が、潜在的な攻撃者に漏れることがないようにしなければなりません。 従うべきいくつかのガイドラインを以下に示します。

- 列マスター キーまたは暗号化キーをデータベースをホストするコンピューター上で生成しないでください。 代わりに、別のコンピューター (キー管理専用またはキーへのアクセスを必要とするアプリケーションをホストしているコンピューターのいずれか) でキーを生成します。 つまり、攻撃者がプロビジョニングや Always Encrypted キーの維持に使用しているコンピューターにアクセスすると、ツールのメモリにキーが短時間表示されるだけでも、攻撃者がキーを取得できる可能性があるため、**キーを生成するために使用したツールをデータベースをホストしているコンピューター上で決して実行しないでください**。
- キー管理プロセスで誤って列マスター キーや列暗号化キーを公開しないようにするには、キー管理プロセスを定義して実装する前に、潜在的な敵対者およびセキュリティの脅威を識別することが重要です。 たとえば、DBA が機密データにアクセスできないようにすることが目的の場合は、DBA がキーの生成を担当することはできません。 ただし、メタデータにはプレーンテキストのキーは含まれていないため、DBA はデータベース内のキーのメタデータを管理することは *できます* 。

## <a name="next-steps"></a>Next Steps
- [Always Encrypted ウィザードを使用して列暗号化を構成する](always-encrypted-wizard.md)
- [Always Encrypted の列マスター キーを作成して保存する](create-and-store-column-master-keys-always-encrypted.md)
- [SQL Server Management Studio を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md)
- [PowerShell を使用して Always Encrypted キーをプロビジョニングする](configure-always-encrypted-keys-using-powershell.md)

## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted ウィザード チュートリアル (Azure Key Vault)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault/)
- [Always Encrypted ウィザード チュートリアル (Windows 証明書ストア)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)




