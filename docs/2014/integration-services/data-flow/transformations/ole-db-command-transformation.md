---
title: OLE DB コマンド変換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a8ffc33de161c71c6f72eebf8616d1e814fb994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770392"
---
# <a name="ole-db-command-transformation"></a>OLE DB コマンド変換
  OLE DB コマンド変換は、データ フローの各行に対して SQL ステートメントを実行します。 たとえば、データベース テーブル内に行を挿入したり、行を更新または削除する SQL ステートメントを実行できます。  
  
 OLE DB コマンド変換は、次の方法で構成できます。  
  
-   各行に対して変換が実行する SQL ステートメントを指定します。  
  
-   SQL ステートメントがタイムアウトになる時間を秒数で指定します。  
  
-   既定のコード ページを指定します。  
  
 通常、SQL ステートメントにはパラメーターが含まれます。 パラメーター値は変換入力内の外部列に格納され、入力列を外部列にマップすることによって、入力列をパラメーターにマップします。 たとえば、 **ProductKey** 列の値を使用し、 **DimProduct** テーブルの行を探して削除するには、 **Param_0** という名前の外部列を **ProductKey** という名前の入力列にマップし、SQL ステートメント `DELETE FROM DimProduct WHERE ProductKey = ?`を実行します。 OLE DB コマンド変換で用意されているパラメーター名は変更できません。 パラメーター名は、 **Param_0**、 **Param_1**のように指定されます。  
  
 **[詳細エディター]** ダイアログ ボックスを使用して OLE DB コマンド変換を構成する場合、SQL ステートメント内のパラメーターは変換入力内の外部列に自動的にマップされ、 **[最新の情報に更新]** ボタンをクリックすると、各パラメーターの特性が定義されます。 ただし、OLE DB コマンド変換で使用する OLE DB プロバイダーが、パラメーターから取得するパラメーター情報をサポートしていない場合、外部列を手動で構成する必要があります。 つまり、外部入力に渡すパラメーターごとに列を変換に追加し、 **Param_0**などの名前が使用されるように列名を更新します。さらに、DBParamInfoFlags プロパティの値を指定し、パラメーター値を含む入力列を外部列にマップする操作が必要です。  
  
 DBParamInfoFlags の値は、パラメーターの特性を表します。 たとえば、値 **1** は、パラメーターが入力パラメーターであることを表し、値 **65** は、パラメーターが入力パラメーターであり、NULL 値を含めることができることを表します。 この値は、OLE DB DBPARAMFLAGSENUM 列挙値と一致する必要があります。 詳細については、OLE DB のリファレンス マニュアルを参照してください。  
  
 OLE DB コマンド変換には、`SQLCommand` カスタム プロパティがあります。 このプロパティは、パッケージの読み込み時にプロパティ式で更新できます。 詳細については、「[Integration Services &#40;SSIS&#41; の式](../../expressions/integration-services-ssis-expressions.md)」、「[パッケージでプロパティ式を使用する](../../expressions/use-property-expressions-in-packages.md)」、および「[変換のカスタム プロパティ](transformation-custom-properties.md)」を参照してください。  
  
 この変換は、1 つの入力、1 つの標準出力、および 1 つのエラー出力をとります。  
  
## <a name="logging"></a>ログの記録  
 OLE DB コマンド変換による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、OLE DB コマンド変換による外部データ ソースへの接続およびコマンドに関するトラブルシューティングを行うことができます。 OLE DB コマンド変換による外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択する必要があります。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 変換は、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーまたはオブジェクト モデルを使用して構成できます。 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーを使用して変換を構成する方法については、「  [OLE DB コマンド変換を構成する](../../configure-the-ole-db-command-transformation.md)」を参照してください。 プログラムによってこの変換を構成する方法の詳細については、開発者ガイドを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データ フロー](../data-flow.md)   
 [Integration Services の変換](integration-services-transformations.md)  
  
  
