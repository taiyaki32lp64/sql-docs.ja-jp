---
title: クエリ パラメーターをデータ フロー コンポーネントの変数にマップする | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92caab2b0631c80403c7367aeb98ae001a5e11eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901634"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>クエリ パラメーターをデータ フロー コンポーネントの変数にマップする
  パラメーター化クエリを使用するように OLE DB ソースを構成すると、パラメーターを変数にマップすることができます。  
  
 OLE DB ソースは、データ ソースに接続する際に、パラメーター化クエリを使用してデータのフィルター選択を行うことができます。  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>クエリ パラメーターを変数にマップするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[データ フロー]** タブをクリックし、次に **[ツールボックス]** で、OLE DB ソースをデザイン画面にドラッグします。  
  
4.  OLE DB ソースを右クリックし、 **[編集]** をクリックします。  
  
5.  **[OLE DB ソース エディター]** で、OLE DB 接続マネージャーを選択してデータ ソースへの接続に使用するか、 **[新規作成]** をクリックして新しい OLE DB 接続マネージャーを作成します。  
  
6.  データ アクセス モードの **[SQL コマンド]** オプションをクリックし、 **[SQL コマンド テキスト]** ペインにパラメーター化クエリを入力します。  
  
7.  **[パラメーター]** をクリックします。  
  
8.  **[クエリ パラメーターの設定]** ダイアログ ボックスで、 **[パラメーター]** 一覧にある各パラメーターを、 **[変数]** 一覧の変数にマップするか、 **[\<新しい変数>]** をクリックして新しい変数を作成します。 **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  マッピングで使用できる変数は、パッケージのスコープ内、Foreach ループなどの親コンテナーのスコープ内、またはデータ フロー コンポーネントが含まれるデータ フロー タスクのスコープ内にある、システム変数およびユーザー定義変数だけです。 変数のデータ型は、パラメーターが割り当てられる WHERE 句の列と互換性がある必要があります。  
  
9. **[プレビュー]** をクリックすると、クエリが返すデータを最大 200 行表示できます。  
  
10. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [OLE DB ソース](ole-db-source.md)   
 [参照変換](transformations/lookup-transformation.md)  
  
  
