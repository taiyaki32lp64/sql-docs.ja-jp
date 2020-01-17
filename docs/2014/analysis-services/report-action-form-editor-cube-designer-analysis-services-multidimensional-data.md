---
title: レポート アクション フォーム エディター ([アクション] タブ、キューブ デザイナー) (Analysis Services - 多次元データ) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eeb3df670097c0d511a9f5b779b6705f40a5e897
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070297"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>レポート アクション フォーム エディター (キューブ デザイナーの [アクション] タブ) (Analysis Services - 多次元データ)
  キューブ デザイナーで **[アクション]** タブの**レポート アクション フォーム エディター** ペインを使用すると、 **[アクション オーガナイザー]** ペインで選択されたレポート アクションを変更できます。  
  
## <a name="options"></a>および  
 **名前**  
 アクションの名前を入力します。  
  
 **[アクションの対象]**  
 **[対象になる種類]** オプションと **[対象になるオブジェクト]** オプションの表示を拡張します。  
  
 **ターゲットの種類**  
 アクションが関連付けられるオブジェクトの種類を選択します。 サーバーは、指定された種類のオブジェクトに適用されるアクションのみをクライアントに返します。 アクションは、 **[条件]** が一致する場合、および次の表に指定されたオブジェクトが選択された場合に、クライアントに対して使用可能になります。  
  
|値|選択されたオブジェクト|  
|-----------|---------------------|  
|[属性メンバー]|**[対象になるオブジェクト]** の属性に基づくレベルからメンバーが選択されます。<br /><br /> 注:選択した属性を使用するその他のユーザー階層は、レポート アクションを継承します。|  
|セル|**[対象になるオブジェクト]** の名前付きセットが選択されます。 キューブ内のすべてのセルを選択するには、 **[すべてのセル]** を選択します。|  
|Cube|**[対象になるオブジェクト]** のキューブが選択されます。 現在のキューブを使用するには、[CURRENTCUBE] を選択します。<br /><br /> 注:[Currentcube] を使用する場合、キューブの名前を変更することがありますまたは他のキューブにアクションがコピーされる移植性を提供します。 現在のキューブを表すために、[CURRENTCUBE] を使用することをお勧めします。|  
|[ディメンションのメンバー]|**[対象になるオブジェクト]** でディメンションのメンバーが選択されます。|  
|Hieararchy|**[対象になるオブジェクト]** で階層が選択されます。|  
|[階層メンバー]|**[対象になるオブジェクト]** で階層内のメンバーが選択されます。|  
|Level|**[対象になるオブジェクト]** でレベルが選択されます。|  
|[レベル メンバー]|**[対象になるオブジェクト]** でレベル内のメンバーが選択されます。|  
  
 **ターゲット オブジェクト**  
 アクションが関連付けられるオブジェクトを選択します。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスは、選択したオブジェクトに適用されるこれらのアクションのみをクライアントに返します。 使用可能なオブジェクトは、 **[対象になる種類]** の選択によって制限されます。  
  
 **[条件 (省略可能)]**  
 オプションの条件を記述する多次元式 (MDX) を入力します。この式は、アクションが使用可能な場合に制限を設定する **[対象になるオブジェクト]** のメンバーと一緒に使用されます。 この式は、ブール値を返す必要があります (true は、アクションが使用可能なことを示します)。  
  
 選択した要素を **[計算ツール]** ペインからこのオプションへドラッグして、選択した要素に対して MDX 構文を含めます。  
  
 **レポート サーバー**  
 **[サーバー名]** オプション、 **[サーバー パス]** オプション、および **[レポート形式]** オプションの表示を拡張します。  
  
 **サーバー名**  
 アクションがレポートを実行する [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] インスタンスの名前を入力します。  
  
 **[サーバー パス]**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] インスタンスのレポートへのパスを入力します。 たとえば、「 **Sales/YearlySalesByCategory**」と入力します。  
  
 **[レポート形式]**  
 レポートが返される形式を選択します。 次の表では、使用可能な形式について説明しています。  
  
