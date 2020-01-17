---
title: メモリ最適化テーブルに対するトランザクションの概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ceedcedae64bf2ec8f8ede0ccbb99350b979fd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773381"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>メモリ最適化テーブルを対象にするトランザクションについて
  トランザクションでは、複数のバージョンから成るオプティミスティック コンカレンシーを使用して、メモリ最適化テーブルにアクセスします。 これは、データに異なるバージョンがあることを意味します。 各トランザクションでは、他の同時実行トランザクションから独立して、トランザクション上の一貫性のある固有のバージョンのデータベースを処理します。 また、トランザクションは、他の同時実行トランザクションとの競合がないというオプティミスティックな仮定の下で行われます。 これにより、ロックを使用する必要はなくなりますが、システムで競合を検出して競合状態のトランザクションの一方を終了する必要があります。 競合は書き込み - 書き込みトランザクションおよび読み取り - 書き込みトランザクションのみで発生する可能性があります。 書き込み - 書き込みが競合する場合、1 つの書き込みトランザクションが終了します。  
  
 メモリ最適化テーブルのコンカレンシー制御と、READ_COMMITTED_SNAPSHOT および SNAPSHOT のトランザクション分離レベルを対象とするディスク ベース テーブルのコンカレンシー制御には類似点があります。 (ディスク ベース テーブルの詳細については、次を参照してください[データベース エンジン内の行のバージョン管理に基づく分離レベル](https://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx)。)。  
  
## <a name="topics-in-this-section"></a>このセクションのトピック  
 ここでは、次のトピックを含め、メモリ最適化テーブルのトランザクションを取り扱います。  
  
-   [メモリ最適化テーブルのトランザクション分離レベルに関するガイドライン](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [メモリ最適化テーブルでのトランザクションの再試行ロジックのガイドライン](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [メモリ最適化テーブルでのトランザクション](transactions-in-memory-optimized-tables.md)  
  
-   [トランザクション分離レベル](transaction-isolation-levels.md)  
  
-   [複数コンテナーにまたがるトランザクション](cross-container-transactions.md)  
  
 詳しくは、「[トランザクションの持続性の制御](../relational-databases/logs/control-transaction-durability.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブル](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
