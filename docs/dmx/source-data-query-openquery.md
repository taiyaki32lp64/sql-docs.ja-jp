---
title: OPENQUERY (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: caac43eb176e17a6e92e487f3dedae71a252f5af
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887728"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;ソースデータクエリ&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  ソース データ クエリを既存のデータ ソースへのクエリで置き換えます。 INSERT、SELECT FROM 予測結合、および SELECT FROM ナチュラル予測結合ステートメントでは、 **OPENQUERY**がサポートされています。  
  
## <a name="syntax"></a>構文  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>引数  
 *名前付きデータソース*  
 データベースに[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]存在するデータソース。[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
 *クエリ構文*  
 行セットを返すクエリ構文です。  
  
## <a name="remarks"></a>コメント  
 **OPENQUERY**は、データソースのアクセス許可をサポートすることにより、外部データにアクセスするより安全な方法を提供します。 接続文字列はデータ ソースに格納されるので、管理者はデータ ソースのプロパティを使用して、データへのアクセスを管理することができます。 データソースの詳細については、「[サポート&#40;されるデータ&#41;ソース (SSAS-多次元)](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional)」を参照してください。  
  
 サーバーで使用できるデータソースの一覧を取得するには、 **MDSCHEMA_INPUT_DATASOURCES**スキーマ行セットに対してクエリを実行します。 **MDSCHEMA_INPUT_DATASOURCES**の使用方法の詳細については、「 [MDSCHEMA_INPUT_DATASOURCES Rowset](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset)」を参照してください。  
  
 また、次の DMX クエリを使用すると、現在の Analysis Services データベース内のデータ ソースの一覧を返すこともできます。  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>使用例  
 次の例では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]データベースに既に定義されている myds データソースを使用して、 [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]データベースへの接続を作成し、 **vtargetmail**ビューに対してクエリを実行します。  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>参照  
 [&#60;ソースデータクエリ&#62;](../dmx/source-data-query.md)   
 [データマイニング拡張&#40;機能&#41; DMX データ操作ステートメント](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