|値|説明|  
|-----------|-----------------|  
|[HTML5]|レポートが HTML 5.0 に準拠した形式で返されます。|  
|[HTML3]|レポートが HTML 3.2 に準拠した形式で返されます。|  
|[エクスポート]|レポートが [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel ワークシート (.xls) ファイルとして返されます。|  
|PDF|レポートが Adobe Portable Document Format (.pdf) ファイルとして返されます。|  
  
 **[パラメーター (省略可能)]**  
 **[レポート]** で指定されたレポートに対してレポート パラメーターを指定することができるグリッドの表示を拡張します。 このグリッドには次の列が含まれています。  
  
|[列]|説明|  
|------------|-----------------|  
|**[パラメーター名]**|レポートに渡されるレポート パラメーターの名前を入力します。|  
|**[パラメーター値]**|レポートに渡されるレポート パラメーターの値を入力します。<br /><br /> 参照ボタン ( **[...]** ) をクリックして **[MDX ビルダー]** ダイアログ ボックスを表示し、レポート パラメーターの値を指定する MDX 式を作成します。 **[MDX ビルダー]** ダイアログ ボックスの詳細については、「[MDX ビルダー &#40;Analysis Services - 多次元データ&#41;](mdx-builder-analysis-services-multidimensional-data.md)」を参照してください。<br /><br /> パラメーターが MDX 式に設定されている場合、この MDX 式はアクションが実行されるときに評価されます。設定されていない場合は、変更されずにレポートに渡されます。|  
  
 **[追加のプロパティ]**  
 **[呼び出し]** 、 **[アプリケーション]** 、 **[説明]** 、 **[キャプション]** 、および **[キャプションに MDX を使用]** オプションの表示を拡張します。  
  
 **[呼び出し]**  
 いつアクションを実行する必要があるかを設定します。  
  
> [!NOTE]  
>  このオプションは、クライアント アプリケーションがアクションをいつ実行するかについて推奨するだけで、アクションの呼び出しを直接制御することはありません。  
  
 次の表では、使用可能な設定について説明しています。  
  
|値|説明|  
|-----------|-----------------|  
|Batch (バッチ)|アクションは、バッチ操作または [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] タスクの一部として実行する必要があります。|  
|Interactive|アクションは、ユーザーがアクションを呼び出したときに実行されます。|  
|[オープン時]|アクションは、キューブが最初に開いたときに実行されます。|  
  
 **アプリケーション**  
 **[アクションの式]** によって返される文字列を解釈できる、アプリケーションの名前を入力します。  
  
 このオプションを使用して、どのクライアント アプリケーションが最もよくこのアクションを使用するか識別したり、ポップアップ メニューのアクションの横に適切なアイコンを表示したりできます。  
  
> [!NOTE]  
>  このオプションは、どのクライアント アプリケーションがアクションを実行するかについて推奨するだけで、アクションへのアクセスを直接制御することはありません。 クライアント アプリケーションでは、他のクライアント アプリケーションに関連付けられているすべてのアクションを非表示にする必要があります。  
  
 **[説明]**  
 アクションの説明をオプションで入力します。  
  
 **Caption**  
 **[キャプションに MDX を使用]** を **[False]** に設定する場合は、クライアント アプリケーションでアクションに対して表示されるキャプションを入力します。  
  
 **[キャプションに MDX を使用]** を **[True]** に設定する場合は、キャプションの文字列を返す多次元式 (MDX) を入力します。  
  
 **キャプションに MDX**  
 クライアント アプリケーションのアクションに表示されるキャプションを表すリテラル文字列が **[キャプション]** に入力されている場合は、 **[False]** を選択します。  
  
 クライアント アプリケーションのアクションに表示されるキャプションを表す文字列を返す MDX 式が **[キャプション]** に入力されている場合は、 **[True]** を選択します。 MDX 式は、アクションがクライアント アプリケーションに返される前に解析される必要があります。  
  
## <a name="see-also"></a>参照  
 [アクション&#40;キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [ツールバー&#40;アクションタブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション オーガナイザー&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [計算ツール&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [ドリルスルー アクション フォーム エディター&#40;アクション タブ、キューブ デザイナー&#41; &#40;Analysis Services - 多次元データ&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
