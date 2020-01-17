---
ms.openlocfilehash: 4803a99e0fb1435b545ec775b2a8abe063d9fd8d
ms.sourcegitcommit: cbbb210c0315f9e2be2b9cd68db888ac53429814
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69890923"
---
**SA** アカウントは、セットアップ時に作成される SQL Server インスタンスのシステム管理者です。 SQL Server のコンテナーを作成した後、そのコンテナーで `echo $MSSQL_SA_PASSWORD` を実行すると、指定した環境変数 `MSSQL_SA_PASSWORD` が検索できるようになります。 セキュリティのため、SA のパスワードを変更してください。

1. SA ユーザーに使用する強力なパスワードを選択します。

1. Transact-SQL ステートメントを使用してパスワードを変更するには、`docker exec` を使用して **sqlcmd** ユーティリティを実行します。 `<YourStrong!Passw0rd>` と `<YourNewStrong!Passw0rd>` は、実際のパスワードの値に置き換えます。

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
