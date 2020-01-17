---
title: 挿入、更新、および削除を処理する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],processing data
ms.assetid: 13a84d21-2623-4efe-b442-4125a7a2d690
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 24ab4d509638b3195c7105602c663c04fb47a411
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771129"
---
# <a name="process-inserts-updates-and-deletes"></a>挿入、更新、および削除を処理する
  変更データの増分読み込みを実行する Integration Services パッケージのデータ フローにおいて、2 番目のタスクは、挿入、更新、および削除を分割することです。 その後、適切なコマンドを使用してそれらの変更を変換先に適用できるようになります。  
  
> [!NOTE]  
>  変更データの増分読み込みを実行するパッケージのデータ フローをデザインするための最初のタスクは、変更データを取得するクエリを実行する変換元コンポーネントを構成することです。 このコンポーネントに関する詳細については、「[変更データを取得および理解する](retrieve-and-understand-the-change-data.md)」を参照してください。 変更データの増分読み込みを実行するパッケージを作成するプロセス全体の説明については、「[変更データ キャプチャ &#40;SSIS&#41;](change-data-capture-ssis.md)」を参照してください。  
  
## <a name="associating-friendly-values-to-separate-inserts-updates-and-deletes"></a>挿入、更新、および削除を分割するための表示値の関連付け  
 変更データを取得するクエリ例では、**cdc.fn_cdc_get_net_changes_<capture_instance>** 関数が **__$operation** という名前のメタデータ列のみを返します。 このメタデータ列には、変更を行った操作を示す序数値が格納されます。  
  
> [!NOTE]  
>  **cdc.fn_cdc_get_net_changes_<capture_instance>** 関数を呼び出すクエリの詳細については、「[変更データを取得する関数を作成する](create-the-function-to-retrieve-the-change-data.md)」を参照してください。  
  
 序数値と対応する操作を照合するよりも、操作のニーモニックを使用する方が簡単です。 たとえば、'D' は削除操作、'I' は挿入操作というように簡単に表すことができます。 「 [変更データを取得する関数の作成](create-the-function-to-retrieve-the-change-data.md)」で作成したクエリ例では、序数値が新しい列に返される表示文字列値に変換されます。 次のコードのセグメントは、この変換を示しています。  
  
```  
select   
    ...  
    case __$operation  
        when 1 then 'D'  
        when 2 then 'I'  
        when 4 then 'U'  
        else null  
     end as CDC_OPERATION  
```  
  
## <a name="configuring-a-conditional-split-transformation-to-direct-inserts-updates-and-deletes"></a>挿入、更新、および削除を直接行うための条件分割変換の構成  
 変更データの行を 3 つの出力のいずれかに送信するには、条件分割変換が理想的です。 この変換では、単に各行の **CDC_OPERATION** 列の値がチェックされ、その変更が挿入、更新、または削除かどうかが判断されます。  
  
> [!NOTE]  
>  CDC_OPERATION 列には、 **__$operation** 列の数値から取得された表示文字列値が格納されています。  
  
#### <a name="to-split-inserts-updates-and-deletes-for-processing-by-using-a-conditional-split-transformation"></a>条件分割変換を使用して処理用に挿入、更新、および削除を分割するには  
  
1.  **[データ フロー]** タブで、条件分割変換を追加します。  
  
2.  OLE DB ソースの出力を条件分割変換に接続します。  
  
3.  **[条件分割変換エディター]** の下側のペインで、次の 3 行を入力して 3 つの出力を指定します。  
  
    1.  条件 `CDC_OPERATION == "I"` を指定する行を入力し、挿入した行を挿入用の出力に送信します。  
  
    2.  条件 `CDC_OPERATION == "U"` を指定する行を入力し、更新した行を更新用の出力に送信します。  
  
    3.  条件 `CDC_OPERATION == "D"` を指定する行を入力し、削除した行を削除用の出力に送信します。  
  
## <a name="next-step"></a>次の手順  
 処理用に行を分割したら、次に変更を変換先に適用します。  
  
 **次のトピック:** [変換先に変更を適用する](apply-the-changes-to-the-destination.md)  
  
## <a name="see-also"></a>参照  
 [条件分割変換](../data-flow/transformations/conditional-split-transformation.md)   
 [条件分割変換を使用してデータセットを分割する](../data-flow/transformations/split-a-dataset-by-using-the-conditional-split-transformation.md)  
  
  
