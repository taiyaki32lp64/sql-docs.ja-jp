---
title: パーティション処理変換先のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dbab24f756498d7427f9961e4176249daac8dfb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770948"
---
# <a name="partition-processing-destination-custom-properties"></a>パーティション処理変換先のカスタム プロパティ
  パーティション処理変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、パーティション処理変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|説明|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスへの接続文字列。|  
|KeyDuplicate|Integer (列挙)|UseDefaultConfiguration が`False`、重複キー エラーを処理する方法を示す値。 有効な値は、`IgnoreError` (0)、`ReportAndContinue` (1)、および `ReportAndStop` (2) です。 このプロパティの既定値は `IgnoreError` (0) です。|  
|KeyErrorAction|Integer (列挙)|UseDefaultConfiguration が`False`、キーのエラーを処理する方法を示す値。 有効な値は、`ConvertToUnknown` (0) および `DiscardRecord` (1) です。 このプロパティの既定値は `ConvertToUnknown` (0) です。|  
|KeyErrorLimit|Integer|UseDefaultConfiguration が`False`、許可されているキー エラーの上限値。|  
|KeyErrorLimitAction|Integer (列挙)|UseDefaultConfiguration が`False`、ときに実行するアクションを示す値`KeyErrorLimit`に到達します。 有効な値は、`StopLogging` (1) および `StopProcessing` (0) です。 このプロパティの既定値は `StopProcessing` (0) です。|  
|KeyErrorLogFile|String|UseDefaultConfiguration が`False`、エラー ログ ファイルのパスとファイル名。|  
|KeyNotFound|Integer (列挙)|UseDefaultConfiguration が`False`、見つからないキーのエラーを処理する方法を示す値。 有効な値は、`IgnoreError` (0)、`ReportAndContinue` (1)、および `ReportAndStop` (2) です。 このプロパティの既定値は `ReportAndContinue` (1) です。|  
|NullKeyConvertedToUnknown|Integer (列挙)|UseDefaultConfiguration が`False`、不明な値に変換された null キーを処理する方法を示す値。 有効な値は、`IgnoreError` (0)、`ReportAndContinue` (1)、および `ReportAndStop` (2) です。 このプロパティの既定値は `IgnoreError` (0) です。|  
|NullKeyNotAllowed|Integer (列挙)|UseDefaultConfiguration が`False`、許容されない null の処理方法を示す値。 有効な値は、`IgnoreError` (0)、`ReportAndContinue` (1)、および `ReportAndStop` (2) です。 このプロパティの既定値は `ReportAndContinue` (1) です。|  
|ProcessType|Integer (列挙)|変換が使用するパーティション処理の種類。 有効な値は、`ProcessAdd` (1) (インクリメンタル)、`ProcessFull` (0)、および `ProcessUpdate` (2) です。|  
|UseDefaultConfiguration|ブール値|変換が既定のエラー構成を使用するかどうかを指定する値。 場合、このプロパティは`False`変換は、KeyDuplicate や具合を含めて、このテーブルに表示されているエラー処理のカスタム プロパティの値を使用します。|  
  
 パーティション処理変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [パーティション処理変換先](partition-processing-destination.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [共通プロパティ](../common-properties.md)  
  
  
