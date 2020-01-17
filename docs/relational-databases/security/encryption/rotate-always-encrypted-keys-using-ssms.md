---
title: SQL Server Management Studio を使用した Always Encrypted キーの交換 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
- sql13.SWB.COLUMNMASTERKEY.CLEANUP.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5d0a96f061f01749194cd3f0d1be1aae5443ff8a
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595707"
---
# <a name="rotate-always-encrypted-keys-using-sql-server-management-studio"></a>SQL Server Management Studio を使用して Always Encrypted キーを交換する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

この記事では、[SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md) を使用して、Always Encrypted の列マスター キーと列暗号化キーを交換するためのタスクについて説明します。

推奨されるベスト プラクティスやセキュリティ上の重要な考慮事項など、Always Encrypted のキー管理の概要については、「[Always Encrypted のキー管理の概要](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)」をご覧ください。

<a name="rotatecmk"></a>
## <a name="rotate-column-master-keys"></a>列マスター キーの交換 

列マスター キーの回転は、既存の列マスター キーを新しい列マスター キーに置き換える処理です。 キーの回転は、キーが侵害されている場合に、または必須の暗号化キーを定期的に回転することを求めた組織のポリシーまたはコンプライアンス規定に準拠するために、行うことが必要な場合があります。 列マスター キーの回転では、現在の列マスター キーで保護された列暗号化キーを暗号化解除し、新しい列マスター キーを使用して列暗号化キーを再度暗号化し、キーのメタデータを更新するという処理が必要です。 

### <a name="step-1-provision-a-new-column-master-key"></a>手順 1:新しい列マスター キーをプロビジョニングする

「[[新しい列マスター キー] ダイアログを使用して列マスター キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)」に記載されている手順に従ってください。

### <a name="step-2-encrypt-column-encryption-keys-with-the-new-column-master-key"></a>手順 2:新しい列マスター キーで列暗号化キーを暗号化する

列マスター キーは、通常、1 つまたは複数の列暗号化キーを保護します。 列暗号化キーを列マスター キーにより暗号化すると、各列暗号化キーの暗号化された値がデータベースに格納されます。
この手順では、回転する列マスター キーで保護されている各列暗号化キーを新しい列マスター キーで暗号化し、新しい暗号化された値をデータベースに格納します。 結果的に、回転の影響を受けた各列暗号化キーには暗号化された値が 2 つ含まれることになります。1 つは既存の列マスター キーにより暗号化された値、もう 1 つは新しい列マスター キーで暗号化された値です。

1.  **オブジェクト エクスプローラー**で **[セキュリティ] > [Always Encrypted キー] > [列マスター キー]** フォルダーの順に移動し、回転する列マスター キーを探します。
2.  列マスター キーを右クリックし、 **[回転]** を選択します。
3.  **[列マスター キーの回転]** ダイアログの **[ターゲット]** フィールドで、手順 1 で作成した、新しい列マスター キーの名前を選択します。
4.  既存の列マスター キーで保護された、列暗号化キーの一覧を確認します。 これらのキーは、回転の影響を受けます。
5.  **[OK]** をクリックします。

SQL Server Management Studio では、古い列マスター キーで保護された列暗号化キーのメタデータと、古い列マスター キーおよび新しい列マスター キーのメタデータを取得します。 次に、SSMS では、列マスター キーのメタデータを使用することで、古い列マスター キーが格納されたキー ストアにアクセスし、列暗号化キーを暗号化解除します。 さらに、SSMS では、新しい列マスター キーを保持しているキー ストアにアクセスして、列暗号化キーの暗号化された値セットを新たに作成し、その新しい値をメタデータに追加します ( [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) ステートメントの生成および発行)。

> [!NOTE]
> 古い列マスター キーで暗号化されたそれぞれの列暗号化キーが他の列マスター キーで暗号化されていないことを確認します。 つまり、回転の影響を受けるすべての列暗号化キーに、データベースの暗号化された値が 1 つだけ含まれている必要があります。 影響を受ける列暗号化キーのいずれかに複数の暗号化された値が含まれている場合、回転を続行する前にその値を削除する必要があります (列暗号化キーの暗号化された値を削除する方法は、 *"手順 4"* を参照してください)。

### <a name="step-3-configure-your-applications-with-the-new-column-master-key"></a>手順 3:新しい列マスター キーでアプリケーションを構成する

この手順では、回転している列マスター キーで保護されたデータベース列 (つまり、回転されている列マスター キーで暗号化される列暗号化キーで暗号化されたデータベース列) に対してクエリを実行するすべてのクライアント アプリケーションが、新しい列マスター キーにアクセスできるようにする必要があります。 この手順は、新しい列マスター キーが格納されているキー ストアの種類によって異なります。 例:

