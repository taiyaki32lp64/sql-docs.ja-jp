---
title: XML 出力ファイル形式 (ssbdiagnose) |Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 414c6a08e4caaf14e55c1e05412cdb86c8658979
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986071"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>XML 出力ファイルの形式 (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **ssbdiagnose** ユーティリティは、 **-XML** スイッチを指定して実行した場合、その出力を XML ファイルとして配布します。 XML 出力ファイルでは、ヘッダー情報と、分析された [!INCLUDE[ssSB](../../includes/sssb-md.md)] の構成またはメッセージ交換で検出されたエラーが示されます。 ファイルに示されたエラーを分析して報告するためのアプリケーションを作成することができます。 また、XML ファイルを XML Notepad などの一般的な XML エディターで表示することもできます。  
  
 **ssbdiangose** の出力ファイルには、2 種類の子を持つ DiagnosticInformation ルート要素が含まれます。  
  
-   ヘッダー情報を含む Banner 要素。  
  
-   **ssbdiagnose**によって報告される各問題を示す Issue 要素。  
  
## <a name="diagnosticinformation-root-element"></a>DiagnosticInformation ルート要素 (ssbdiagnose)  
  
-   [DiagnosticInformation 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Banner 要素  
  
-   [Banner 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Issue 要素  
  
-   [Issue 要素 &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>参照  
 [ssbdiagnose ユーティリティ &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
