---
title: 文字マップ変換 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8211045a72ae56b04bb93b7be7e83f296f2467e5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291662"
---
# <a name="character-map-transformation"></a>文字マップ変換

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  文字マップ変換は、小文字から大文字への変換関数などの文字列関数を、文字データに適用します。 この変換は、文字列データ型の列データにのみ実行されます。  
  
 文字マップ変換では、列データを適切に変換したり、変換出力に列を追加して、変換後のデータを新しい列に挿入したりできます。 また、さまざまなマップ操作のセットを同じ入力列に適用し、その結果を別の列に格納できます。 たとえば、同じ列を大文字と小文字に変換し、その結果を 2 つの異なる列に格納できます。  
  
 状況によっては、マップによってデータが切り捨てられる場合があります。 たとえば、1 バイト文字をマルチバイトで表記される文字にマップした場合、切り捨てが発生することがあります。 文字マップ変換には 1 つのエラー出力が含まれます。このエラー出力を使用すると、切り捨てられたデータを別の出力に送ることができます。 詳しくは、「 [データのエラー処理](../../../integration-services/data-flow/error-handling-in-data.md)」をご覧ください。  
  
 この変換は、1 つの入力、1 つの出力、および 1 つのエラー出力をとります。  
  
## <a name="mapping-operations"></a>マップ操作  
 次の表では、文字マップ変換がサポートするマップ操作について説明します。  
  
|演算|[説明]|  
|---------------|-----------------|  
|バイトの反転|バイト順を反転します。|  
|全角|半角文字を全角文字にマップします。|  
|半角|全角文字を半角文字にマップします。|  
|ひらがな|カタカナをひらがなにマップします。|  
|カタカナ|ひらがなをカタカナにマップします。|  
|言語の文字種|システム規則ではなく言語の文字種を適用します。 言語の文字種は、Win32 API が提供する、チュルク語や他のロケールの Unicode 単純文字種のマップに関する機能を基準とします。|  
|小文字|文字を小文字に変換します。|  
|Simplified Chinese|繁体中国語文字を簡体中国語文字にマップします。|  
|Traditional Chinese|簡体中国語文字を繁体中国語文字にマップします。|  
|大文字|文字を大文字に変換します。|  
  
## <a name="mutually-exclusive-mapping-operations"></a>相互に排他的なマップ操作  
 変換では、複数の操作を実行できます。 ただし、一部のマップ操作は相互に排他的です。 次の表に、同じ行に対して複数の操作を行う場合に適用される制限の一覧を示します。 操作 A 列と操作 B 列の操作は、相互に排他的です。  
  
|操作 A|操作 B|  
|-----------------|-----------------|  
|小文字|大文字|  
|ひらがな|カタカナ|  
|半角|全角|  
|Traditional Chinese|Simplified Chinese|  
|小文字|ひらがな、カタカナ、半角、全角|  
|大文字|ひらがな、カタカナ、半角、全角|  
  
## <a name="configuration-of-the-character-map-transformation"></a>文字マップ変換の構成  
 文字マップ変換は、次の方法で構成できます。  
  
-   変換する列を指定します。  
  
-   各列に適用する操作を指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [変換のカスタム プロパティ](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>文字マップ変換エディター
  **[文字マップ変換エディター]** ダイアログ ボックスを使用すると、列のデータに適用する文字列関数を選択し、マッピングが埋め込み先の変更か新しい列として追加されるかを指定できます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 チェック ボックスを使用し、文字列関数を使用して変換する列を選択します。 選択は下の表に表示されます。  
  
 **入力列**  
 上の表で選択された入力列が表示されます。 使用できる入力列の一覧を使用して、選択した列を変更したり、削除したりできます。  
  
 **変換先**  
 文字列処理の結果を、既定の列を使用して所定の場所に保存するか、変更されたデータを新しい列として保存するかを指定します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|[新しい列]|データを新しい列に保存します。 **[出力の別名]** で、列名を割り当てます。|  
|[埋め込み先変更]|変更されたデータを既存の列に保存します。|  
  
 **操作**  
 列のデータに適用する文字列関数を一覧から選択します。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|小文字|小文字に変換します。|  
|大文字|大文字に変換します。|  
|バイトの反転|バイト順序を反転します。|  
|ひらがな|カタカナをひらがなに変換します。|  
|カタカナ|ひらがなをカタカナに変換します。|  
|半角|全角文字を半角文字に変換します。|  
|全角|半角文字を全角文字に変換します。|  
|言語の文字種|システムのルールではなく、言語の文字種による規則 (チュルク語などのロケールにおける Unicode の文字種の単純な割り当て) を適用します。|  
|Simplified Chinese|繁体中国語の文字を簡体中国語に変換します。|  
|Traditional Chinese|簡体中国語の文字を繁体中国語に変換します。|  
  
 **[出力の別名]**  
 各出力列の別名を入力します。 既定では、入力列の名前の後に " **のコピー** " が追加された別名になりますが、固有のわかりやすい名前を選択することもできます。  
  
 **エラー出力の構成**  
 [[エラー出力の構成]](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) ダイアログ ボックスを使用して、この変換のエラー処理オプションを指定します。  
  
  
