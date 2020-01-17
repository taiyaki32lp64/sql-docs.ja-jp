---
title: ネイティブ コンパイル ストアド プロシージャ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e9bdc0c104b212f3c26389c1792b6b617634a12a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714919"
---
# <a name="natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャ
  ネイティブ コンパイル ストアド プロシージャは、ネイティブ コードにコンパイルされる [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャであり、メモリ最適化テーブルにアクセスします。 ネイティブ コンパイル ストアド プロシージャにより、ストアド プロシージャ内でクエリやビジネス ロジックを効率的に実行できます。 ネイティブ コンパイル処理の詳細については、「 [テーブルとストアド プロシージャのネイティブ コンパイル](native-compilation-of-tables-and-stored-procedures.md)」を参照してください。 ディスク ベース ストアド プロシージャをネイティブ コンパイル ストアド プロシージャに移行する方法の詳細については、「 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](migration-issues-for-natively-compiled-stored-procedures.md)」を参照してください。  
  
> [!NOTE]  
>  解釈された (ディスク ベースの) ストアド プロシージャとネイティブ コンパイル ストアド プロシージャの相違点の 1 つは、解釈されたストアド プロシージャは最初の実行時にコンパイルされ、ネイティブ コンパイル ストアド プロシージャは作成時にコンパイルされる点です。 ネイティブ コンパイル ストアド プロシージャ、多くのエラー条件 (算術オーバーフロー、型変換、および 0 除算のいくつかの条件) を検出できますで時間を作成し、失敗する場合は、ネイティブ コンパイル ストアド プロシージャの作成が発生します。 解釈されたストアド プロシージャでは、通常、このようなエラー状態によってストアド プロシージャの作成時にエラーが発生することはありませんが、実行はすべて失敗します。  
  
 このセクションのトピック:  
  
-   [ネイティブ コンパイル ストアド プロシージャの作成](creating-natively-compiled-stored-procedures.md)  
  
-   [ATOMIC ブロック](atomic-blocks-in-native-procedures.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャ内でサポートされる構造](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャでの Try..Catch の使用](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャ上でサポートされる構造](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャと実行 SET オプション](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャの呼び出しに関するベスト プラクティス](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャのパフォーマンスの監視](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [データ アクセス アプリケーションからのネイティブ コンパイル ストアド プロシージャの呼び出し](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>関連項目  
 [メモリ最適化テーブル](memory-optimized-tables.md)  
  
  
