---
title: CDC ソース | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4572e9fc61649f638b7c86ee23c75450216a4342
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62828128"
---
# <a name="cdc-source"></a>CDC ソース
  CDC ソースは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 変更テーブルから変更データの範囲を読み取り、変更内容を下流の他の SSIS コンポーネントに伝えます。  
  
 CDC ソースによって読み取られた変更データの範囲は "CDC 処理範囲" と呼ばれ、現在のデータ フローの開始前に実行される CDC 制御タスクによって決定されます。 CDC 処理範囲は、テーブル グループの CDC 処理の状態を保持するパッケージ変数の値から導き出されます。  
  
 CDC ソースは、データベース テーブル、ビュー、または SQL ステートメントを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからデータを抽出します。  
  
 CDC ソースは、次の構成を使用します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC データベースにアクセスするための、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 接続マネージャー。 CDC ソース接続を構成する方法の詳細については、「 [[CDC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../cdc-source-editor-connection-manager-page.md)」を参照してください。  
  
-   CDC のために有効にされたテーブル。  
  
-   選択したテーブルのキャプチャ インスタンスの名前 (複数存在する場合)。  
  
-   変更処理モード。  
  
-   CDC 処理範囲が決定される基になる、CDC 状態パッケージ変数の名前。 CDC ソースによって、その変数が変更されることはありません。  
  
 CDC ソースによって返されるデータは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 関数の **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** または **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** (使用できる場合) によって返されるデータと同じです。 唯一、必要に応じて追加できる列として **__$initial_processing** があります。この列は、現在の処理範囲がテーブルの初期読み込みの範囲と重複できるかどうかを示します。 初期処理の詳細については、「 [CDC 制御タスク](../control-flow/cdc-control-task.md)」を参照してください。  
  
 CDC ソースには、1 つの標準出力と 1 つのエラー出力があります。  
  
## <a name="error-handling"></a>エラー処理  
 CDC ソースにはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 値は常に -1 です。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   **エラー行の列**: エラーの原因となったレコード データ。  
  
 CDC ソースは、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。 詳細については、「 [[CDC ソース エディター] &#40;[エラー出力] ページ&#41;](../cdc-source-editor-error-output-page.md)」を参照してください。  
  
## <a name="data-type-support"></a>データ型のサポート  
 Microsoft の CDC ソース コンポーネントはすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートし、SSIS データ型に正確にマッピングします。  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC ソースのトラブルシューティング  
 以下に、CDC ソースのトラブルシューティング情報を示します。  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>このスクリプトを使用して問題を特定し、SQL Server Management Studio で再現する  
 CDC ソース操作は、CDC ソースを呼び出す前に実行される CDC 制御タスク操作によって管理されます。 CDC 制御タスクは、開始 LSN と終了 LSN が保存されている CDC 状態パッケージ変数の値を比較します。 CDC 制御タスクは、次のスクリプトに相当する関数を実行します。  
  
```  
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 それぞれの文字の説明は次のとおりです。  
  
-   \<cdc-enabled-database-name> は、変更テーブルが含まれている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの名前です。  
  
-   \<value-from-state-cs> は、CDC 状態変数に、CS/\<value-from-state-cs>/ として示される値です (CS は Current-processing-range-Start (現在の処理範囲の開始) の略語です)。  
  
-   \<value-from-state-ce> は、CDC 状態変数に、CE/\<value-from-state-ce>/ として示される値です (CE は Current-processing-range-End (現在の処理範囲の終了) の略語です)。  
  
-   \<mode> は、CDC の処理モードです。 この処理モードは、 **[すべて]** 、 **[古い値を含むすべて]** 、 **[差分]** 、 **[更新マスクを含む差分]** 、 **[結合を含む差分]** のいずれかの値です。  
  
 このスクリプトを実行すると、エラーの再現と特定を簡単に行うことができる [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で問題を再現することによって、問題を特定できます。  
  
#### <a name="sql-server-error-message"></a>SQL Server エラー メッセージ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって、次のメッセージが返されることがあります。  
  
 **プロシージャまたは関数 cdc.fn_cdc_get_net_changes_\<..> に指定された引数が不足しています。**  
  
 このエラーは、引数が不足していることを示すものではありません。 CDC 状態変数の開始または終了 LSN 値が無効であることを示します。  
  
## <a name="configuring-the-cdc-source"></a>CDC ソースの構成  
 CDC ソースは、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 詳細については、次のいずれかのトピックを参照してください。  
  
-   [[CDC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [[CDC ソース エディター] &#40;[列] ページ&#41;](../cdc-source-editor-columns-page.md)  
  
-   [CDC ソース エディター &#40;[エラー出力] ページ&#41;](../cdc-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、CDC ソースを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 **[詳細エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [CDC ソースのカスタム プロパティ](cdc-source-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [[CDC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../cdc-source-editor-connection-manager-page.md)  
  
-   [[CDC ソース エディター] &#40;[列] ページ&#41;](../cdc-source-editor-columns-page.md)  
  
-   [[CDC ソース エディター] &#40;[エラー出力] ページ&#41;](../cdc-source-editor-error-output-page.md)  
  
-   [CDC ソースのカスタム プロパティ](cdc-source-custom-properties.md)  
  
-   [CDC ソースを使用した変更データ抽出](cdc-source.md)  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   mattmasson.com のブログ「[CDC ソースの処理モード](https://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/)」  
  
  
