---  
layout: default  
title: Login Components
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/login-page
---  

# Log In Components
{: .no_toc }



## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## AccountSection

AccountSection is a component which handles logging in and out on the website. It displays a prompt to log in if the user is not logged in, and if the user is logged in, it displays account details, including whether the user is an admin.

**Props used:**
- *fbAuth*: a Firebase authentication object. This should be handed down from the App.js component.
- *fbProvider*: a Firebase provider object. This should be handed down from the App.js component.
- *db*: a Firestore database object. Used to check whether the user is an admin or not.
- *currentUser*: the current user object. Used to display information pertaining to the user.
- *setCurrentUser*: updates the current user object. Used when logging in/out.
- *isUserAdmin*: indicates if the user is an admin. 
    - Please note that this does not truly affect what the user is able to do with writing permissions, as if a user's account is not really an admin account, their attempts to write to the Firestore will be rejected regardless of this variable's value.
- *setIsUserAdmin*: sets the indicator for if the user is an admin.

**Functions implemented:**
- *onAuthStateChanged*: Calls a callback function whenever the state of the authentication object is changed (i.e. log in, log out, etc.).
    - The callback function used in this component checks whether there is a user logged in, and if there is, grabs whether they're an admin, and sets the isUserAdmin state, as well as the currentUser state.
    - If the user is not logged in, it sets isUserAdmin to false, and sets currentUser to undefined.
    - Please note that this function is simply called in this file, and not actually created. However, its call contains a callback function which is implemented in this file.

**Noteworthy components used:**
- *LoggedInSection*: A component displayed if the user is logged in (checked by whether currentUser has a value). More information in the LoggedInSection section of this page.
- *LogInSection*: A component displayed if the user is not logged in. More information in the LogInSection section of this page.

## LoggedInSection

**Props used:**
- *fbAuth*: a Firebase authentication object. This should be handed down from the App.js component.
- *currentUser*: the current user object. Used to display information pertaining to the user.
- *setCurrentUser*: updates the current user object. Used when logging out.
- *isUserAdmin*: indicates if the user is an admin.
- *setIsUserAdmin*: sets the indicator for if the user is an admin.

**Functions implemented:**
- *logOutOfAccount*: signs the user out of their account, and sets currentUser and isUserAdmin to undefined and false respectively.

## LogInSection

**Props used:**
- *fbAuth*: a Firebase authentication object. This should be handed down from the App.js component.
- *fbProvider*: a Firebase provider object. This should be handed down from the App.js component.

**Notes:**
- This component will make a pop-up for logging in via Google. This component doesn't need to set the current user because the authorization object state change handles this on its own in the AccountDetails component.

{: .fs-6 .fw-300 }