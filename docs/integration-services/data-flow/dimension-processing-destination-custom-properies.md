---
title: ディメンション処理変換先のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f46acb401bf04e9b0445c452e26d69de42a2d94
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292826"
---
# <a name="dimension-processing-destination-custom-properies"></a>ディメンション処理変換先のカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ディメンション処理変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、ディメンション処理変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ|データ型|[説明]|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] プロジェクトへの接続文字列。|  
|KeyDuplicate|Integer (列挙)|UseDefaultConfiguration が **False**の場合、重複キー エラーの処理方法を示す値。 指定できる値は **IgnoreError** (0)、 **ReportAndContinue** (1)、 **ReportAndStop** (2) です。 このプロパティの既定値は **IgnoreError** (0) です。|  
|KeyErrorAction|Integer (列挙)|UseDefaultConfiguration が **False**である場合に、キー エラーを処理する方法を示す値。 指定できる値は **ConvertToUnknown** (0) と **DiscardRecord** (1) です。 このプロパティの既定値は **ConvertToUnknown** (0) です。|  
|KeyErrorLimit|Integer|UseDefaultConfiguration が **False**である場合に有効になるキー エラーの数の上限。|  
|KeyErrorLimitAction|Integer (列挙)|UseDefaultConfiguration が **False**である場合、 **KeyErrorLimit** に到達したときに実行するアクションを示す値。 指定できる値は **StopLogging** (1) と **StopProcessing** (0) です。 このプロパティの既定値は **StopProcessing** (0) です。|  
|KeyErrorLogFile|String|UseDefaultConfiguration が **False**である場合、エラー ログ ファイルのパスとファイル名。|  
|KeyNotFound|Integer (列挙)|UseDefaultConfiguration が **False**である場合、見つからないキーのエラーを処理する方法を示す値。 指定できる値は **IgnoreError** (0)、 **ReportAndContinue** (1)、 **ReportAndStop** (2) です。 このプロパティの既定値は **IgnoreError** (0) です。|  
|NullKeyConvertedToUnknown|Integer (列挙)|UseDefaultConfiguration が **False**の場合、不明な値に変換された NULL キーの処理方法を示す値。 指定できる値は **IgnoreError** (0)、 **ReportAndContinue** (1)、 **ReportAndStop** (2) です。 このプロパティの既定値は **IgnoreError** (0) です。|  
|NullKeyNotAllowed|Integer (列挙)|UseDefaultConfiguration が **False**である場合、許容されない NULL を処理する方法を示す値。 指定できる値は **IgnoreError** (0)、 **ReportAndContinue** (1)、 **ReportAndStop** (2) です。 このプロパティの既定値は **IgnoreError** (0) です。|  
|ProcessType|Integer (列挙)|変換が使用するディメンション処理の種類。 値は **ProcessAdd** (1) (インクリメンタル)、 **ProcessFull** (0)、 **ProcessUpdate** (2) です。|  
|UseDefaultConfiguration|Boolean|変換が既定のエラー構成を使用するかどうかを指定する値。 このプロパティが **False**の場合、変換にはエラー処理に関する情報が含まれます。|  
  
 ディメンション処理変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [ディメンション処理変換先](../../integration-services/data-flow/dimension-processing-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
