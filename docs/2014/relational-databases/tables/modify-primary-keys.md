---
title: 主キーの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying primary keys
- primary keys [SQL Server], modifying
ms.assetid: 8e2a15ba-1cd1-4408-b860-16c3ee37d635
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e9e19d6d6453acedff16e46dbd2d90d92a3b9587
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211825"
---
# <a name="modify-primary-keys"></a>主キーの変更
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して主キーを変更できます。 列の順序、インデックス名、クラスター化オプション、または FILL FACTOR を変更することで、テーブルの主キーを変更できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **主キーを変更するための方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 テーブルに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-modify-a-primary-key"></a>主キーを変更するには  
  
1.  主キーを変更するテーブルのテーブル デザイナーを開き、テーブル デザイナー内を右クリックして、ショートカット メニューの **[インデックス/キー]** をクリックします。  
  
2.  **[インデックス/キー]** ダイアログ ボックスで、 **[選択された主/一意キーまたはインデックス]** ボックスから主キー インデックスを選択します。  
  
3.  次の表の操作を完了します。  
  
    |目的|手順|  
    |--------|------------------------|  
    |主キーの名前を変更する。|**[オブジェクト名]** ボックスに新しい名前を入力します。 新しい名前が **[選択された主/一意キーまたはインデックス]** ボックスの一覧の名前と重複していないことを確認します。|  
    |クラスター化オプションを設定する。|主キーのクラスター化インデックスを作成するには、 **[CLUSTERED として作成]** を選択し、ドロップダウン リスト ボックスからオプションを選択します。 1 つのテーブルには、クラスター化インデックスを 1 つだけ作成できます。 インデックスにこのオプションを使用できない場合は、まず既存のクラスター化インデックスでこのチェック ボックスをオフにする必要があります。<br /><br /> このオプションを選択しない場合、一意の非クラスター化インデックスが作成されます。|  
    |FILL FACTOR を定義する。|**[FILL の指定]** カテゴリを展開して、 **[FILL FACTOR]** ボックスに 0 ～ 100 の整数を入力します。 Fill Factor の詳細とその使用方法については、「 [インデックスの FILL FACTOR の指定](../indexes/specify-fill-factor-for-an-index.md)」を参照してください。|  
    |列の順序を変更する。|**[列]** をクリックして、プロパティの右にある省略記号 ( **[...]** ) をクリックします。 **[インデックスの列]** ダイアログ ボックスで、主キーから列を削除します。 次に、削除した列を必要な順序で再度追加します。 **[列名]** ボックスの一覧から列名を削除するだけで、キーから列を削除できます。|  
  
4.  **[ファイル]** メニューの **[<_テーブル名_> を保存]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **主キーを変更するには**  
  
 Transact-SQL を使用して PRIMARY KEY 制約を変更するには、最初に既存の PRIMARY KEY 制約を削除してから、新しい定義を使用して再作成する必要があります。 詳細については、「 [Delete Primary Keys](delete-primary-keys.md) 」および「 [Create Primary Keys](create-primary-keys.md)」を参照してください。  
  
###  <a name="TsqlExample"></a>  
