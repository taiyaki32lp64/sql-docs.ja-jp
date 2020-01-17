---
title: 通知 (ストレージのオプション ダイアログ ボックス) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23845118c4c202db781fe325c4afc2402ceee271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072203"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>[通知] ([ストレージのオプション] ダイアログ ボックス) (Analysis Services - 多次元データ)
  **の** [ストレージのオプション] **ダイアログ ボックスの** [通知] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] タブを使用すると、ディメンション、キューブ、メジャー グループ、またはパーティションの通知方法およびそれに関連する設定を行うことができます。  
  
> [!NOTE]  
>  これらの設定を変更する前に、ストレージ モードおよびプロアクティブ キャッシュの機能について理解しておく必要があります。 詳細については、「[プロアクティブ キャッシュ &#40;パーティション&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)」をご覧ください。  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**ストレージ モード**|オブジェクトで使用するストレージ モードを選択します。<br /><br /> **MOLAP**<br /> 多次元 OLAP (MOLAP) ストレージが使用されます。<br /><br /> **HOLAP**<br /> ハイブリッド OLAP (HOLAP) ストレージが使用されます。<br /><br /> **ROLAP**<br /> リレーショナル OLAP (ROLAP) ストレージが使用されます。|  
|**プロアクティブ キャッシュを有効にします。**|プロアクティブ キャッシュを有効にします。<br /><br /> 注:除くすべてのオプション、このオプションが選択されていない場合**ストレージ モード**は無効になります。|  
|**SQL Server**|[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の特殊なトレース機構を使用して、オブジェクトの基になるテーブルに加えられた変更を識別します。|  
|**追跡テーブルを指定します。**|オブジェクトに関して追跡する基底のテーブルを指定した後、セミコロン (;) で区切ったテーブルの一覧を入力するか、参照ボタン ( **[...]** ) をクリックして **[リレーショナル オブジェクト]** ダイアログ ボックスを開き、追跡するテーブルを選択します。 詳細については、「[[リレーショナル オブジェクト] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。<br /><br /> このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、特定の条件が満たされたときに、追跡する基底のテーブルの一覧を取得しようとします。 これらの要件の詳細については、「[プロアクティブ キャッシュ &#40;パーティション&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)」をご覧ください。|  
|**開始したクライアント**|選択すると、XML for Analysis (XMLA) コマンドの `NotifyTableChange` を使用して、オブジェクトの基底のテーブルに加えられた変更を識別できます。 通常、クライアント ベースの通知プロセスを使用する場合は、このオプションを選択します。|  
|**追跡テーブルを指定します。**|選択した場合は、オブジェクトに関して追跡する基底のテーブルを指定した後、セミコロン (;) で区切ったテーブルの一覧を入力するか、参照ボタン ( **[...]** ) をクリックして **[リレーショナル オブジェクト]** ダイアログ ボックスを開き、追跡するテーブルを選択します。 詳細については、「[[リレーショナル オブジェクト] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](relational-objects-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。<br /><br /> このオプションが選択されていない場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、特定の条件が満たされたときに、追跡する基底のテーブルの一覧を取得しようとします。 これらの要件の詳細については、「[プロアクティブ キャッシュ &#40;パーティション&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)」をご覧ください。|  
|**定期ポーリング**|ポーリング機構を使用してオブジェクトの基底のテーブルに対して一連のクエリを実行することにより、変更を識別します。|  
|**[ポーリング間隔]**|ポーリング グリッドに定義されたポーリング クエリおよび処理クエリを実行する前に、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] が待機する時間とその時間単位を指定します。|  
|**増分更新を有効にします。**|追加データだけを識別するように設計されたポーリング クエリと処理クエリのセットに基づいて、オブジェクトの MOLAP キャッシュを増分更新します。 このオプションを選択した場合、ポーリング クエリがデータ ソース ビュー内のテーブル識別子に関連付けられます。 次に、処理クエリによって、ポーリング クエリの現在の値と、以前に実行されたポーリング クエリの格納値とが比較され、変更が識別されます。<br /><br /> このオプションが選択されていない場合、MOLAP キャッシュは完全更新されます。 その場合、変更が発生したことを識別するためにポーリング クエリが使用されます。処理クエリまたはテーブル識別子は必要ありません。|  
|**ポーリング グリッド**|データ ソースをポーリングしたり、オブジェクトの基底のテーブルに対する変更を識別したりするために [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] によって使用されるポーリング クエリ、処理クエリ、およびテーブル識別子が格納されます。 このグリッドには次の列が含まれています。<br /><br /> **ポーリング クエリ**:オブジェクトの変更を識別するためにポーリング間隔で実行される単一クエリを入力します。または、参照ボタン ( **[...]** ) をクリックして **[ポーリング クエリの作成]** ダイアログ ボックスを開き、単一クエリを定義します。 詳細については、「[[ポーリング クエリの作成] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](create-polling-query-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。 **[増分更新を有効にする]** を選択した場合、ポーリング クエリの結果として、 **[テーブル]** に定義されているテーブルに追加された最後のレコードを識別する値が返されます。 **[増分更新を有効にする]** が選択されていない場合、ポーリング クエリの結果として、テーブル内の現在のレコード数を識別する値が返されます。<br /><br /> **処理クエリ**: **[テーブル]** に識別されているテーブルから新しいレコードを取得するためにポーリング間隔で実行されるクエリを入力します。または、参照ボタン ( **[...]** ) をクリックして **[処理クエリの作成]** ダイアログ ボックスを開き、クエリを定義します。 詳細については、「[[処理クエリの作成] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](create-processing-query-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。 クエリでは、によって返される 2 つのパラメーターの前値を受け入れるように、クエリはパラメーター化する必要があります**ポーリング クエリ**と現在の値でクエリによって返される**ポーリング クエリ**に使用することができます識別し、ポーリング期間中に追加されたレコードのみを抽出します。 なお、このオプションは、 **[増分更新を有効にする]** が選択されている場合にのみ有効です。<br /><br /> **テーブル**: **[ポーリング クエリ]** のクエリで最後のレコードを追跡する場合に対象とするテーブルの識別子を入力します。または、参照ボタン ( **[...]** ) をクリックして **[テーブルの検索]** ダイアログ ボックスを開き、テーブルを選択します。 詳細については、「[[テーブルの検索] ダイアログ ボックス &#40;Analysis Services - 多次元データ&#41;](find-table-dialog-box-analysis-services-multidimensional-data.md)」をご覧ください。|  
  
## <a name="see-also"></a>参照  
 [ストレージのオプション ダイアログ ボックス&#40;Analysis Services - 多次元データ&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