- 新しい列マスター キーが Windows 証明書ストアに格納された証明書である場合、データベースの列マスター キーのキー パスに指定された場所と同じ証明書ストアの場所 ( *[現在のユーザー]* または *[ローカル コンピューター]* ) に証明書を展開する必要があります。 アプリケーションが、証明書にアクセスできる必要があります。
  - 証明書が、"*現在のユーザー*" の証明書ストアに格納されている場合、証明書をアプリケーションの Windows ID (ユーザー) の [現在のユーザー] ストアにインポートする必要があります。
  - 証明書が "*ローカル コンピューター*" の証明書ストアに格納されている場合、アプリケーションの Windows ID に証明書へのアクセス許可が必要です。
- 新しい列マスター キーが Microsoft Azure Key Vault に格納されている場合は、アプリケーションが Azure を認証でき、キーにアクセスできるように実装する必要があります。

詳細については、「[Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

> [!NOTE]
> 回転のこの時点では、古い列マスター キーと新しい列マスター キーの両方が有効であり、これらを使ってデータにアクセスすることができます。

### <a name="step-4-clean-up-column-encryption-key-values-encrypted-with-the-old-column-master-key"></a>手順 4:古い列マスター キーで暗号化された列暗号化キーの値をクリーンアップする

新しい列マスター キーを使用するようにすべてのアプリケーションを構成したら、 *"古い"* 列マスター キーで暗号化された列暗号化キーの値をデータベースから削除します。新しい列マスター キーを使用するようにすべてのアプリケーションを構成したら、古い列マスター キーで暗号化された列暗号化キーの値をデータベースから削除します。 古い値を削除することで、次の回転を行うことができます (ただし、回転される列マスター キーで保護されたすべての列暗号化キーに、必ず暗号化された値が 1 つ必要です)。

古い列マスター キーをアーカイブまたは削除する前に古い値をクリーンアップするもう 1 つの理由は、パフォーマンスに関係します。暗号化された列にクエリを実行すると、Always Encrypted が有効なクライアント ドライバーで、古い値と新しい値の 2 つの暗号化を解除しなければならない場合があるからです。 ドライバーでは、アプリケーションの環境で 2 つの列マスター キーのどちらが有効かは認識されません。このため、ドライバーでは暗号化された値が両方ともサーバーから取得されます。 使用できない列マスター キー (ストアから削除されている古い列マスター キーなど) で暗号化されていることにより一方の値の暗号化の解除が失敗すると、ドライバーでは新しい列マスター キーを使用してもう一方の値の暗号化の解除が試みられます。

> [!WARNING]
> 対応する列マスター キーがアプリケーションで使用できるようになる前に列暗号化キーの値を削除すると、データベース列をアプリケーションが暗号化解除できなくなります。

1.  **オブジェクト エクスプローラー**で、 **[セキュリティ]、[Always Encrypted キー]** フォルダーの順に移動し、交換する既存の列マスター キーを探します。
2.  既存の列マスター キーを右クリックし、 **[クリーンアップ]** を選択します。
3.  削除される列暗号化キーの値の一覧を確認します。
4.  **[OK]** をクリックします。

SQL Server Management Studio では、 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) ステートメントを発行して、古い列マスター キーで暗号化された列暗号化キーの暗号化された値を削除します。

### <a name="step-5-delete-metadata-for-your-old-column-master-key"></a>手順 5:古い列マスター キーのメタデータを削除する

データベースから古い列マスター キーの定義を削除する場合は、次の手順を使用します。

1. **オブジェクト エクスプローラー**で **[セキュリティ]、[Always Encrypted キー]、[列マスター キー]** フォルダーの順に移動し、データベースから削除する古い列マスター キーを探します。
2. 古い列マスター キーを右クリックし、 **[削除]** を選択します ( [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) ステートメントが生成および発行され、列マスター キーのメタデータが削除されます)。
3. **[OK]** をクリックします。

> [!NOTE]
> 回転の後、古い列マスター キーは完全に削除しないを強くお勧めします。 そこで、古い列マスター キーを現在のキー ストアに保存するか、セキュリティで保護された別の場所にアーカイブします。 バックアップ ファイルからデータベースを復元して、新しい列マスター キーを構成する前の時点まで戻る場合は、古いキーでデータにアクセスする必要があります。

### <a name="permissions-for-rotating-column-master-key"></a>列マスター キーを回転するためのアクセス許可

列マスター キーを回転するには、次のデータベース権限が必要です。

- **ALTER ANY COLUMN MASTER KEY** - 新しい列マスター キーのメタデータを作成し、古い列マスター キーのメタデータを削除するのに必要です。
- **ALTER ANY COLUMN ENCRYPTION KEY** - 列暗号化キーのメタデータを変更するのに必要です (新しい暗号化された値の追加)。

