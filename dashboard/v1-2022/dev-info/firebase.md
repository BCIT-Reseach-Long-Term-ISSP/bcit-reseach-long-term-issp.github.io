---  
layout: default  
title: Firebase
has_children: false  
permalink: /docs/dashboard/firestore
parent: Dashboard  
has_toc: true
---  

# Firebase
{: .no_toc }

This page contains information relevant to the dashboard with regard to Firebase and Firestore.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Firestore Rules

Reading and writing from the Firestore requires rules to be set. These rules dictate who can edit which documents from which collection, and they help protect the database from malicious users. Rules only apply to external access to the Firestore; rules do not apply to any actions performed within the Firebase console.

Rules of Firestore are written in a custom language. More information about this language can be found [here](https://firebase.google.com/docs/rules/rules-language).

As of May 12th, 2022, the rules dictated thus:
- Anyone can read from the "devices" collection of the database, regardless of authentication and whether they are logged in.
- Only users who are logged in as an admin account may write to the "devices" collection of the database.
- Users can only read the document in the "users" collection corresponding to their own user UID, and cannot read anyone else's, regardless of authentication status.
- The "users" collection cannot be written to externally.

Below is the code/content which causes the above rules to be enforced. They can be found in the "rules" tab of the "Firestore Database" page in the Firebase console.

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
  	// anyone can read devices
    // but only admin users can write
    match /devices/{document=**} {
      allow read: if true;
      allow write: if get(/databases/$(database)/documents/users/$(request.auth.uid)).data.admin == true;
    }
    
    // users can only read whether they're an admin
    // and users can only read their own data
    match /users/{userId} {
      allow read: if request.auth != null && request.auth.uid == userId;
      allow write: if false;
    }
  }
}
```

Information on how to construct basic rules can be found [here](https://firebase.google.com/docs/rules/basics).

## Making a user an admin for the dashboard

In the dashboard's manage device/notifications page, users must sign in via Google as an admin account in order to edit device information such as a device's name or its thresholds.

By default, however, users are not designated as an admin account. User admin status is stored within the bcitema Firebase project's Firestore database, in the "users" collection.

Per the rules, contents of the "users" collection cannot be edited externally; this means that admins must be added via the Firebase console. 

Below details the steps required to add a user as an admin using the Firebase console.

1. Have the user log in via the Account tab of the manage device/notifications page of the dashboard.
   
   ![Account page with no user logged in](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account1NotLoggedIn.png?raw=true "Account page with no user logged in")

   ![Account page with a non-admin user logged in](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account2NonAdmin.png?raw=true "Account page with a non-admin user logged in")

    Note that the user will be a non-admin account. What's important, however, is that the user has logged in, as it will allow us to see their Google user UID, which we will use to add an entry into the "users" collection to designate the user as an admin.

2. In the Authentication page of the Firebase console, find the identifier (email address) of the user whom you would like to provide admin status to, and copy their User UID by pressing the copy UID button.

    ![Authentication page, with user UID pointed out](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account3AuthenticationPage.png?raw=true "Authentication page, with user UID pointed out")

    Please ensure that the User UID which you copy is absolutely the correct User UID, as any error will potentially result in an unintended user gaining editor permissions inside the dashboard.

3. Navigate to the Firestore Database page of the Firebase console. Then, select the "users" collection, and select "Add document".

    ![Firestore tab, with "users" collection and "Add document" option pointed out](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account4FirestorePage.png?raw=true "Firestore page, with \"users\" collection and \"Add document\" option pointed out")

4. In the "Document ID" field, paste the UID which you copied. Then, in the "field" section, type "admin" (case-sensitive), and change the type to "boolean". Ensure that the value is "true". Then, press "Save".

   ![Add a document, with details filled out](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account5FirestoreDocument.png?raw=true "Add a document, with details filled out")

    After pressing done, the new document should appear in the "users" collection list.

5. You're all set. The user may need to refresh the dashboard window, but when they do, it should state that they are an admin user, as seen below.

   ![Account page with an admin user logged in](https://github.com/BCIT-Reseach-Long-Term-ISSP/bcit-reseach-long-term-issp.github.io/blob/master/dashboard/assets/Account6Admin.png?raw=true "Account page with an admin user logged in")

    Now, the user will be able to edit device information.

{: .fs-6 .fw-300 }