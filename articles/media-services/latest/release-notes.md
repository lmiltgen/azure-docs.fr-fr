---
title: Notes de publication Azure Media Services v3 | Microsoft Docs
description: Pour vous informer des développements les plus récents, cet article détaille les toutes dernières mises à jour concernant Azure Media Services v3.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 11/09/2018
ms.author: juliako
ms.openlocfilehash: 70a3de35f6fd942bca5355db3a7c6b57aec6adbc
ms.sourcegitcommit: b62f138cc477d2bd7e658488aff8e9a5dd24d577
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51613934"
---
# <a name="azure-media-services-v3-release-notes"></a>Notes de publication Azure Media Services v3 

Pour vous informer des développements les plus récents, cet article détaille les thèmes suivants :

* Versions les plus récentes
* Problèmes connus
* Résolution des bogues
* Fonctionnalités dépréciées
* Modifications planifiées

## <a name="november-2018"></a>Novembre 2018

Le module CLI 2.0 est désormais disponible pour [Azure Media Services v3 GA](https://docs.microsoft.com/cli/azure/ams?view=azure-cli-latest) – v 2.0.50.

### <a name="new-commands"></a>Nouvelles commandes

- [az ams account](https://docs.microsoft.com/cli/azure/ams/account?view=azure-cli-latest)
- [az ams account-filter](https://docs.microsoft.com/cli/azure/ams/account-filter?view=azure-cli-latest)
- [az ams asset](https://docs.microsoft.com/cli/azure/ams/asset?view=azure-cli-latest)
- [az ams asset-filter](https://docs.microsoft.com/cli/azure/ams/asset-filter?view=azure-cli-latest)
- [az ams content-key-policy](https://docs.microsoft.com/cli/azure/ams/content-key-policy?view=azure-cli-latest)
- [az ams job](https://docs.microsoft.com/cli/azure/ams/job?view=azure-cli-latest)
- [az ams live-event](https://docs.microsoft.com/cli/azure/ams/live-event?view=azure-cli-latest)
- [az ams live-output](https://docs.microsoft.com/cli/azure/ams/live-output?view=azure-cli-latest)
- [az ams streaming-endpoint](https://docs.microsoft.com/cli/azure/ams/streaming-endpoint?view=azure-cli-latest)
- [az ams streaming-locator](https://docs.microsoft.com/cli/azure/ams/streaming-locator?view=azure-cli-latest)
- [az ams account mru](https://docs.microsoft.com/cli/azure/ams/account/mru?view=azure-cli-latest) : vous permet de gérer les unités réservées Multimédia

### <a name="new-features-and-breaking-changes"></a>Nouvelles fonctionnalités et dernières modifications

#### <a name="asset-commands"></a>Commandes des éléments multimédia

- Les arguments ```--storage-account``` et ```--container``` ont été ajoutés.
- Les valeurs par défaut pour le délai d’expiration (présent + 23h) et les autorisations (lecture) dans la commande ```az ams asset get-sas-url``` ont été ajoutées.

#### <a name="job-commands"></a>Commandes des tâches

- Les arguments ```--correlation-data``` et ```--label``` ont été ajoutés.
- ```--output-asset-names``` a été renommé en ```--output-assets```. Il accepte désormais une liste de ressources séparée par des espaces au format « assetName=label ». Une ressource sans étiquette peut être envoyée comme ceci : « assetName= ».

#### <a name="streaming-locator-commands"></a>Commandes du localisateur de diffusion en continu

- La commande de base ```az ams streaming locator``` a été remplacée par ```az ams streaming-locator```.
- Les arguments ```--streaming-locator-id``` et ```--alternative-media-id support``` ont été ajoutés.
- L'argument ```--content-keys argument``` a été mis à jour.
- ```--content-policy-name``` a été renommé en ```--content-key-policy-name```.

#### <a name="streaming-policy-commands"></a>Commandes des stratégies de diffusion en continu

- La commande de base ```az ams streaming policy``` a été remplacée par ```az ams streaming-policy```.
- La prise en charge des paramètres de chiffrement dans ```az ams streaming-policy create``` a été ajoutée.

#### <a name="transform-commands"></a>Commandes de transformation

- L'argument ```--preset-names``` a été remplacé par ```--preset```. À présent vous ne pouvez définir qu’une sortie/présélection à la fois (pour en ajouter d’autres, vous devez exécuter ```az ams transform output add```). En outre, vous pouvez définir StandardEncoderPreset de façon personnalisée en transmettant le chemin à votre JSON personnalisé.
- ```az ams transform output remove``` désormais possible en transmettant le chemin de l’index pour le supprimer.
- Les arguments ```--relative-priority, --on-error, --audio-language and --insights-to-extract``` ont été ajoutés dans les commandes ```az ams transform create``` et ```az ams transform output add```.

## <a name="october-2018---ga"></a>Octobre 2018 - Mise à la disposition générale

Cette section décrit les mises à jour d’octobre d’Azure Media Services (AMS).

### <a name="rest-v3-ga-release"></a>Version en disponibilité générale de REST v3

La [version en disponibilité générale de REST v3](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01) contient davantage d’API pour les filtres de manifeste de niveau En direct, Compte/Élément multimédia, ainsi qu’une prise en charge de DRM.

#### <a name="azure-resource-management"></a>Gestion des ressources Azure 

La prise en charge de la gestion des ressources Azure permet l’unification des API de gestion et des opérations (désormais tout se trouve à un même emplacement).

À partir de cette version, vous pouvez utiliser des modèles Resource Manager pour créer des événements en direct.

#### <a name="improvement-of-asset-operations"></a>Amélioration des opérations sur les éléments multimédias 

Voici les améliorations qui ont été apportées :

- Ingestion à partir d’URL HTTP(s) ou d’URL SAP de Stockage Blob Azure.
- Possibilité de spécifier des noms de conteneurs personnalisés pour les éléments multimédias. 
- Meilleure prise en charge de la sortie pour créer des flux de travail personnalisés avec Azure Functions.

#### <a name="new-transform-object"></a>Nouvel objet Transform

Le nouvel objet **Transform** simplifie le modèle d’encodage. Le nouvel objet facilite la création et le partage de modèles et de préréglages Resource Manager d’encodage. 

#### <a name="azure-active-directory-authentication-and-rbac"></a>Authentification et RBAC Azure Active Directory

L’authentification et le contrôle d’accès en fonction du rôle (RBAC) Azure AD autorise les transformations sécurisées, les événements en direct, les stratégies de clé de contenu ou les éléments multimédias par rôle ou utilisateurs dans Azure AD.

#### <a name="client-sdks"></a>Kits de développement logiciel (SDK) client  

Langages pris en charge dans Media Services v3 : .NET Core, Java, Node.js, Ruby, Typescript, Python, Go.

#### <a name="live-encoding-updates"></a>Mises à jour de l’encodage en direct

Voici les mises à jour de l’encodage en direct qui ont été apportées :

- Nouveau mode de faible latence pour le direct (10 secondes de bout en bout).
- Prise en charge améliorée de RTMP (stabilité accrue et meilleure prise en charge de l’encodeur source).
- Ingestion sécurisée RTMPS.

    Quand vous créez un événement en direct, vous obtenez maintenant 4 URL d’ingestion. Les 4 URL d’ingestion sont presque identiques, ont le même jeton de streaming (AppId) ; seule la partie du numéro de port est différente. Il existe deux URL principales et de secours pour RTMPS. 
- Prise en charge d’un transcodage de 24 heures. 
- Prise en charge améliorée de la signalisation des annonces dans RTMP via SCTE35.

#### <a name="improved-event-grid-support"></a>Prise en charge améliorée d’Event Grid

Voici les améliorations de la prise en charge d’Event Grid que vous pouvez constater :

- Intégration d’Azure EventGrid pour un développement facilité avec Logic Apps et Azure Functions. 
- Abonnement aux événements Encodage, Canaux live, etc.

### <a name="cmaf-support"></a>Prise en charge de CMAF

Prise en charge du chiffrement CMAF et « cbcs » pour les lecteurs Apple HLS (iOS 11+) et MPEG-DASH qui prennent en charge CMAF.

### <a name="video-indexer"></a>Video Indexer

La version en disponibilité générale de l’indexeur vidéo a été annoncée en août. Pour être au fait des dernières informations concernant les fonctionnalités actuellement prises en charge, consultez [Qu’est-ce que Video Indexer](../../cognitive-services/video-indexer/video-indexer-overview.md?toc=/azure/media-services/video-indexer/toc.json&bc=/azure/media-services/video-indexer/breadcrumb/toc.json). 

### <a name="plans-for-changes"></a>Modifications planifiées

#### <a name="azure-cli-20"></a>Azure CLI 2.0
 
Le module Azure CLI 2.0 qui inclut des opérations sur toutes les fonctionnalités (dont En direct, Stratégies de clé de contenu, Filtres de comptes/éléments multimédias, Stratégies de streaming) sera bientôt disponible. 

### <a name="known-issues"></a>Problèmes connus

Seuls les clients qui utilisaient la préversion de l’API pour les filtres d’éléments multimédias ou de comptes sont concernés par le problème suivant.

Si vous avez créé des filtres d’éléments multimédias ou de comptes entre le 28/09 et le 12/10 avec l’interface CLI ou les API Media Services v3, vous devez supprimer tous les filtres d’éléments multimédias et de comptes et les recréer en raison d’un conflit de version. 

## <a name="may-2018---preview"></a>Mai 2018 - Préversion

### <a name="net-sdk"></a>Kit de développement logiciel (SDK) .Net

Les fonctionnalités suivantes sont présentes dans le Kit de développement logiciel (SDK) .Net :

* **Transformations** et **Travaux** pour encoder ou analyser le contenu du média. Pour obtenir des exemples, consultez [Diffuser des fichiers](stream-files-tutorial-with-api.md) et [Analyser](analyze-videos-tutorial-with-api.md).
* **StreamingLocators** pour la publication et la diffusion en continu de contenu sur les appareils de l’utilisateur final
* **StreamingPolicies** et **ContentKeyPolicies** pour configurer la distribution de clés et la protection du contenu (DRM) lors de la remise de contenu.
* **LiveEvents** et **LiveOutputs** pour configurer l’ingestion et l’archivage de contenu en continu en direct.
* **Éléments multimédias** pour stocker et publier du contenu multimédia dans le stockage Azure. 
* **StreamingEndpoints** pour configurer et mettre à l’échelle l’empaquetage dynamique, le chiffrement et la diffusion en continu du contenu multimédia en direct et à la demande.

### <a name="known-issues"></a>Problèmes connus

* Quand vous soumettez un travail, vous pouvez spécifier l’ingestion de votre vidéo source à l’aide d’URL HTTPS, d’URL SAP ou de chemins de fichiers situés dans le stockage Blob Azure. AMS v3 ne prend pas en charge l’encodage de transfert mémorisé en bloc sur les URL HTTPS.

## <a name="next-steps"></a>Étapes suivantes

[Vue d'ensemble](media-services-overview.md)
