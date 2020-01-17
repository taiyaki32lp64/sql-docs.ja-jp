---
title: '[操作を実行しています] (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.performingoperation.f1
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 22f9918800930be9534441d2bb3706ad7844e9f7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285366"
---
# <a name="performing-operation-sql-server-import-and-export-wizard"></a>[操作を実行しています] (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


ウィザードで行った選択を見直して **[ウィザードを完了する]** ページで **[完了]** をクリックすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードに **[操作を実行しています]** と表示されます。 このページでは、前のページで構成した操作の進行状況と結果を確認できます。 このページでいかなる操作も必要はありません。

## <a name="screen-shot---operation-in-progress"></a>スクリーン ショット - 実行中の操作 
 次のスクリーンショットは、操作がまだ進行中の間に表示されるウィザードの **[操作を実行しています]** ページを示します。  
  
 ![インポートおよびエクスポート ウィザードの[操作を実行しています] ページ](../../integration-services/import-export-data/media/performing-operation1.png "インポートおよびエクスポート ウィザードの [操作を実行しています] ページ")  

## <a name="screen-shot---operation-completed"></a>スクリーン ショット - 操作の完了 
 次のスクリーンショットは、操作が完了した後に表示されるウィザードの **[操作を実行しています]** ページを示します。 **[メッセージ]** 列のアイテムをクリックすると、対応する手順の詳細が表示されます。  
  
 ![インポートおよびエクスポート ウィザードの[操作を実行しています] ページ](../../integration-services/import-export-data/media/performing-operation2.png "インポートおよびエクスポート ウィザードの [操作を実行しています] ページ")  
  
## <a name="watch-the-progress-of-the-operation"></a>操作の進行状況を確認する
 **操作**  
 操作の各手順が表示されます。  
  
 **ステータス**  
 各手順が成功したか、失敗したかを表示します。  
  
 **メッセージ**  
 手順に関する情報メッセージおよびエラー メッセージが表示されます。 この列のアイテムをクリックすると、対応する手順の詳細が表示されます。

## <a name="interrupt-the-operation-or-save-the-results"></a>操作を中断するか結果を保存する
 **停止**  
 必要に応じて、 **[停止]** ボタンをクリックして操作を中断できます。  
  
 **レポート**  
 結果レポートを表示したり、ファイルに保存することができます。さらに、レポートをクリップボードにコピーすることも、電子メールで送信することもできます。  
  
## <a name="whats-next"></a>次の操作  
 構成した操作が正常に実行されて完了したら、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの実行は終了です。  
-   操作をすぐに実行した場合は、選択したコピー先を開いてウィザードがコピーしたデータを確認できます。  
-   ウィザードによって作成された SSIS パッケージを保存した場合は、それを SQL Server Data Tools で開いてカスタマイズし、再利用できます。 保存されたパッケージをカスタマイズし、後でもう一度実行する方法の詳細については、 [SSIS パッケージの保存](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)に関するページを参照してください。

## <a name="see-also"></a>参照
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


