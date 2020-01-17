---
title: レコードセット変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.recordsetdest.f1
helpviewer_keywords:
- Recordset destination
- ADO recordsets [Integration Services]
- destinations [Integration Services], Recordset
- in-memory ADO recordsets [Integration Services]
ms.assetid: be973cf1-c4ff-49f8-987e-314c08ef98e4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0553b1cbbd75196fa8534cf6bf64c58c1dad206b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770908"
---
# <a name="recordset-destination"></a>レコードセット変換先
  レコードセット変換先は、インメモリ ADO レコードセットを作成して設定します。 レコードセットの形態は、レコードセット変換先への入力によってデザイン時に定義されます。  
  
## <a name="configuration-of-the-recordset-destination"></a>レコードセット変換先の構成  
 レコードセット変換先を構成するには、ADO レコードセットを格納する変数を指定します。  
  
 実行時に、ADO レコードセットは、レコードセット変換先の VariableName プロパティで指定されたオブジェクト型の変数に書き込まれます。 その後、この変数はスクリプトおよび他のパッケージ要素で使用できるため、レコードセットはデータ フローの外部で利用可能になります。  
  
 この変換先は 1 つの入力をとります。 エラー出力はサポートされていません。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../common-properties.md)  
  
-   [レコードセット変換先のカスタム プロパティ](recordset-destination-custom-properties.md)  
  
 データ フロー コンポーネントのプロパティの設定方法については、「 [データ フロー コンポーネントのプロパティを設定する](set-the-properties-of-a-data-flow-component.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [レコードセット変換先を使用する](recordset-destination.md)  
  
  
