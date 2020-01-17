---
title: OLE DB コマンド変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09850707b83481909a881dcefdf00e710e6a8790
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291247"
---
# <a name="ole-db-command-transformation"></a>OLE DB コマンド変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB コマンド変換は、データ フローの各行に対して SQL ステートメントを実行します。 たとえば、データベース テーブル内に行を挿入したり、行を更新または削除する SQL ステートメントを実行できます。  
  
 OLE DB コマンド変換は、次の方法で構成できます。  
  
-   各行に対して変換が実行する SQL ステートメントを指定します。  
  
-   SQL ステートメントがタイムアウトになる時間を秒数で指定します。  
  
-   既定のコード ページを指定します。  
  
 通常、SQL ステートメントにはパラメーターが含まれます。 パラメーター値は変換入力内の外部列に格納され、入力列を外部列にマップすることによって、入力列をパラメーターにマップします。 たとえば、 **ProductKey** 列の値を使用し、 **DimProduct** テーブルの行を探して削除するには、 **Param_0** という名前の外部列を **ProductKey** という名前の入力列にマップし、SQL ステートメント `DELETE FROM DimProduct WHERE ProductKey = ?`を実行します。 OLE DB コマンド変換で用意されているパラメーター名は変更できません。 パラメーター名は、 **Param_0**、 **Param_1**のように指定されます。  
  
 **[詳細エディター]** ダイアログ ボックスを使用して OLE DB コマンド変換を構成する場合、SQL ステートメント内のパラメーターは変換入力内の外部列に自動的にマップされ、 **[最新の情報に更新]** ボタンをクリックすると、各パラメーターの特性が定義されます。 ただし、OLE DB コマンド変換で使用する OLE DB プロバイダーが、パラメーターから取得するパラメーター情報をサポートしていない場合、外部列を手動で構成する必要があります。 つまり、外部入力に渡すパラメーターごとに列を変換に追加し、 **Param_0**などの名前が使用されるように列名を更新します。さらに、DBParamInfoFlags プロパティの値を指定し、パラメーター値を含む入力列を外部列にマップする操作が必要です。  
  
 DBParamInfoFlags の値は、パラメーターの特性を表します。 たとえば、値 **1** は、パラメーターが入力パラメーターであることを表し、値 **65** は、パラメーターが入力パラメーターであり、NULL 値を含めることができることを表します。 この値は、OLE DB DBPARAMFLAGSENUM 列挙値と一致する必要があります。 詳細については、OLE DB のリファレンス マニュアルを参照してください。  
  
 OLE DB コマンド変換には、 **SQLCommand** カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../../integration-services/expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../../integration-services/expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの標準出力、および 1 つのエラー出力をとります。  
  
## <a name="logging"></a>ログ記録  
 OLE DB コマンド変換による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、OLE DB コマンド変換による外部データ ソースへの接続およびコマンドに関するトラブルシューティングを行うことができます。 OLE DB コマンド変換による外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択する必要があります。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 変換は、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーまたはオブジェクト モデルを使用して構成できます。 プログラムによってこの変換を構成する方法の詳細については、開発者ガイドを参照してください。  
  
## <a name="configure-the-ole-db-command-transformation"></a>OLE DB コマンド変換を構成する
  OLE DB コマンド変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと、フラット ファイル ソースや OLE DB ソースなどの変換元があらかじめ含まれている必要があります。 この変換は、通常、パラメーター化クエリを実行するために使用されます。  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>OLE DB コマンド変換を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB コマンド変換をデザイン画面にドラッグします。  
  
4.  OLE DB コマンド変換をデータ フローに連結します。連結するには、緑または赤の矢印のコネクタを、データ ソースまたは前の変換から OLE DB コマンド変換にドラッグします。  
  
5.  コンポーネントを右クリックし、[編集] または **[詳細エディターの表示]** をクリックします。  
  
6.  **[接続マネージャー]** タブで、 **[接続マネージャー]** 一覧から OLE DB 接続マネージャーを選択します。 詳細については、「 [OLE DB 接続マネージャー](../../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
7.  **[コンポーネントのプロパティ]** タブをクリックし、 **[SQL コマンド]** ボックスの参照ボタン ( **[...]** ) をクリックします。  
  
8.  **[文字列値エディター]** で、各パラメーターのパラメーター マーカーとして疑問符 (?) を使用して、パラメーター化 SQL ステートメントを入力します。  
  
9. **[更新]** をクリックします。 **[更新]** をクリックすると、この変換は各パラメーターに対する列を External Columns コレクションに作成し、DBParamInfoFlags プロパティを設定します。  
  
10. **[入力プロパティと出力プロパティ]** タブをクリックします。  
  
11. **[OLE DB コマンドの入力]** を展開し、次に **[外部列]** を展開します。  
  
12. **[外部列]** 一覧に、SQL ステートメント内の各パラメーターに対する列が表示されていることを確認します。 列名は、 **Param_0**、 **Param_1**のように表示されます。  
  
     この列名は変更できません。 列名を変更すると、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] によって OLE DB コマンド変換の検証エラーが生成されます。  
  
     また、このデータ型も変更できません。 各列の DataType プロパティは、正しいデータ型に設定されます。  
  
13. **[外部列]** 一覧に列が表示されていない場合は、手動で列を追加する必要があります。  
  
    -   SQL ステートメントのパラメーターごとに、 **[列の追加]** を 1 回ずつクリックします。  
  
    -   列名を、 **Param_0**、 **Param_1**のように更新します。  
  
    -   DBParamInfoFlags プロパティの値を指定します。 この値は、OLE DB DBPARAMFLAGSENUM 列挙値と一致する必要があります。 詳細については、OLE DB のリファレンス マニュアルを参照してください。  
  
    -   データ型に応じて列のデータ型を指定し、列のコード ページ、長さ、有効桁数、および小数点以下桁数を指定します。  
  
    -   未使用のパラメーターを削除するには、 **[外部列]** でパラメーターを選択し、 **[列の削除]** をクリックします。  
  
    -   **[列マッピング]** をクリックし、 **[使用できる入力列]** 一覧の列を **[使用できる変換先列]** 一覧のパラメーターにマップします。  
  
14. **[OK]** をクリックします。  
  
15. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [データ フロー](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
