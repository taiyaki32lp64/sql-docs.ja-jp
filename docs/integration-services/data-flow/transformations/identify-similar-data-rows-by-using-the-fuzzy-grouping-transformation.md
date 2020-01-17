---
title: あいまいグループ化変換を使用して類似のデータ行を識別する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c47bd07fd48431f850744e58ba2838b61d5969d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291548"
---
# <a name="identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation"></a>あいまいグループ化変換を使用して類似のデータ行を識別する

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  あいまいグループ化変換を追加して構成するには、パッケージに 1 つ以上のデータ フロー タスクと 1 つの変換元があらかじめ含まれている必要があります。  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>データ フローにあいまいグループ化変換を実装するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、あいまいグループ化変換をデザイン画面にドラッグします。  
  
4.  あいまいグループ化変換をデータ フローに連結します。連結するには、データ ソースまたは直前の変換からあいまいグループ化変換にコネクタをドラッグします。  
  
5.  あいまいグループ化変換をダブルクリックします。  
  
6.  **[あいまいグループ化変換エディター]** ダイアログ ボックスの **[接続マネージャー]** タブで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに接続する OLE DB 接続マネージャーを選択します。  
  
    > [!NOTE]  
    >  この変換では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに接続し、一時テーブルおよびインデックスを作成する必要があります。  
  
7.  **[列]** タブをクリックし、 **[使用できる入力列]** 一覧で、データセット内で類似の行を識別するために使用する入力列のチェック ボックスをオンにします。  
  
8.  **[パススルー]** 列のチェック ボックスをオンにし、変換出力に渡す入力列を指定します。 パススルー列は、重複する行の識別処理には含まれません。  
  
    > [!NOTE]  
    >  グループ化で使用される入力列は、自動的にパススルー列として選択されます。この入力列は、グループ化で使用されている間は選択解除できません。  
  
9. 必要に応じて、 **[出力の別名]** 列で出力列の名前を更新します。  
  
10. 必要に応じて、 **[グループ出力の別名]** 列で、クリーンにした列の名前を更新します。  
  
    > [!NOTE]  
    >  列の既定の名前は、入力列の名前に "_clean" サフィックスが付いたものとなります。  
  
11. 必要に応じて、 **[一致の種類]** 列で、使用する一致の種類を更新します。  
  
    > [!NOTE]  
    >  少なくとも 1 列では、あいまい一致を使用する必要があります。  
  
12. **[最小類似]** 列で、最小の類似レベル列を指定します。 この値は、0 から 1 までの値である必要があります。 値が 1 に近づくほど、入力列内の値をグループ化するために必要な類似性が高くなります。 最小類似が 1 の場合は、完全一致であることを示します。  
  
13. 必要に応じて、 **[類似出力の別名]** 列で、類似列の名前を更新します。  
  
14. データ値の数値の処理を指定するには、 **[数字]** 列の値を更新します。  
  
15. 変換による列内の文字列データの比較方法を指定するには、 **[比較フラグ]** 列内にある比較オプションの既定の選択を変更します。  
  
16. **[詳細設定]** タブをクリックすると、一意の行識別子 (_key_in)、重複の行識別子 (_key_out)、および類似値 (_score) の出力に、変換が追加する列の名前を変更できます。  
  
17. 必要に応じて、スライダー バーを移動して類似のしきい値を調整します。  
  
18. 必要に応じて、データ内の区切り記号を無視するように、トークン区切り記号のチェック ボックスをオフにします。  
  
19. **[OK]** をクリックします。  
  
20. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Fuzzy Grouping Transformation](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Integration Services の変換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services のパス](../../../integration-services/data-flow/integration-services-paths.md)   
 [[データ フロー タスク]](../../../integration-services/control-flow/data-flow-task.md)  
  
  
