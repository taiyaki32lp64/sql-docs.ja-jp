---
title: CREATE KPI ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e2380f72fe8a5faf9dc5504e56941f724b1bd159
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098397"
---
# <a name="mdx-data-definition---create-kpi"></a>MDX データ操作 - CREATE KPI


  主要業績評価指標 (KPI) を作成します。 KPI は、キューブ内のメジャー グループに関連付けられた、ビジネスやシナリオの成功の評価に使用される計算のコレクションです。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Kpi 名*  
 KPI 名を指定する有効な文字列です。  
  
 *KPI_Value*  
 数値の値を返す有効な多次元式 (MDX) 式。  
  
 *Property_Name*  
 KPI のプロパティの名前を指定する有効な文字列。  
  
 *Property_Value*  
 KPI のプロパティの値を定義する有効なスカラー式です。  
  
## <a name="remarks"></a>コメント  
 現在接続されているキューブ以外に、キューブを指定するエラーが発生します。 そのため、現在のキューブを表すためにキューブ名の代わりに CURRENTCUBE を使用する必要があります。  
  
## <a name="kpi-properties"></a>KPI のプロパティ  
 次の表は、すべての KPI のプロパティを一覧表示します。 これらのプロパティの [なし] は、既定値を持ちます。 したがって、KPI のプロパティに特定の値が割り当てられるまで、そのプロパティに対してクエリを実行すると NULL 値が返されます。  
  
|プロパティの識別子|説明|  
|-------------------------|-------------|  
|目標|数値の値を返す有効な MDX 式です。|  
|STATUS|数値の値を返す有効な MDX 式です。|  
|STATUS_GRAPHIC|クライアント アプリケーションが使用するグラフィック イメージのセットを定義する文字列です。|  
|傾向|数値の値を返す有効な MDX 式です。|  
|TREND_GRAPHIC|クライアント アプリケーションが使用するグラフィック イメージのセットを定義する文字列です。|  
|WEIGHT|数値の値を返す有効な MDX 式です。|  
|CURRENT_TIME_MEMBER は|時間ディメンションのメンバーを返す有効な MDX 式です。 CURRENT_TIME_MEMBER は、すべての相対時間関数の参照ポイントを設定します。|  
|PARENT_KPI|親 KPI の名前を指定する文字列です。|  
|キャプション|KPI のキャプションとしてクライアント アプリケーションが使用する文字列です。|  
|DISPLAY_FOLDER|クライアント アプリケーションで表示される KPI が、表示フォルダーのパスを指定する文字列。 フォルダー レベルの区切り記号は、クライアント アプリケーションによって定義されます。 ツールおよびクライアントによって提供される[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、円記号 (\\) レベルの区切り記号です。 定義されたメンバーを複数の表示フォルダーを指定するには、セミコロン (;) を使用します。フォルダーを区切ります|  
|ASSOCIATED_MEASURE_GROUP|すべての MDX 計算で参照される必要がある、メジャー グループの名前を指定する文字列です。|  
  
 目標、状態、および傾向のプロパティの値は、-1 ~ 1 の間で評価される MDX 式です。 ただし、これらのプロパティで実際に使用される値の範囲は、クライアント アプリケーションによって定義されます。 ツールおよびクライアントによって提供されるを使用すると[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]Kpi を参照するには、-1 未満の値は-1 として処理、および 1 より大きい値は 1 として扱われます。  
  
 STATUS_GRAPHIC と TREND_GRAPHIC は、クライアント アプリケーションを表示するイメージの正しいセットを識別するために使用する文字列値です。 これらの文字列は表示関数の動作も定義します。 この動作には表示する状態の数が含まれています (通常、これは数が奇数) とそれぞれの状態を使用する画像。  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>SQL Server Data Tools での KPI グラフィック  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、KPI グラフィックが 3 または 5 つのいずれかの状態にあることができます。 次の表は、それぞれの状態の値を定義します。  
  
|KPI グラフィックの状態の数|これらの状態の値|  
|--------------------------------------|---------------------------|  
|3|悪い =-1-0.5 ~<br /><br /> -0.4999 を = OK 0.4999<br /><br /> 0\.50 ~ 1 の良い =|  
|5|悪い = -1 ～ -0.75<br /><br /> リスク-0.25 に-0.7499 を =<br /><br /> [Ok] を 0.2499-0.2499 を =<br /><br /> 上昇 = 0.25 ～ 0.7499<br /><br /> 良い = 0.75 ～ 1|  
  
> [!NOTE]  
>  反転ゲージや反転した状態の矢印などの一部のグラフィックは、範囲が反転されます。 つまり、-1 が良い評価、1 が悪い評価になります。  
  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、KPI グラフィックの名前によって、そのグラフィックの状態が 3 つであるか 5 つであるかを判断できます。 次の表に、使用法、名前、および数値の状態を[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]KPI グラフィックに関連付けます。  
  
|グラフィックの使用法|KPI グラフィックの名前|状態の数|  
|--------------------|-------------------------|----------------------|  
|状態|図形|3|  
|状態|信号機|3|  
|状態|道路標識|3|  
|状態|ゲージ|3|  
|状態|反転ゲージ|5|  
|状態|温度計|3|  
|状態|円柱|3|  
|状態|顔|3|  
|状態|変位の矢印|3|  
|傾向|標準の矢印|3|  
|傾向|状態の矢印|3|  
|傾向|反転した状態の矢印|5|  
|傾向|顔|3|  
  
## <a name="see-also"></a>関連項目  
 [DROP KPI ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [MDX データ定義ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
