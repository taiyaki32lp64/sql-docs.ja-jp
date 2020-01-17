---
title: MSSQLSERVER_41368 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41368 (Database Engine error)
ms.assetid: abc71559-4c4d-4cce-a08f-3299dd167842
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: 66c836c80db24b951bbf4e53d77c975eea6e4832
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123162"
---
# <a name="mssqlserver41368"></a>MSSQLSERVER_41368
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|41368|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|SQL_IMPLICIT_AND_EXPLICIT_TX_NOT_SUPPORTED|  
|メッセージ テキスト|READ COMMITTED 分離レベルを使用してメモリ最適化テーブルにアクセスする機能は、オートコミット トランザクションでのみサポートされます。 明示的なトランザクションおよび暗黙的なトランザクションではサポートされていません。 メモリ最適化テーブルには WITH (SNAPSHOT) などのテーブル ヒントを使用して、サポートされる分離レベルを指定します。|  
  
## <a name="explanation"></a>説明  
READ COMMITTED 分離レベルを使用してメモリ最適化テーブルにアクセスする機能は、自動コミット トランザクションでのみサポートされます。 詳細については、「[インメモリ テーブルおよびプロシージャでのトランザクション](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)」を参照してください。  
  
BEGIN TRANSACTION を使用して開始された明示的なトランザクション、または IMPLICIT_TRANSACTIONS が ON に設定されている状況で暗黙的なトランザクションからメモリ最適化テーブルにアクセスする場合は、READ COMMITTED 分離レベルはサポートされません。  
  
## <a name="user-action"></a>ユーザーの操作  
明示的または暗黙的な READ COMMITTED トランザクションからメモリ最適化されたテーブルにアクセスする場合は、テーブルにアクセスするために SNAPSHOT を使用します。 この手法を実現するには、テーブル ヒント WITH (SNAPSHOT) (詳細については、「[インメモリ テーブルおよびプロシージャでのトランザクション](~/relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)」を参照) を使用するか、データベース オプション MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT を ON (詳細については、「[ALTER DATABASE SET Options &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql.md)」を参照) に設定します。  
  
## <a name="see-also"></a>参照  
[インメモリ OLTP &#40;インメモリ最適化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
