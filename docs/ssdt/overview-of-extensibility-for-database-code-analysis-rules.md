---
title: データベース コード分析ルールの機能拡張の概要 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fd64a7c3152941a88122543dc4b8b80045f175a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984491"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>データベース コード分析ルールの機能拡張の概要
SQL Server Data Tools を含む Visual Studio エディションには、Transact\-SQL のデータベース コードの設計、命名、およびパフォーマンスに関する警告についてレポートするコード分析ルールが用意されています。 詳細については、「[データベース コードの分析によるコードの品質の向上](https://msdn.microsoft.com/library/dd172133(v=vs.100).aspx)」を参照してください。  
  
組み込みのコード分析ルールに、必要な Transact\-SQL の問題がない場合は、カスタムのデータベース コード分析ルールを作成できます。 たとえば、「[チュートリアル: SQL Server のカスタムの静的コード分析ルール アセンブリを作成する](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md)」のように、WAITFOR DELAY ステートメントを使用しないカスタム ルールを作成できます。 カスタムのデータベース コード分析ルールを作成するには、[CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx) 名前空間のクラスを使用します。  
  
カスタム コード分析ルールを作成する前に、データベース コード分析ルールのさまざまなコンポーネントの中でも、基本アーキテクチャについて理解しておく必要があります。  
  
## <a name="database-code-analysis-rules-components"></a>データベース コード分析ルールのコンポーネント  
次の図は、データベース コード分析ルールのコンポーネント間の処理です。  
  
![データベース コード分析ルールのコンポーネント](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "データベース コード分析ルールのコンポーネント")  
  
静的コード分析を直接実行するか (詳細については、「[方法: Transact-SQL コードを分析して障害を検出する](https://msdn.microsoft.com/library/dd172119(v=vs.100).aspx)」を参照してください)、またはビルドを実行することで、データベース コード分析ルール機能を使用する場合は、すべてのルールが読み込まれ、ご利用のプロジェクトでのそれらの構成内容に従って使用されます。 詳細については、「[ソフト NUMA を使用するようにデータベース コードのスタティック分析の特定の規則を有効または無効にする](https://msdn.microsoft.com/library/dd172131(v=vs.100).aspx)」を参照してください。 拡張機能マネージャーには、作成、登録したカスタム ルール アセンブリも読み込まれます。 詳細については、「[ソフト NUMA を使用するように機能拡張のインストールと管理](../ssdt/how-to-install-and-manage-feature-extensions.md)」を参照してください。  
  
カスタムのコード分析ルール クラスは、[SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx) から継承します。 カスタムのルール クラスからは、ルール実行コンテキスト経由で便利なオブジェクトにアクセスできます。 たとえば、次のオブジェクトにアクセスできます。  
  
-   ルール自体に関するメタデータ。  
  
-   データベースのスキーマを表す Dac.Model.TSqlModel。すべてのモデル要素、要素間の関係、要素のプロパティなどです。  
  
-   特定の要素を確認するルールの場合、モデル内のそのスキーマ要素を表す Dac.Model.TSqlObject をコンテキストに含めます。  
  
-   多くのスキーマ オブジェクトには、このコンテキスト経由でアクセスできる [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表現も含まれます。これは、要素の AST ベースの表現です。[SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx) の存在など、構文の問題を確認するときに便利です。  
  
Dac.CodeAnalysis.SqlRuleProblem は、検出された問題を表すルールで作成されます。 このルールを作成すると、関連する Dac.Model.TSqlObject と場合によっては [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 表現要素がコンストラクターに渡され、ソース コード ファイルの問題の場所を特定するために使用されます。 分析が完了すると、すべての問題がエラー マネージャーに渡され、エラー一覧に表示されます。  
  
## <a name="see-also"></a>参照  
[データベース機能の拡張](../ssdt/extending-the-database-features.md)  
  
