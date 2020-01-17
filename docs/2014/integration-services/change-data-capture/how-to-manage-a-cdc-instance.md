---
title: CDC インスタンスを管理する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd64fe5cad5f85c41830d25dce279ba09915626b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771170"
---
# <a name="how-to-manage-a-cdc-instance"></a>How to Manage a CDC Instance
  この手順では、CDC デザイナー コンソールを使用して CDC インスタンスの操作を実行時に管理する方法について説明します。  
  
### <a name="to-manage-cdc-instance-operations"></a>CDC インスタンスの操作を管理するには  
  
1.  **[スタート]** メニューの **[CDC デザイナー コンソール]** をクリックします。  
  
2.  左側のペインで **[Change Data Capture]** を展開し、表示するインスタンスが含まれているサービスを展開します。  
  
3.  操作するインスタンスの名前を選択します。  
  
4.  CDC デザイナー コンソールの右側にある **[アクション]** ペインで、実行する操作をクリックします。  
  
     左ペインでインスタンスの名前を右クリックして、実行する操作を選択することもできます。  
  
     実行できるタスクは次のとおりです。  
  
    -   **[開始]** : 変更のキャプチャを開始します。  
  
    -   **[停止]** : 変更のキャプチャを停止します。  
  
    -   **[リセット]** : CDC インスタンスを初期 (空) の状態にリセットするには、 **[リセット]** をクリックします。 このオプションは、CDC インスタンスが停止しているときに使用できます。 変更テーブル内のすべての変更および CDC インスタンスの内部状態が削除されます。 CDC インスタンスが後から開始されると、変更キャプチャはその時点から開始され、CDC インスタンスの開始後に開始されたトランザクションのみがキャプチャの対象となります。  
  
    -   **[削除]** :CDC インスタンスを削除します。  
  
    -   **[Oracle ログ スクリプト]** : [Oracle ログ スクリプト] ダイアログ ボックスに Oracle 補足ログ スクリプトを表示するには、 **[Oracle ログ スクリプト]** をクリックします。 このダイアログ ボックスで実行できる操作の詳細については、「 [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md)」を参照してください。  
  
         **注**:補足ログ スクリプトを実行すると、[スクリプトを実行するための Oracle 資格情報] ダイアログ ボックスが表示されます。このダイアログ ボックスで、有効な Oracle ユーザー名とパスワードを指定します。 適切な Oracle 資格情報を指定する方法については、「 [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md)」を参照してください。  
  
    -   **[CDC インスタンスの配置]** : CDC インスタンスの配置スクリプトを生成します。 このダイアログ ボックスの詳細については、「 [CDC Instance Deployment Script](cdc-instance-deployment-script.md)」を参照してください。  
  
     これらの作業の詳細については、「 [Manage a CDC Instance](manage-a-cdc-instance.md)」を参照してください。  
  
 **[プロパティ]** を選択して、CDC インスタンスの構成プロパティを編集することもできます。 CDC インスタンスのプロパティの編集の詳細については、「 [Edit Instance Properties](edit-instance-properties.md)」を参照してください。  
  
  
