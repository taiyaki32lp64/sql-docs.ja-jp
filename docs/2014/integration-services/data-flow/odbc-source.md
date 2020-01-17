---
title: ODBC 入力元 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d125a725a9e1c0cab34c7066fd9554ef0099d6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901107"
---
# <a name="odbc-source"></a>ODBC 入力元
  ODBC 入力元は、データベース テーブル、ビュー、または SQL ステートメントを使用して、ODBC でサポートされているデータベースからデータを抽出します。  
  
 ODBC 入力元には、データを抽出するために、次のデータ アクセス モードがあります。  
  
-   テーブルまたはビュー。  
  
-   SQL ステートメントの結果。  
  
 入力元は、使用するプロバイダーを指定する、ODBC 接続マネージャーを使用します。  
  
 ODBC 入力元には、ソース データ出力列があります。 出力列が ODBC 入力先で入力先列にマッピングされている場合に、入力先列にマッピングされている入力列がないときにはエラーが発生することがあります。 さまざまな種類の列をマッピングできますが、出力列と入力先との間に互換性がない場合は、実行時にエラーが発生します。 エラー動作設定に応じて、エラーが無視されるか、エラーが発生するか、エラー出力に行が送信されます。  
  
 ODBC 入力元には、1 つの標準出力と 1 つのエラー出力があります。  
  
## <a name="error-handling"></a>エラー処理  
 ODBC 入力元にはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 現在のエラーに対応する数字です。 エラーの一覧については、使用している ODBC でサポートされているデータベースのドキュメントを参照してください。 SSIS エラー コードの一覧については、「SSIS のエラー コードおよびメッセージ リファレンス」を参照してください。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   標準出力データ列。  
  
 ODBC 入力元は、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。 詳細については、「[ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../odbc-destination-editor-connection-manager-page.md)」を参照してください。  
  
## <a name="data-type-support"></a>データ型のサポート  
 ODBC 入力元でサポートされるデータ型については、「Connector for Open Database Connectivity (ODBC) by Attunity」を参照してください。  
  
## <a name="extract-options"></a>抽出オプション  
 ODBC 入力元は、 **バッチ** または **行ごと** のどちらかのモードで動作します。 使用するモードは、 **FetchMethod** プロパティによって決まります。 以下に、モードの説明を示します。  
  
-   **バッチ**: コンポーネントは、把握した ODBC プロバイダーの機能に基づいて、最も効率的なフェッチ方法を使用します。 最新の ODBC プロバイダーの場合、これは配列バインドを使用する SQLFetchScroll です (このとき、配列のサイズは **BatchSize** プロパティによって決定します)。 **[バッチ]** を選択したが、この方法がプロバイダーでサポートされていない場合、ODBC 入力先は自動的に **[行ごと]** モードに切り替わります。  
  
-   **行ごと**: コンポーネントは SQLFetch を使用して、一度に 1 行ずつ取得します。  
  
 **FetchMethod** プロパティの詳細については、「 [ODBC 入力元のカスタム プロパティ](odbc-source-custom-properties.md)」を参照してください。  
  
## <a name="parallelism"></a>Parallelism  
 並列実行できる ODBC 入力元コンポーネントの数に制限はありません。これは、同一テーブル上にある場合または異なるテーブル上にある場合、同一コンピューター上で実行する場合または異なるコンピューター上で実行する場合のいずれにも該当します (ただし、通常のグローバルなセッション制限を除きます)。  
  
 ただし、使用する ODBC プロバイダーの制限によって、プロバイダーを介するコンカレント接続数が制限される場合があります。 これらの制限によって、ODBC 入力元で使用できる並列インスタンス数のサポートが制限されます。 SSIS プロバイダーは、使用される ODBC プロバイダーの制限を把握し、SSIS パッケージを作成する際に考慮する必要があります。  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 入力元のトラブルシューティング  
 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ODBC 入力元による外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録するには、ODBC ドライバー マネージャーによるトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)*」の Microsoft のドキュメントを参照してください。  
  
## <a name="configuring-the-odbc-source"></a>ODBC 入力元の構成  
 ODBC 入力元は、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 詳細については、次のいずれかのトピックを参照してください。  
  
-   [[ODBC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [[ODBC ソース エディター] &#40;[列] ページ&#41;](../odbc-source-editor-columns-page.md)  
  
-   [[ODBC ソース エディター] &#40;[エラー出力] ページ&#41;](../odbc-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、ODBC 入力元を右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 [詳細エディター] ダイアログ ボックスで設定できるプロパティの詳細については、「 [ODBC 入力元のカスタム プロパティ](odbc-source-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [[ODBC ソース エディター] &#40;[エラー出力] ページ&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [[ODBC ソース エディター] &#40;[列] ページ&#41;](../odbc-source-editor-columns-page.md)  
  
-   [[ODBC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [ODBC 入力元を使用したデータ抽出](odbc-source.md)  
  
-   [ODBC 入力元のカスタム プロパティ](odbc-source-custom-properties.md)  
  
  
