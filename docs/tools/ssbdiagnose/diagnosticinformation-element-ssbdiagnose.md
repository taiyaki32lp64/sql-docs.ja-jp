---
title: DiagnosticInformation 要素 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0d20ef070a390eb942b29498381da9e2479d0218
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986182"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 要素 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **DiagnosticInformation** 要素には、ユーティリティによって検出された診断情報を報告するすべての要素が含まれます。 **DiagnosticInformation** は、 **ssbdiagnostic** XML 出力ファイルのルート要素です。  
  
## <a name="syntax"></a>構文  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>要素の属性  
  
|属性|[説明]|  
|---------------|-----------------|  
|**なし**|なし|  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|[説明]|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|**ssbdiagnose** XML 出力ファイルごとに 1 つ。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[なし] :|  
|**子要素**|[Banner 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Remarks  
 XML 名前空間の詳細については、 [MSDN Library の「](https://go.microsoft.com/fwlink/?LinkId=7341) XML ドキュメントにおける名前空間 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ssbdiagnose ユーティリティ &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
