---
title: ネイティブ コンパイル ストアド プロシージャと SET オプション
ms.custom: seo-dt-2019
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f626c997ac0615eefa7caede0f379c22fed25ab6
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412573"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>ネイティブ コンパイル ストアド プロシージャと実行 SET オプション
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

「[ATOMIC ブロック](atomic-blocks-in-native-procedures.md)」で説明されているように、セッションのオプションは ATOMIC ブロックでは固定されています。 ATOMIC ブロックは必須なので、ストアド プロシージャの実行はセッションの SET オプションの影響を受けません。 ただし、特定の SET オプション (SET NOEXEC や SET SHOWPLAN_XML など) を指定すると、ストアド プロシージャ (ネイティブ コンパイル ストアド プロシージャを含む) が実行されなくなります。   
  
 任意の STATISTICS オプションを有効にしてネイティブ コンパイル ストアド プロシージャを実行すると、統計情報は、ステートメントごとではなく、プロシージャ全体に対して収集されます。 詳細については、「[SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md)」、「[SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md)」、「[SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)」、「[SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)」を参照してください。 ネイティブ コンパイル ストアド プロシージャのステートメントごとのレベルに対する実行統計を取得するには、ストアド プロシージャの実行に含まれる各クエリが完了したときに開始される sp_statement_completed イベントの拡張イベント セッションを使用します。 拡張イベント セッションの作成の詳細については、「[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)」を参照してください。  
  
 ネイティブ コンパイル ストアド プロシージャでは、**SHOWPLAN_XML** がサポートされています。 **SHOWPLAN_ALL** と **SHOWPLAN_TEXT** は、ネイティブ コンパイル ストアド プロシージャではサポートされていません。  
  
 **SET FMTONLY** は、ネイティブ コンパイル ストアド プロシージャではサポートされていません。 代わりに [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) を使用します。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
