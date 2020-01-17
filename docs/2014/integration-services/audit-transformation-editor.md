---
title: 監査変換エディター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.audittransformation.f1
helpviewer_keywords:
- Audit Transformation Editor
ms.assetid: 32786a34-5870-4fde-83c7-ec74d62404b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9d31f297b9544c75e416fe798facd6a1c328ff0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061416"
---
# <a name="audit-transformation-editor"></a>監査変換エディター
  監査変換により、パッケージが実行される環境に関するデータをパッケージ内のデータ フローに含めることができます。 たとえば、パッケージ、コンピューター、および演算子の名前をデータ フローに追加できます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、この情報を提供するシステム変数が含まれています。  
  
 監査変換の詳細については、「 [Audit Transformation](data-flow/transformations/audit-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[出力列の名前]**  
 監査情報を格納する、新しい出力列の名前を入力します。  
  
 **[監査の種類]**  
 監査情報を得るために使用できるシステム変数を選択します。  
  
|値|説明|  
|-----------|-----------------|  
|**[実行インスタンスの GUID]**|パッケージの実行インスタンスを個別に識別する GUID を挿入します。|  
|**[パッケージ ID]**|パッケージを個別に識別する GUID を挿入します。|  
|**パッケージ名**|パッケージ名を挿入します。|  
|**[バージョン ID]**|パッケージのバージョンを個別に識別する GUID を挿入します。|  
|**[実行開始時刻]**|パッケージの実行が開始される時刻を挿入します。|  
|**コンピューター名**|パッケージを起動したコンピューターの名前を挿入します。|  
|**ユーザー名**|パッケージを起動したユーザーのログイン名を挿入します。|  
|**[タスク名]**|監査変換が関連付けられているデータ フロー タスクの名前を挿入します。|  
|**[タスク ID]**|監査変換が関連付けられているデータ フロー タスクを個別に識別する GUID を挿入します。|  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
