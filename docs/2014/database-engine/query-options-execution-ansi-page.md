---
title: '[クエリ オプション] ([ANSI] ページ) の実行 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.ansi.f1
ms.assetid: c90d7cdf-3309-46f4-b900-220521bb9552
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d9a8b5dea5ab90137c95c9ddaf609c63532dd5b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089077"
---
# <a name="query-options-execution-ansi-page"></a>[クエリ オプション] の [実行] ([ANSI] ページ)
  このページを使用すると、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] でクエリを実行する際に ISO (ANSI) 規格で指定されているすべての設定または設定の一部を使用するように指定できます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **SET ANSI_DEFAULTS**  
 既定の ISO 設定をすべて選択します。 このボックスは ISO 設定の一部だけを構成するので、既定では使用できません。  
  
 **SET QUOTED_IDENTIFIER**  
 オブジェクト識別子を引用符で囲みます。 既定では、このオプションはオンになっています。  
  
 **SET ANSI_NULL_DFLT_ON**  
 CREATE TABLE または ALTER TABLE ステートメントの実行中に、NOT NULL が明示的に定義されていないすべてのユーザー定義データ型または列に対して、NULL 値を許容します (既定の状態)。 既定では、このオプションはオンになっています。  
  
 **[SET IMPLICIT_TRANSACTIONS]**  
 既定では、このオプションはオフになっています。  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 トランザクションがコミットされたときに開いているカーソルを自動的に閉じます (ISO に準拠)。 この値がオフに設定されている場合、トランザクションが変わってもカーソルは開いたままです。接続が終了するか、カーソルが明示的に閉じるときだけカーソルが閉じます。 既定では、このオプションはオフになっています。  
  
 **SET ANSI_PADDING**  
 列に定義されているサイズよりも短い値を列に格納する方法と、値の後に **char**、 **varchar**、 **binary**、 **varbinary** データ型で空白が続いている値を列に格納する方法を指定します。 この設定は新しい列の定義にだけ影響します。 列が作成された後は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では列の作成時の設定に基づいて値が格納されます。 この設定を後で変更しても、既存の列には影響がありません。 既定では、このチェック ボックスはオンになっています。  
  
 **SET ANSI_WARNINGS**  
 複数のエラー条件に対して ISO 標準の動作をすることを指定します。  
  
-   このチェック ボックスをオンにすると、NULL 値が集計関数 (SUM、AVG、MAX、MIN、STDEV、STDEVP、VAR、VARP、COUNT など) で使用されている場合に、警告メッセージが生成されます。 **オフ**の場合は、警告メッセージは生成されません。  
  
-   このチェック ボックスをオフにすると、0 除算や演算オーバーフロー エラーが発生したときにステートメントがロールバックされ、エラー メッセージが生成されます。 オフの場合は、0 除算や演算オーバーフロー エラーが発生したときに NULL 値が返されます。 INSERT 処理または UPDATE 処理が character、Unicode、または binary 型の列に対して実行され、新しい値が列の最大サイズより長くなると、0 除算や演算オーバーフロー エラーが原因となって NULL 値が返されます。 **[SET ANSI_WARNINGS]** がオンの場合は、INSERT 処理または UPDATE 処理は ISO 規格の指定に従って取り消されます。 文字型の列の後続の空白とバイナリ列の後続の NULL は無視されます。 OFF の場合、データは列のサイズに切り捨てられ、ステートメントは成功します。  
  
 既定では、このオプションはオンになっています。  
  
 **SET ANSI_NULLS**  
 `=`(等号) 比較演算子と`<>`(不等号) 比較演算子を NULL 値に対して使用した場合に ISO に準拠した動作をすることを指定します。 **[SET ANSI_NULLS]** がオンの場合、NULL 値に対する比較はすべて UNKNOWN として評価されます。これは ISO に準拠した動作です。 **[SET ANSI_NULLS]** がオフの場合、データ値が NULL であれば、NULL 値に対するデータの比較はすべて TRUE に評価されます。 既定では、このオプションはオンになっています。  
  
 **既定値にリセット**  
 このページ上のすべての値を元の既定値にリセットします。  
  
  
