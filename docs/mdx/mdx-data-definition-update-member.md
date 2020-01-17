---
title: UPDATE MEMBER ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 73a2bf2973d8c4f8f9bf9ac886728fb45250343f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038137"
---
# <a name="mdx-data-definition---update-member"></a>MDX データ操作 - UPDATE MEMBER


  既存の計算されるメンバーを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 メンバーを含むキューブの名前を指定する有効な文字列です。  
  
 *Member_Name*  
 既存のメンバーの名前を指定する有効な文字列です。  
  
 *MDX_Expression*  
 メンバーを更新する有効な多次元式 (MDX) 式です。  
  
 *Property_Name*  
 計算されるメンバーのプロパティの名前を指定する有効な文字列です。  
  
 *Property_Value*  
 計算されるメンバーのプロパティの値を指定する有効なスカラー式。  
  
## <a name="remarks"></a>コメント  
 UPDATE MEMBER ステートメントは、他の計算に対してこのメンバーの相対的な優先順位を維持しながら、既存の計算されるメンバーを更新します。 したがって、SOLVEORDER を変更するために UPDATE MEMBER ステートメントを使用することはできません。  
  
 キューブの MDX スクリプトでは、UPDATE MEMBER ステートメントを指定できません。  
  
 現在接続されているキューブ以外に、キューブを指定するエラーが発生します。 そのため、現在のキューブを表すためにキューブ名の代わりに CURRENTCUBE を使用する必要があります。  
  
 OLE DB によって定義されるメンバー プロパティの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="standard-properties"></a>標準的なプロパティ  
 各メンバーには、既定のプロパティのセットがあります。 次の表は、これらの既定のプロパティを一覧表示します。  
  
|プロパティの識別子|説明|  
|-------------------------|-------------|  
|FORMAT_STRING|セルの値を表示するクライアント アプリケーションが使用できる Office のスタイル書式指定文字列。|  
|表示されます。|計算されるメンバーがスキーマ行セットに表示されるかどうかを示す値。 表示では、メンバーのセットに追加できますされる計算される、 [AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md)関数。 0 以外の値は、計算されるメンバーが表示されていることを示します。 このプロパティの既定値は*Visible*します。<br /><br /> 表示されない計算されるメンバーより複雑な計算されるメンバーの途中のステップとして一般的に使用されます。 これらの計算されるメンバーは、メンバー、メジャーなどの他の種類によってにも参照できます。|  
|NON_EMPTY_BEHAVIOR|空のセルを解決する場合の計算されるメンバーの動作を決定するために MDX が使用するメジャーまたはセットです。|  
|キャプション|メンバーを表示するクライアント アプリケーションが使用されるキャプションを指定する文字列値。|  
|DISPLAY_FOLDER|クライアント アプリケーションで表示されるように、メンバーが、表示フォルダーのパスを指定する文字列値。 フォルダー レベルの区切り記号は、クライアント アプリケーションによって定義されます。 ツールおよびクライアントによって提供される[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、円記号 (\\) レベルの区切り記号として。 定義されたメンバーで複数の表示フォルダーを指定するには、セミコロン (;) を使用してフォルダーを区切ります。|  
|ASSOCIATED_MEASURE_GROUP|このメンバーが関連付けられているメジャー グループの名前です。|  
  
## <a name="see-also"></a>関連項目  
 [DROP MEMBER ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [CREATE MEMBER ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX データ定義ステートメント&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
