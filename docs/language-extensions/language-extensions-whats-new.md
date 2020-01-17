---
title: SQL Server 言語拡張の新機能
titleSuffix: ''
description: SQL Server の言語拡張の新機能について説明します。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3bcf60c390b06695c4913bd1347045b807c1ae9d
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658805"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>SQL Server 言語拡張の新機能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

外部言語とデータ プラットフォーム間の統合が継続的に拡大、拡張、および強化されており、各リリースで[言語拡張](language-extensions-overview.md)機能が SQL Server に追加されています。 

## <a name="new-in-sql-server-2019"></a>SQL Server 2019 の新機能 

このリリースでは、SQL Server 言語拡張のサポートが追加されました。 このリリースのすべての機能の詳細については、「[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md)」および「[SQL Server 2019 のリリース ノート](../sql-server/sql-server-ver15-release-notes.md)」を参照してください。

- Windows および Linux の既定の Java ランタイムは Open Zulu JRE であり、[Windows 上の SQL Server 言語拡張のインストール](install/install-sql-server-language-extensions-on-windows.md)と [Linux 上の SQL Server 言語拡張のインストール](../linux/sql-server-linux-setup-language-extensions.md)に含まれています。
- サポートされている [Java データ型](how-to/java-to-sql-data-types.md)。
- SQL Server で外部言語 (Java など) を登録するための [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)。
- [Microsoft 拡張機能 SDK for Java](how-to/extensibility-sdk-java-sql-server.md)。
- Windows および Linux 上では、外部ライブラリで [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md) ステートメントを使用して Java コードにアクセスできます。 詳細情報:[SQL Server から Java を呼び出す方法](how-to/call-java-from-sql.md)。
- Windows および Linux 上の [Java 言語拡張](language-extensions-overview.md)。 アクセス許可を割り当て、パスを設定することで、コンパイル済みの Java コードを SQL Server で使用できるようになります。 SQL Server にアクセスできるクライアント アプリでは、[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) を呼び出すことで、データを使用し、コードを実行することができます。これは、SQL Server Machine Learning Services 上での R と Python の統合に使用されるものと同じ手順です。

## <a name="next-steps"></a>次の手順

+ [Windows 上](install/install-sql-server-language-extensions-on-windows.md)または [Linux 上に SQL Server 言語拡張をインストール](../linux/sql-server-linux-setup-language-extensions.md)します
