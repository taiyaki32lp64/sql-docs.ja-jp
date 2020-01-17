---
title: 文字列データの比較 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3c84997d8ec11a4eb620daf7bf34af7adf3e8de1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293237"
---
# <a name="comparing-string-data"></a>比較、文字列データ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文字列比較は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]によって実行される多くの変換において重要な部分です。また、文字列比較は、変数内の式やプロパティ式の評価でも使用されます。 たとえば、並べ替え変換はデータセット内の値を比較し、昇順または降順にデータを並べ替えます。  
  
## <a name="configuring-transformations-for-string-comparisons"></a>文字列の比較時の変換の構成  
 並べ替え変換、集計変換、あいまいグループ化変換、およびあいまい参照変換をカスタマイズして、文字列の比較方法を列レベルで変更できます。 たとえば、比較で大文字と小文字を区別しないように指定できます。この場合は、大文字と小文字が同じ文字として扱われます。  
  
 次の変換は、文字列比較を含むことができる式を使用します。  
  
-   条件分割変換は、式の内部で文字列比較を使用し、データ行を送信する出力を決定できます。 詳細については、「 [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md)」を参照してください。  
  
-   派生列変換は、式の内部で文字列比較を使用し、新しい列の値を生成できます。 詳細については、「 [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md)」を参照してください。  
  
 変数、変数マッピング、および優先順位制約でも、文字列比較を含めた式を使用できます。 式の詳細については、「[Integration Services &#40;SSIS&#41; の式](../../integration-services/expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
## <a name="processing-during-string-comparison"></a>文字列の比較時の処理  
 データおよび変換の構成によっては、文字列データの比較中に次の処理が発生する場合があります。  
  
-   データの Unicode への変換。 変換元のデータが Unicode でない場合、比較が行われる前に自動的に Unicode に変換されます。  
  
-   ロケールを使用した、日付、時間、10 進数データ、および並べ替え順序を解釈するための、ロケール固有のルールの適用。  
  
-   比較の区別を変更するための、列レベルでの比較オプションの適用。  
  
## <a name="converting-string-data-to-unicode"></a>文字列データの Unicode への変換  
 変換が実行する操作や変換の構成によっては、文字列データは、文字列の Unicode 表現である DT_WSTR データ型に変換される場合があります。  
  
 DT_STR データ型の文字列データは、列のコード ページを使用して Unicode に変換されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、列レベルでのコード ページがサポートされており、各列はそれぞれ異なるコード ページを使用して変換できます。  
  
 多くの場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はデータ ソースから正しいコード ページを識別できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースおよび列レベルで照合順序を設定できます。 コード ページは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序から取得します。この照合順序には、Windows または SQL の照合順序のどちらかを設定できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が予期しないコード ページを提供する場合、またはパッケージが正しいコード ページを決定するための十分な情報を提供しないプロバイダーを使用してデータ ソースにアクセスする場合は、OLE DB ソースおよび OLE DB 変換先で既定のコード ページを指定できます。 既定のコード ページは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で提供されるコード ページの代わりに使用されます。  
  
 ファイルにはコード ページはありません。 代わりに、パッケージがファイル データへの接続に使用するフラット ファイル接続マネージャーおよび複数フラット ファイル接続マネージャーに、ファイルのコード ページを指定するプロパティが含まれます。 コード ページはファイル レベルでのみ設定できます。列レベルでは設定できません。  
  
## <a name="setting-locale"></a>ロケールの設定  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、データを並べ替えたり、日付、時間、および 10 進数データを解釈するためのロケール固有のルールを推定する場合、コード ページを使用しません。 その代わり、変換はデータ フロー コンポーネント、データ フロー タスク、コンテナー、またはパッケージ上の LocaleId プロパティによって設定されるロケールを読み取ります。 既定では、変換のロケールはデータ フロー タスクから継承され、データ フロー タスクはパッケージからロケールを継承します。 データ フロー タスクが For ループ コンテナーなどのコンテナー内にある場合は、コンテナーからロケールを継承します。  
  
 また、フラット ファイル接続マネージャーや、複数のフラット ファイル接続マネージャー用のロケールも指定できます。  
  
## <a name="setting-comparison-options"></a>比較オプションの設定  
 ロケールは、文字列データの比較に関する基本ルールを提供します。 たとえば、ロケールは、アルファベット内の各文字の並べ替えの位置を指定します。 ただし、こうしたルールは一部の変換が実行する比較に対しては十分でない場合があり、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ではロケールの比較ルールよりも詳細な比較オプションのセットがサポートされています。 これらの比較オプションは、列レベルで設定されます。 たとえば、詳細比較オプションの 1 つを使用すると、分音文字を無視できます。 このオプションをオンにした場合、比較時にアクセントなどの分音記号が無視され、"a" と "Ã¡" が同一と見なされます。  
  
 次の表では、比較オプションと並べ替えスタイルについて説明します。  
  
|比較オプション|[説明]|  
|-----------------------|-----------------|  
|大文字と小文字を区別しない|比較時に、大文字と小文字を区別するかどうかを示します。 このオプションを設定した場合、文字列比較で大文字と小文字は区別されません。 たとえば、"ABC" は "abc" と同一になります。|  
|カタカナを区別しない|日本語の比較で、2 種類のかな文字である、ひらがなとカタカナを区別するかどうかを指定します。 このオプションを設定した場合、文字列比較でひらがなとカタカナは区別されません。|  
|文字幅を区別しない|比較で、1 バイト文字と、それと同じ文字を表記した 2 バイト文字を区別するかどうかを指定します。 このオプションを設定した場合、文字列比較で 1 バイト表記と 2 バイト表記は同一文字として扱われます。|  
|分音文字を無視する|比較で、通常の文字と分音文字付きの文字を区別するかどうかを指定します。 このオプションを設定した場合、比較で分音文字は無視されます。 たとえば、"Ã¥" は "a" に等しくなります。|  
|記号を無視する|比較で、通常の文字を、空白文字、句読点、通貨記号、数学記号などの記号と区別するかどうかを指定します。 このオプションを設定した場合、文字列比較で記号は無視されます。 たとえば、" New York" は "New York" と同一になり、"*ABC" は "ABC" と同一になります。|  
|句読点を記号として並べ替え|比較で、ハイフンとアポストロフィを除くすべての句読点記号を、英数文字の前に並べ替えるかどうかを指定します。 たとえば、このオプションを設定すると、".ABC" は "ABC" の前に並べ替えられます。|  
  
 並べ替え変換、集計変換、あいまいグループ化変換、およびあいまい参照変換には、データを比較するためのこれらのオプションが含まれています。  
  
 あいまいグループ化変換およびあいまい参照変換の **[詳細エディター]** ダイアログ ボックスには、 **[FullySensitive]** 比較フラグが表示されます。 **[FullySensitive]** 比較フラグを選択すると、すべての比較オプションが適用されます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)   
 [高速解析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [標準解析](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
