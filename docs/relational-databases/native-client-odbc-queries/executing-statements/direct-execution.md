---
title: 直接実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, statements
- direct execution [ODBC]
- SQLExecDirect function
- statements [ODBC], direct execution
ms.assetid: fa36e1af-ed98-4abc-97c1-c4cc5d227b29
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 292b0f787819a52eb5759ead41bde80fc3a72acf
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73779757"
---
# <a name="direct-execution"></a>直接実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  直接実行はステートメントを実行する最も基本的な方法です。 アプリケーションは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを含む文字列を構築し、 **SQLExecDirect**関数を使用して実行するために送信します。 ステートメントがサーバーに到達すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がステートメントを実行プランにコンパイルしてから、すぐにその実行プランを実行します。  
  
 直接実行は、通常、実行時にステートメントを構築して実行するアプリケーションで使用され、1 回だけステートメントを実行する場合には最も効率的な方法です。 多くのデータベースでの直接実行の欠点は、SQL ステートメントを実行するたびに解析とコンパイルが必要なことで、ステートメントを複数回実行する場合はオーバーヘッドが増加します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、マルチユーザー環境で通常実行されるステートメントに関して、直接実行のパフォーマンスが大幅に向上します。また、通常、SQL ステートメントの実行にパラメーター マーカーを指定して SQLExecDirect を使用すると、準備実行に近い効率を得ることができます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに接続されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは[sp_executesql](../../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md)を使用して、 **SQLExecDirect**で指定された SQL ステートメントまたはバッチを転送します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、 **sp_executesql**で実行された SQL ステートメントまたはバッチが、既にメモリに存在する実行プランを生成したステートメントまたはバッチと一致するかどうかをすばやく判断するロジックがあります。 一致する場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は新しいプランをコンパイルしないで、単に既存のプランを再利用します。 これは、多くのユーザーがいるシステムで**SQLExecDirect**を使用して実行された一般的に実行される SQL ステートメントが、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のストアドプロシージャでしか使用できなかった、プラン再利用の多くの利点を活用できることを意味します。  
  
 実行プランを再利用することで得られる利点は、複数のユーザーが同じ SQL ステートメントやバッチを実行しているときにのみ効果があります。 異なるクライアントが実行する SQL ステートメントを可能な限り統一の取れたステートメントにして、実行プランの再利用を可能にするために、次のコーディング規則に従ってください。  
  
-   SQL ステートメントには定数データを含めません。代わりにプログラム変数にバインドされるパラメーター マーカーを使用します。 詳細については、「[ステートメントパラメーターの使用](../../../relational-databases/native-client-odbc-queries/using-statement-parameters.md)」を参照してください。  
  
-   完全修飾オブジェクト名を使用します。 実行プランは、オブジェクト名が修飾されていないと再利用されません。  
  
-   アプリケーション接続では、できる限り、接続オプションとステートメント オプションの共通のセットを使用します。 あるオプションのセット (ANSI_NULLS など) を使用する接続に対して生成される実行プランは、別のオプションのセットを使用する接続には再利用されません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、どちらもこれらのオプションに同じ既定値を使用します。  
  
 **SQLExecDirect**で実行されたすべてのステートメントが、これらの規則を使用してコード化されている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、営業案件が発生したときに実行プランを再利用でき  
  
## <a name="see-also"></a>参照  
 [ステートメント&#40;の実行 ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
