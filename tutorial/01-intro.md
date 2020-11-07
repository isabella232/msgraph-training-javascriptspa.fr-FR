---
ms.openlocfilehash: bbb1dd429dca4e67735c5fdb2b2280f729115eb2
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822823"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8bdaa-101">Ce didacticiel vous apprend à créer une application JavaScript à une seule page qui utilise l’API Microsoft Graph pour récupérer des informations de calendrier pour un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-101">This tutorial teaches you how to build a JavaScript single-page app that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="8bdaa-102">Si vous préférez télécharger simplement le didacticiel terminé, vous pouvez télécharger ou cloner le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span><span class="sxs-lookup"><span data-stu-id="8bdaa-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8bdaa-103">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8bdaa-103">Prerequisites</span></span>

<span data-ttu-id="8bdaa-104">Avant de commencer ce didacticiel, vous aurez besoin d’accéder à un serveur HTTP pour héberger les fichiers d’exemple.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-104">Before you start this tutorial, you will need access to an HTTP server to host the sample files.</span></span> <span data-ttu-id="8bdaa-105">Il peut s’agir d’un serveur de test sur votre ordinateur de développement ou d’un serveur distant.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-105">This could be a test server on your development machine, or a remote server.</span></span> <span data-ttu-id="8bdaa-106">Le didacticiel comprend des instructions sur l’utilisation d’un package de Node.js pour exécuter un serveur de test simple sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-106">The tutorial includes instructions to use a Node.js package to run a simple test server on your development machine.</span></span> <span data-ttu-id="8bdaa-107">Si vous envisagez d’utiliser cette option, vous devez avoir [Node.js](https://nodejs.org) installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-107">If you plan to use this option, you should have [Node.js](https://nodejs.org) installed on your development machine.</span></span> <span data-ttu-id="8bdaa-108">Si vous n’avez pas Node.js, reportez-vous au lien précédent pour obtenir les options de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-108">If you do not have Node.js, visit the previous link for download options.</span></span>

<span data-ttu-id="8bdaa-109">Vous devez également disposer d’un compte Microsoft personnel disposant d’une boîte aux lettres sur Outlook.com ou d’un compte professionnel ou scolaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-109">You should also have either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span> <span data-ttu-id="8bdaa-110">Si vous n’avez pas de compte Microsoft, vous disposez de deux options pour obtenir un compte gratuit :</span><span class="sxs-lookup"><span data-stu-id="8bdaa-110">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="8bdaa-111">Vous pouvez vous [inscrire pour obtenir un nouveau compte Microsoft personnel](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="8bdaa-111">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="8bdaa-112">Vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-112">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="8bdaa-113">Ce didacticiel a été écrit avec le nœud version 12.16.1.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-113">This tutorial was written with Node version 12.16.1.</span></span> <span data-ttu-id="8bdaa-114">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.</span><span class="sxs-lookup"><span data-stu-id="8bdaa-114">The steps in this guide may work with other versions, but that has not been tested.</span></span>

## <a name="feedback"></a><span data-ttu-id="8bdaa-115">Commentaires</span><span class="sxs-lookup"><span data-stu-id="8bdaa-115">Feedback</span></span>

<span data-ttu-id="8bdaa-116">Veuillez fournir des commentaires sur ce didacticiel dans le [référentiel GitHub](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span><span class="sxs-lookup"><span data-stu-id="8bdaa-116">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-javascriptspa).</span></span>
