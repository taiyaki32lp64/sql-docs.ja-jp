---
title: Integration Services (SSIS) の式 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- expressions [Integration Services], packages
- SSIS packages, expressions
ms.assetid: 26d2e242-7f60-4fa9-a70d-548a80eee667
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f2e884e7a34af6cae14b4b057038e54b20255200
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71289685"
---
# <a name="integration-services-ssis-expressions"></a>Integration Services (SSIS) の式

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  式は、単一のデータ値が得られる、識別子、リテラル、関数、演算子などの記号の組み合わせです。 単純式には、1 つの定数、変数、または関数を指定できます。 より頻繁に使用されるのは複雑な式で、複数の演算子や関数を使用し、複数の列や変数を参照します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、CASE ステートメントの条件の定義、データ列値の生成および更新、変数への値の代入、実行時のプロパティの更新および作成、優先順位制約の制約の定義、および For ループ コンテナーでの利用に式を使用できます。  
  
 式は、式の言語および式エバリュエーターに基づいています。 式エバリュエーターは式を解析して、式の言語のルールに従っているかどうか判断します。 式の構文およびサポートされているリテラルと識別子の詳細については、次のトピックを参照してください。  
  
-   [構文 (SSIS)](../../integration-services/expressions/syntax-ssis.md)  
  
-   [リテラル (SSIS)](../../integration-services/expressions/numeric-string-and-boolean-literals.md)  
  
-   [識別子 (SSIS)](../../integration-services/expressions/identifiers-ssis.md)  
  
## <a name="components-that-use-expressions"></a>式を使用するコンポーネント  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の次の要素で式を使用できます。  
  
-   条件分割変換では、式に基づいて、データ行を別の出力先に出力するかどうかを決定する決定構造が実装されます。 条件分割変換で使用する式は、 **true** または **false**に評価される必要があります。 たとえば、式 "Column1 > Column2" の条件を満たす行は、別の出力にルーティングされます。  
  
-   派生列変換では、式で生成された値を使用して、データ フローに新しい列を作成するか、または既存の列を更新します。 たとえば、Column1 + " ABC" という式を使用して連結された文字列で、値を更新したり、新しい値を生成できます。  
  
-   変数に値を設定するために式を使用します。 たとえば、GETDATE() を使用すると、変数の値として現在の日付が設定されます。  
  
-   優先順位制約では、式を使用して、パッケージ内の制約付きタスクまたはコンテナーを実行するかどうか判断する条件を指定します。 優先順位制約で使用する式は、 **true** または **false**に評価される必要があります。 たとえば、\@A > \@B という式は 2 つのユーザー定義変数を比較して、制約付きタスクを実行するかどうかを判断します。  
  
-   For ループ コンテナーでは、式を使用して、ループ構造で使用する初期化ステートメント、評価ステートメント、および増分ステートメントを作成します。 たとえば、\@Counter = 1 という式はループ カウンターを初期化します。  
  
 式は、パッケージ、For ループや Foreach ループなどのコンテナー、タスク、パッケージおよびプロジェクト レベルの接続マネージャー、ログ プロバイダー、Foreach 列挙子のプロパティ値の更新にも使用できます。 たとえば、プロパティの式を使用して、"Localhost.AdventureWorks" という文字列を SQL 実行タスクの ConnectionName プロパティに割り当てることができます。 詳細については、「 [パッケージでプロパティ式を使用する](../../integration-services/expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
## <a name="icon-markers-for-expressions"></a>式のアイコン マーカー  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]では、式が設定されている接続マネージャー、変数、およびタスクの横に特別なアイコン マーカーが表示されます。 **HasExpressions** プロパティは、変数を除き、式をサポートするすべての SSIS オブジェクトで使用できます。 このプロパティにより、式が設定されているオブジェクトを簡単に識別できます。  
  
## <a name="expression-builder"></a>[式ビルダー]  
 式ビルダーは、式を作成するためのグラフィック ツールです。 **[条件分割変換エディター]** ダイアログ ボックス、 **[派生列変換エディター]** ダイアログ ボックス、および **[式ビルダー]** ダイアログ ボックスで使用できます。  
  
 式ビルダーでは、パッケージ固有の要素が格納されているフォルダーと、式の言語で使用される関数、型キャスト、演算子が格納されているフォルダーが用意されています。 パッケージ固有の要素として、システム変数とユーザー定義変数が含まれます。 **[条件分割変換エディター]** ダイアログ ボックスおよび **[派生列変換エディター]** ダイアログ ボックスでは、データ列も表示されます。 変換のための式を作成するには、フォルダー内のアイテムを **[条件]** または **[式]** 列にドラッグするか、式を列に直接入力します。 式ビルダーは、変数名の \@ プレフィックスなど、必要な構文要素を自動的に追加します。  
  
> [!NOTE]  
>  ユーザー定義変数およびシステム変数の名前では、大文字と小文字が区別されます。  
  
 変数にはスコープがあるため、式ビルダーの **[変数]** フォルダーにはスコープ内で使用できる変数のみが表示されます。 詳細については、「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フロー コンポーネントで式を使用する](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
## <a name="see-also"></a>参照  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
