---
ms.openlocfilehash: 177f436812050ab4e9bf6c86bb5229b30f0f885b
ms.sourcegitcommit: 18785a430bc1885ccac1ebbe1f3eba634c58bea8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2020
ms.locfileid: "48822864"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="0fe39-101">Dans cette section, vous allez ajouter la possibilité de créer des événements dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0fe39-101">In this section you will add the ability to create events on the user's calendar.</span></span>

## <a name="create-a-new-event-form"></a><span data-ttu-id="0fe39-102">Créer un formulaire d’événement</span><span class="sxs-lookup"><span data-stu-id="0fe39-102">Create a new event form</span></span>

1. <span data-ttu-id="0fe39-103">Ajoutez la fonction suivante pour **ui.js** afin de restituer un formulaire pour le nouvel événement.</span><span class="sxs-lookup"><span data-stu-id="0fe39-103">Add the following function to **ui.js** to render a form for the new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/ui.js" id="showNewEventFormSnippet":::

## <a name="create-the-event"></a><span data-ttu-id="0fe39-104">Créer l’événement</span><span class="sxs-lookup"><span data-stu-id="0fe39-104">Create the event</span></span>

1. <span data-ttu-id="0fe39-105">Ajoutez la fonction suivante pour **graph.js** lire les valeurs du formulaire et créer un événement.</span><span class="sxs-lookup"><span data-stu-id="0fe39-105">Add the following function to **graph.js** to read the values from the form and create a new event.</span></span>

    :::code language="javascript" source="../demo/graph-tutorial/graph.js" id="createEventSnippet":::

1. <span data-ttu-id="0fe39-106">Enregistrez vos modifications et actualisez l’application.</span><span class="sxs-lookup"><span data-stu-id="0fe39-106">Save your changes and refresh the app.</span></span> <span data-ttu-id="0fe39-107">Cliquez sur l’élément de navigation **calendrier** , puis cliquez sur le bouton **créer un événement** .</span><span class="sxs-lookup"><span data-stu-id="0fe39-107">Click the **Calendar** nav item, then click the **Create event** button.</span></span> <span data-ttu-id="0fe39-108">Renseignez les valeurs et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="0fe39-108">Fill in the values and click **Create**.</span></span> <span data-ttu-id="0fe39-109">L’application revient à l’affichage Calendrier une fois que le nouvel événement est créé.</span><span class="sxs-lookup"><span data-stu-id="0fe39-109">The app returns to the calendar view once the new event is created.</span></span>

    ![Capture d’écran du nouveau formulaire d’événement](images/create-event-01.png)
