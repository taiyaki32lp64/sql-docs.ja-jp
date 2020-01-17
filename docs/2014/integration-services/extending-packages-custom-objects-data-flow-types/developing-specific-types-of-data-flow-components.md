---
title: 特定の種類のデータ フロー コンポーネントの開発 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78810a0599d2345770175bc0ed9bdc06f3195817
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896334"
---
# <a name="developing-specific-types-of-data-flow-components"></a>特定の種類のデータ フロー コンポーネントの開発
  このセクションでは、変換元コンポーネント、同期出力型変換コンポーネント、非同期出力型変換コンポーネント、および変換先コンポーネントの開発の詳細について説明します。  
  
 コンポーネント開発全般の詳細については、「[カスタム データ フロー コンポーネントの開発](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [カスタム変換元コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 外部データ ソースのデータにアクセスし、そのデータをデータ フローの下流コンポーネントに提供するコンポーネントの開発について説明します。  
  
 [同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 入力に同期して出力する変換コンポーネントの開発について説明します。 これらのコンポーネントは、データ フローにデータを追加せず、データが渡されるたびに処理を行います。  
  
 [非同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 出力が入力に同期しない変換コンポーネントの開発について説明します。 これらのコンポーネントは、上流コンポーネントからデータを受け取ると共に、データをデータ フローに追加します。  
  
 [カスタム変換先コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 データ フローの上流コンポーネントから行を受け取り、外部データ ソースに書き込むコンポーネントの開発について説明します。  
  
## <a name="reference"></a>リファレンス  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 カスタム データ フロー コンポーネントを作成するために使用するクラスやインターフェイスが含まれています。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 データ フロー タスクのアンマネージ クラスやアンマネージ インターフェイスを示します。 プログラムによってデータ フローを構築する場合、またはカスタム データ フロー コンポーネントを作成する場合、開発者はこれらを使用します。また、マネージド <xref:Microsoft.SqlServer.Dts.Pipeline> 名前空間も同じ目的で使用されます。  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [スクリプティング ソリューションとカスタム オブジェクトとの比較](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [特定の種類のスクリプト コンポーネントの開発](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
