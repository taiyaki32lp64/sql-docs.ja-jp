---
title: 構造をネイティブ コンパイル ストアド プロシージャでサポートされています |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 6b21f47e-bceb-4054-8b3c-9d39bb9583c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc064eb8a4c6b206d3b690a4c4e7ca196c7475dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467876"
---
# <a name="supported-constructs-on-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャ上でサポートされる構造
  このトピックでは、ネイティブ コンパイル ストアド プロシージャでサポートされる構造について説明します。  
  
 サポートされていない構造については、「[インメモリ OLTP でサポートされていない Transact-SQL の構造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)」を参照してください。  
  
## <a name="procedure-ddl"></a>プロシージャ DDL  
 サポート対象は次のとおりです。  
  
-   CREATE PROCEDURE  
  
-   DROP PROCEDURE  
  
-   SCHEMABINDING (ネイティブ コンパイル ストアド プロシージャで必要です)  
  
-   NATIVE_COMPILATION  
  
-   パラメーターは NOT NULL として宣言できます。  
  
-   テーブル値パラメーター  
  
## <a name="security"></a>セキュリティ  
 サポート対象は次のとおりです。  
  
-   プロシージャ。EXECUTE AS OWNER、SELF、およびユーザー。  
  
-   テーブルおよびプロシージャに対する GRANT 権限および DENY 権限。  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)  
  
  
