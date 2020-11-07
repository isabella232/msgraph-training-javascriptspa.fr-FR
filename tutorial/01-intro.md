---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822823"
---
<!-- markdownlint-disable MD002 MD041 -->

Ce didacticiel vous apprend à créer une application JavaScript à une seule page qui utilise l’API Microsoft Graph pour récupérer des informations de calendrier pour un utilisateur.

> [!TIP]
> Si vous préférez télécharger simplement le didacticiel terminé, vous pouvez télécharger ou cloner le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).

## <a name="prerequisites"></a>Conditions préalables

Avant de commencer ce didacticiel, vous aurez besoin d’accéder à un serveur HTTP pour héberger les fichiers d’exemple. Il peut s’agir d’un serveur de test sur votre ordinateur de développement ou d’un serveur distant. Le didacticiel comprend des instructions sur l’utilisation d’un package de Node.js pour exécuter un serveur de test simple sur votre ordinateur de développement. Si vous envisagez d’utiliser cette option, vous devez avoir [Node.js](https://nodejs.org) installé sur votre ordinateur de développement. Si vous n’avez pas Node.js, reportez-vous au lien précédent pour obtenir les options de téléchargement.

Vous devez également disposer d’un compte Microsoft personnel disposant d’une boîte aux lettres sur Outlook.com ou d’un compte professionnel ou scolaire Microsoft. Si vous n’avez pas de compte Microsoft, vous disposez de deux options pour obtenir un compte gratuit :

- Vous pouvez vous [inscrire pour obtenir un nouveau compte Microsoft personnel](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.

> [!NOTE]
> Ce didacticiel a été écrit avec le nœud version 12.16.1. Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.

## <a name="feedback"></a>Commentaires

Veuillez fournir des commentaires sur ce didacticiel dans le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).
