---
title: 強力なパスワード | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6737a954881a56961b77dcf7d8f0373b0e30e848
ms.sourcegitcommit: 03884a046aded85c7de67ca82a5b5edbf710be92
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564753"
---
# <a name="strong-passwords"></a>強力なパスワード
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  パスワードは、サーバーのセキュリティ上で最も弱点になる可能性があります。 パスワードを選択するときは、常に最大限の注意が必要です。 強力なパスワードの特徴は次のとおりです。  
  
-   8 文字以上である  
  
-   文字、数字、および記号を組み合わせたパスワードである  
  
-   辞書に載っていない  
  
-   コマンド名ではない  
  
-   人名ではない  
  
-   ユーザー名ではない  
  
-   コンピューター名ではない  
  
-   定期的に変更される  
  
-   以前のパスワードと明らかに異なる  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパスワードは、最大 128 文字までで、英字、記号、数字を使用できます。 ログイン、ユーザー名、ロール、およびパスワードは [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで使用されることが多く、特定の記号については二重引用符 (") または角かっこ ([ ]) で囲む必要が生じます。 これらの区切り記号を [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで使用するのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログイン、ユーザー、ロール、またはパスワードに次のような特徴がある場合です。  
  
-   スペースが含まれているか、スペースが先頭にある  
  
-   $ または \@ で始まる  
  
 OLE DB または ODBC の接続文字列で使用する場合、ログインまたはパスワードに次の文字は含めないでください: [] {}() , ; ? * ! \@ =。 これらの文字は、接続の初期化や、接続の値を区切る場合に使用されています。  
  
## <a name="related-content"></a>関連コンテンツ  
 [パスワード ポリシー](../../relational-databases/security/password-policy.md)  
  
  
