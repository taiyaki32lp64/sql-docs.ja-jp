---
title: 日付テーブルとしてマーク (SSAS テーブル) のタイム インテリジェンスで使用するための指定 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27a03aaf94d518caa6b649b7ccd826e08798dacb
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284884"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a>タイム インテリジェンスで使用する [日付テーブルとしてマーク] の指定 (SSAS テーブル)
  DAX 数式のタイム インテリジェンス機能を使用するには、日付テーブルと Date データ型の一意の識別子 (datetime) の列を指定する必要があります。 日付テーブルの列が一意の識別子として指定されている場合は、日付テーブル内の列と任意のファクト テーブルのリレーションシップを作成できます。  
  
 タイム インテリジェンス機能を使用する場合、次のルールが適用されます。  
  
-   DAX タイム インテリジェンス機能を使用する場合は、ファクト テーブルから datetime 列を指定しない。 1 つ以上の datetime 列 (Date データ型で、一意の値を持つ) を含む独立した日付テーブルをモデル内に必ず作成する。  
  
-   日付テーブルの日付の範囲が連続している。  
  
-   日付テーブル内の datetime 列の粒度は日単位 (1 日未満の時間を含まない) にする。  
  
-   **[日付テーブルとしてマーク]** ダイアログ ボックスを使用して、日付テーブルと一意識別子列を指定する必要がある。  
  
-   日付テーブル内の Date データ型の列とファクト テーブルの間にリレーションシップを作成する。  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>日付テーブルと一意識別子を指定するには  
  
1.  モデル デザイナーで、日付テーブルをクリックします。  
  
2.  **[テーブル]** メニュー、 **[日付]** 、 **Mark as [日付] [テーブル]** の順にクリックします。  
  
3.  **[日付テーブルとしてマーク]** ダイアログ ボックスの **[日付]** ボックスの一覧で、一意識別子として使用する列を選択します。 この列は、一意の値を含んでいる必要があり、Date データ型である必要があります。 例 :  
  
    |date|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  必要に応じて、ファクト テーブルと日付テーブルの間のリレーションシップを作成します。  
  
## <a name="see-also"></a>参照  
 [計算 (SSAS テーブル)](calculations-ssas-tabular.md)   
 [タイム インテリジェンス関数&#40;DAX&#41;](/dax/time-intelligence-functions-dax)  
  
  
