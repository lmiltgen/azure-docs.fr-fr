---
title: 'Résolution des problèmes : Données manquantes dans les journaux d’activité Azure Active Directory téléchargés | Microsoft Docs'
description: Fournit une résolution au problème de données manquantes dans les journaux d’activité Azure Active Directory téléchargés.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 2607c5dacf6f261f27e7805e02df189a2753404c
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51625644"
---
# <a name="i-cant-find-all-the-data-in-the-azure-active-directory-activity-logs-i-downloaded"></a>Je ne parviens pas à trouver toutes les donnée dans les journaux d’activité Azure Active Directory que j’ai téléchargés

## <a name="symptoms"></a>Symptômes

J’ai téléchargé les journaux d’activité (d’audit ou de connexion) et tous les enregistrements correspondant à la période choisie n’apparaissent pas. Pourquoi ? 

 ![Reporting](./media/troubleshoot-missing-data-download/01.png)
 
## <a name="cause"></a>Cause :

Lorsque vous téléchargez des journaux d’activité dans le portail Azure, nous limitons l’échelle à des enregistrements de 5 000 Ko, triés du plus récent au moins récent. 

## <a name="resolution"></a>Résolution :

Vous pouvez tirer parti des [API de création de rapports Azure AD](concept-reporting-api.md) pour extraire jusqu’à un million d’enregistrements pour un point donné. Nous vous recommandons [d’exécuter un script de façon planifiée](tutorial-signin-logs-download-script.md) qui appelle les API de création de rapports pour extraire des enregistrements de manière incrémentielle sur une période donnée (par exemple, quotidienne ou hebdomadaire). 

## <a name="next-steps"></a>Étapes suivantes

* [FAQ sur les rapports Azure Active Directory](reports-faq.md)

