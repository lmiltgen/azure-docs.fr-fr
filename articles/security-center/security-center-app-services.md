---
title: Protection d’App Services dans Azure Security Center | Microsoft Docs
description: Cet article a pour but de vous aider à vous familiariser avec la protection de vos App Services dans Azure Security Center.
services: security-center
documentationcenter: na
author: rkarlin
manager: mbaldwin
editor: ''
ms.assetid: e8518710-fcf9-44a8-ae4b-8200dfcded1a
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: rkarlin
ms.openlocfilehash: 062d3ce75372cd09e617fb984208542a31cb8e4a
ms.sourcegitcommit: 00dd50f9528ff6a049a3c5f4abb2f691bf0b355a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51019775"
---
# <a name="protect-app-service-with-azure-security-center"></a>Protéger App Service avec Azure Security Center
Cet article vous aide à utiliser Azure Security Center pour surveiller et protéger vos applications s’exécutant au-dessus d’App Service.

App Service vous permet de créer et d’héberger des applications web dans le langage de programmation de votre choix sans gérer l’infrastructure. App Service offre une mise à l’échelle automatique et une haute disponibilité, une prise en charge de Windows et Linux, ainsi que déploiements automatisés à partir de GitHub, de Visual Studio Team Services ou de tout dépôt Git. 

Les vulnérabilités des applications web sont fréquemment exploitées par des attaquants, car elles présentent une interface commune et dynamique pour pratiquement toutes les organisations sur Internet. Les demandes adressées aux applications s’exécutant par dessus App Service passent par plusieurs passerelles déployées dans des centres de données Azure dans le monde entier, responsables du routage de chaque demande vers son application correspondante. 

Azure Security Center peut générer des évaluations et des suggestions sur vos applications s’exécutant dans App Service au sein de bacs à sable à l’intérieur de votre machine virtuelle ou d’instances à la demande. En tirant parti de la visibilité dont Azure dispose en tant que fournisseur de cloud, Security Center analyse vos journaux internes d’App Service pour surveiller les attaques d’applications web courantes qui sont souvent dirigées contre plusieurs cibles.

Security Center profite de l’échelle du cloud pour détecter les attaques dirigées contre vos applications App Service et se concentrer sur les attaques émergentes, lorsque les pirates sont en phase de reconnaissance et analysent les vulnérabilités de multiples sites web hébergés sur Azure. Security Center se sert d’analyses et de modèles d’apprentissage pour couvrir toutes les interfaces permettant aux clients d’interagir avec leurs applications, que ce soit via le protocole HTTP ou des méthodes de gestion. De plus, en tant que service principal dans Azure, Security Center occupe également dans une position privilégiée pour proposer des analyses de sécurité basées sur l’hôte, couvrant des nœuds de calcul sous-jacents pour ce PaaS, ce qui permet à Security Center de détecter les attaques dirigées contre des applications web qui ont déjà été exploitées.

## <a name="prerequisites"></a>Prérequis

Pour surveiller et sécuriser votre App Service, vous devez disposer d’un plan App Service associé à des machines dédiées. Il s’agit des plans suivants : De base, Standard, Premium, Isolé ou Linux. Azure Security Center ne prend pas en charge les plans Gratuit, Partagé ou Consommation. Pour plus d’informations, voir [Plans App Service](https://azure.microsoft.com/pricing/details/app-service/plans/).

## <a name="security-center-protection"></a>Protection de Azure Security Center

Azure Security Center protège l’instance de machine virtuelle dans laquelle votre App Service s’exécute et l’interface de gestion. Il surveille également les demandes et réponses échangées avec vos applications s’exécutant dans App Service.

Security Center étant intégré en mode natif avec App Service, aucun déploiement ou intégration ne sont nécessaires. L’intégration est complètement transparente.



## <a name="enabling-monitoring-and-protection-of-app-service"></a>Activation de la surveillance et la protection d’App Service

1. Dans Azure, choisissez le Security Center.
2. Accédez à **Stratégie de sécurité**, puis choisissez un abonnement.
3. À la fin de la ligne de l’abonnement, cliquez sur **Modifier les paramètres**.
4. Sous **Niveau tarifaire**, dans la ligne **App Service**, définissez votre plan sur **Activé**.

![activation/désactivation d’app service](./media/security-center-app-services/app-services-toggle.png)

>[!NOTE]
> Le nombre d’instances répertoriées pour votre quantité de ressources est le nombre d’instances pertinentes d’App Service actives lorsque vous avez ouvert le panneau du niveau tarifaire. Étant donné que ce nombre peut varier en fonction des options de mise à l’échelle sélectionnées, le nombre d’instances qui vous sont facturées est modifié en conséquence.

Pour désactiver la surveillance et les suggestions pour votre App Service, répétez ce processus et définissez votre plan **App Service** sur **Désactivé**.



## <a name="see-also"></a>Voir aussi
Dans cet article, vous avez vu comment utiliser les fonctionnalités de surveillance d’Azure Security Center. Pour plus d’informations sur le Centre de sécurité Azure, consultez les rubriques suivantes :

* [Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des paramètres de sécurité dans Azure Security Center.
* [Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.
* [Surveillance des solutions partenaires avec Azure Security Center](security-center-partner-solutions.md) : découvrez comment surveiller l’état d’intégrité de vos solutions partenaires.
* [FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.
