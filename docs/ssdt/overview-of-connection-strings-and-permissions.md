---
title: 接続文字列とアクセス許可の概要 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ceff114e-a738-46ad-9785-b6647a2247f9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ae4fe656cbd299d46960ec9b711de4c51d30a51
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064791"
---
# <a name="overview-of-connection-strings-and-permissions"></a>接続文字列とアクセス許可の概要
SQL Server 単体テストを実行するには、1 つまたは 2 つの特定の接続文字列を使用してデータベース サーバーに接続する必要があります。 各接続文字列は、テストの一部として特定のスクリプトでタスクまたはタスク セットを実行するために必要な特定のアクセス許可を保持するアカウントを表します。 これらの文字列は、 **[SQL Server テスト構成]** ダイアログ ボックスで指定するか、テスト プロジェクトの app.config ファイルを手動で編集することにより指定できます。  
  
## <a name="connection-strings"></a>接続文字列  
**[SQL Server テスト構成]** ダイアログ ボックスで、次の各アカウントの接続文字列を指定できます。  
  
> [!NOTE]  
> 実行コンテキストと特権コンテキストが異なるのは、SQL Server 認証を使用する場合のみです。 Windows 認証を使用する場合、同じ資格情報が両方の接続文字列に使用されます。  
  
-   実行コンテキスト (必須): テスト スクリプトを実行するためのユーザー アカウントです。 この接続文字列には、ユーザーが保持するのと同じ資格情報が必要です。 これによって適切なアクセス許可がデータベースに適用されていることが確認できるため、これは重要です。 詳細については、「[ソフト NUMA を使用するようにSQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)」を参照してください。  
  
    テスト プロジェクトの app.config ファイルでは、このアカウントは `ExecutionContext` 要素です。  
  
-   特権コンテキスト (省略可能): 事前テスト アクション、事後テスト アクション、TestInitialize、および TestCleanup の各スクリプトを実行するための上位のアクセス許可を保持している、同じデータベース上のアカウントです。 これらのスクリプトは、データベース状態を設定します。また事後テスト アクションについては、データベース内のオブジェクトを検証するために使用できます。 この接続文字列は、データベースの変更を配置し、データを生成するためにも使用されます。  
  
    テスト プロジェクトの app.config ファイルでは、このアカウントは `PrivilegedContext` 要素です。 SQL Server 単体テストでテスト スクリプトのみを実行する場合、特権コンテキストを指定する必要はありません。  
  
[プロジェクト構成] ダイアログ ボックスで指定する文字列は、テスト プロジェクトの app.config ファイルに格納されます。 このファイルを直接編集し、プロジェクトをリビルドすることもできます。その後は、新しい値がダイアログ ボックスに表示されます。  
  
## <a name="windows-authentication-versus-sql-server-authentication"></a>Windows 認証と SQL Server 認証  
接続文字列を指定するときに、Windows 認証と SQL 認証のどちらを使用するかを選択する必要があります。 Windows 認証を選択する理由の 1 つとして、チームによるテストの使用が、SQL Server 認証よりも適切にサポートされているという点が挙げられます。 SQL Server 認証を選択した場合、接続文字列は、ユーザー資格情報に基づき、データ保護 API (DPAPI) を使用して暗号化されます。 つまり、このテスト プロジェクトのテストは、作成者のみが実行できます。テストをチェックインした後にソース制御システムでテストを取得したチーム メンバーは実行できません。 チーム内の他のメンバーがこのテスト プロジェクトのテストを実行するには、自分の資格情報を使用してテスト プロジェクトを再構成する必要があります。 そのためには、app.config ファイルのコピーを編集するか、[プロジェクト構成] ダイアログ ボックスを使用します。  
  
## <a name="permissions"></a>アクセス許可  
テスト スクリプトは、実行コンテキストのアクセス許可レベルで実行されます。このアクセス許可レベルは、通常の使用状態のデータベースで実行されるユーザー コマンドに対して有効なアクセス許可レベルと同じです。 事前テスト アクション、事後テスト、TestInitialize、および TestCleanup の各スクリプトは、特権コンテキストのアクセス許可レベルで実行されます。  
  
事後テスト アクション スクリプトにはアクセス許可レベルの高い接続が使用されるため、このスクリプトで検証を実行することができます。 また、このスクリプトでは、アクセス許可をテストするスクリプト コマンドを実行することもできます。 アクセス許可の詳細については、「[SQL Server Data Tools に必要な権限](../ssdt/required-permissions-for-sql-server-data-tools.md)」の SQL Server 単体テストに関するセクションを参照してください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)  
[SQL Server の単体テストのファイル](../ssdt/sql-server-unit-test-files.md)  
  
