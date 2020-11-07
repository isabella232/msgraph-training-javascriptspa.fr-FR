---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822864"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez ajouter la possibilité de créer des événements dans le calendrier de l’utilisateur.

## <a name="create-a-new-event-form"></a>Créer un formulaire d’événement

1. Ajoutez la fonction suivante pour **ui.js** afin de restituer un formulaire pour le nouvel événement.

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a>Créer l’événement

1. Ajoutez la fonction suivante pour **graph.js** lire les valeurs du formulaire et créer un événement.

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. Enregistrez vos modifications et actualisez l’application. Cliquez sur l’élément de navigation **calendrier** , puis cliquez sur le bouton **créer un événement** . Renseignez les valeurs et cliquez sur **créer**. L’application revient à l’affichage Calendrier une fois que le nouvel événement est créé.

    ![Capture d’écran du nouveau formulaire d’événement](images/create-event-01.png)