また、キー ストアにある古い列マスター キーと新しい列マスター キーの両方にアクセスできることも必要です。 キー ストアにアクセスして、列マスター キーを使用するには、キー ストアとキーの両方、またはそのいずれかに対する権限が必要な場合があります。
- **証明書ストア – ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対する *create*、*get*、*unwrapKey*、*wrapKey*、*sign*、および *verify* 権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

詳細については、「[Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

<a name="rotatecek"></a> 
## <a name="rotate-column-encryption-keys"></a>列暗号化キーの交換

列暗号化キーを回転するには、回転するキーで暗号化されたすべての列のデータを暗号化解除し、新しい列暗号化キーを使用してデータを再度暗号化する必要があります。

>[!NOTE]
> 回転するキーで暗号化された列を含むテーブルが大きい場合、列暗号化キーの回転には長い時間がかかることがあります。 データが再暗号化されている間、アプリケーションは影響を受けるテーブルへの書き込みを行うことができません。 したがって、組織で列暗号化キーを回転する場合は、慎重に計画を立てる必要があります。
列暗号化キーを回転するには、Always Encrypted ウィザードを使用します。

1.  データベースのウィザードを開きます。それには、データベースを右クリックして **[タスク]** をポイントし、 **[列の暗号化]** をクリックします。
2.  **[概要]** ページの内容を確認し、 **[次へ]** をクリックします。
3.  **[列の選択]** ページで、テーブルを展開し、古い列暗号化キーで現在暗号化されている列で、置換する列をすべて特定します。
4.  古い列暗号化キーで暗号化されたそれぞれの列について、 **[暗号化キー]** を新しい自動生成キーに設定します。 **注:** または、ウィザードを実行する前に、新しい列暗号化キーを作成しておくこともできます (「[[新しい列の暗号化キー] ダイアログを使用して列の暗号化キーをプロビジョニングする](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)」を参照)。
5.  **[マスター キーの構成]** ページで、新しいキーを格納する場所を選択し、マスター キー ソースを選択し、 **[次へ]** をクリックします。 **注:** 既存の列暗号化キーを使用する (自動生成されたものではなく) 場合、このページで実行するアクションはありません。
6.  **[検証]** ページで、スクリプトをすぐに実行するか PowerShell スクリプトを作成するかを選択し、 **[次へ]** をクリックします。
7.  **[概要]** ページで、選択したオプションを確認し、完了したら **[完了]** をクリックしてウィザードを閉じます。
8.  **オブジェクト エクスプローラー**で **[セキュリティ]、[Always Encrypted キー]、[列暗号化キー]** フォルダーの順に移動し、データベースから削除する古い列暗号化キーを探します。 キーを右クリックし、 **[削除]** をクリックします。

### <a name="permissions-for-rotating-column-encryption-keys"></a>列暗号化キーを回転するためのアクセス許可

列暗号化キーを回転するために必要なデータベース権限:**ALTER ANY COLUMN MASTER KEY** - 新しい自動生成の列暗号化キーを使用する場合に必要です (新しい列マスター キーとその新しいメタデータも生成されます)。
**ALTER ANY COLUMN ENCRYPTION KEY** - 新しい列暗号化キーのメタデータを追加するのに必要です。

また、新しい列暗号化キーと古い列暗号化キーの両方の列マスター キーにアクセスできることも必要です。 キー ストアにアクセスして、列マスター キーを使用するには、キー ストアとキーの両方、またはそのいずれかに対する権限が必要な場合があります。
- **証明書ストア – ローカル コンピューター** - 列マスター キーとして使用される証明書への読み取りアクセス権を持っているか、コンピューターの管理者である必要があります。
- **Azure Key Vault** - 列マスター キーが格納されている資格情報コンテナーに対する get、unwrapKey、および verify の権限が必要です。
- **キー ストア プロバイダー (CNG)** - キー ストアまたはキーを使用する際には、ストアと KSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。
- **暗号化サービス プロバイダー (CAPI)** - キー ストアまたはキーを使用する際には、ストアと CSP の構成に応じて、必要な権限と資格情報を入力するよう求められる場合があります。

詳細については、「[Always Encrypted の列マスター キーの作成と保存](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)」をご覧ください。

## <a name="next-steps"></a>Next Steps
- [SQL Server Management Studio で Always Encrypted を使用した列にクエリを実行する](always-encrypted-query-columns-ssms.md)
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted のキー管理の概要](overview-of-key-management-for-always-encrypted.md) 
- [SQL Server Management Studio を使用した Always Encrypted の構成](configure-always-encrypted-using-sql-server-management-studio.md)
- [PowerShell を使用した Always Encrypted の構成](configure-always-encrypted-using-powershell.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
