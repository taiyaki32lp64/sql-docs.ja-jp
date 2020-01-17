---
title: 既存の項目をプロジェクトに追加する| Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], item additions
- adding project items
ms.assetid: 084b3879-e96b-45a7-b421-6a4b0db2b92b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cfdc8405fd958efb34a607736648eddf5f4732dc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252837"
---
# <a name="add-existing-items-to-a-project"></a>既存の項目をプロジェクトに追加する
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
プロジェクトに新しい項目を追加して、アプリケーションの機能を拡張できます。 既存の項目は、クエリやその他のファイルです。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] には、次の 2 種類のプロジェクトがあります:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクト、Analysis Services スクリプト プロジェクト。 プロジェクトの種類によって、プロジェクトに追加できるクエリ ファイルが決まります。 たとえば、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ (拡張子が .sql のファイル) は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクトには追加できますが、Analysis Services スクリプト プロジェクトには追加できません。 プロジェクトの種類に追加のファイル拡張子を関連付ける場合は、「[ファイル拡張子をコード エディターに関連付ける方法](../../relational-databases/scripting/associate-file-extensions-to-a-code-editor.md)」をご覧ください。  
  
### <a name="to-add-an-existing-query-or-a-miscellaneous-file-to-a-project"></a>既存のクエリまたはその他のファイルをプロジェクトに追加するには  
  
1.  ソリューション エクスプローラーで、対象のプロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューの **[既存項目の追加]** をクリックします。  
  
    **Look in**  
    プロジェクトに追加するファイルまたはフォルダーをこの一覧から指定します。 XML Web サービスや ASP.NET Web アプリケーションの場合、ファイルは Web サーバーに置かれています。  
  
    **[デスクトップ]**  
    デスクトップに存在するファイルおよびフォルダーを表示します。  
  
    **[マイ プロジェクト]**  
    既定の **[マイ プロジェクト]** の場所にあるファイルとフォルダーを表示します。  
  
    **[マイ コンピューター]**  
    **[マイ コンピューター]** フォルダーの内容を表示します。  
  
    **[ファイル名]**  
    このオプションを使用すると、表示するファイルとフォルダーをフィルター選択できます。 フィルター選択するファイル名またはファイル名の一部を入力します。ワイルドカードとしてアスタリスク (`*`) を使用できます。  
  
    > [!NOTE]  
    > Web およびネットワークの場所に移動するには、 **[ファイル名]** ボックスに URL またはネットワーク パスを入力します。 たとえば、「 **`https://mywebsite`** 」と入力した場合は、"mywebsite" という Web の場所で利用可能なファイルが表示され、「 **\\\myserver\myshare**」と入力した場合は、"myserver" の "myshare" という場所で利用可能なファイルが表示されます。  
  
    **ファイルの種類**  
    ファイルの拡張子に基づいてファイルをフィルター選択するときに、このオプションを使用します。 各製品について、最も一般的なファイルの種類を対象とする既定のフィルターが一覧表示されます。  
  
    **[追加]**  
    このドロップダウン ボタンを使用すると、プロジェクトに項目を追加し、その項目を既定のエディターで開くことができます。  
  
    -   **[追加]**  
  
        既存の項目をディスク上のプロジェクト フォルダーにコピーし、その項目をソリューション エクスプローラーで選択したプロジェクトの下に追加します。 項目に加えられた変更は、元の場所の項目には反映されません。 これは、この種類のファイルの既定のエディターです。  
  
    -   **[リンクとして追加]**  
  
        選択したファイルをプロジェクトに追加し、そのファイルを、ファイルの種類に対応した既定のエディターで開きます。 このオプションでは、最初に選択したファイルが開きます。ファイルがプロジェクト フォルダーにコピーされるわけではありません。  
  
3.  クエリ ファイルを追加する場合は、接続ダイアログが表示され、クエリの接続を指定するように求められます。 クエリに接続を関連付けない場合には、接続ダイアログで **[キャンセル]** をクリックできます。  
  
4.  ファイルがプロジェクトの **[クエリ]** または **[その他]** フォルダーに追加されます。  
  
## <a name="see-also"></a>参照  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[プロジェクトへの新規項目の追加](../../ssms/solution/add-new-items-to-a-project.md)  
[アイテムやプロジェクトのクリアまたは削除](../../ssms/solution/remove-or-delete-an-item-or-project.md)  
  
