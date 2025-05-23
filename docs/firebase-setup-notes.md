# Firebase Setup Notes for Inventory Management Web App

## 1. Firebase Project Setup
- Create a Firebase project in the [Firebase Console](https://console.firebase.google.com/).
- Register your web app in the project settings.
- Copy the Firebase config object (as provided):
  ```js
  const firebaseConfig = {
    apiKey: "AIzaSyDyIQjV7Vmygu0MDTI5qMCcHDDbG1_n4qQ",
    authDomain: "smartcloud-f0dcf.firebaseapp.com",
    projectId: "smartcloud-f0dcf",
    storageBucket: "smartcloud-f0dcf.firebasestorage.app",
    messagingSenderId: "352913613282",
    appId: "1:352913613282:web:80b454a8946833ca8e19bb",
    measurementId: "G-61QQV7MMLV"
  };
  ```

## 2. Initialize Firebase in Your Web App
- Install Firebase SDK:
  ```
  npm install firebase
  ```
- Initialize Firebase in your app (e.g., in `src/lib/firebase.ts`):
  ```ts
  import { initializeApp } from "firebase/app";
  import { getFirestore } from "firebase/firestore";

  const firebaseConfig = {
    apiKey: "...",
    authDomain: "...",
    projectId: "...",
    storageBucket: "...",
    messagingSenderId: "...",
    appId: "...",
    measurementId: "..."
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  export { db };
  ```

## 3. Firestore Database Structure
- Use Firestore (NoSQL) to store your data.
- Suggested collections and documents:

### Collections:
- **products**
  - Document ID: auto-generated or product barcode
  - Fields:
    - name: string
    - barcode: string
    - expirationDate: timestamp
    - quantity: number
    - supplierId: string (reference to suppliers collection)
- **suppliers**
  - Document ID: auto-generated
  - Fields:
    - name: string
    - contactInfo: string
    - orderHistory: array (optional)
- **notifications** (optional)
  - Document ID: auto-generated
  - Fields:
    - productId: string
    - message: string
    - date: timestamp
    - read: boolean

## 4. CRUD Operations with Firestore
- Use Firestore SDK functions to create, read, update, and delete documents.
- Example to add a product:
  ```ts
  import { collection, addDoc } from "firebase/firestore";
  import { db } from "./firebase";

  async function addProduct(product) {
    try {
      const docRef = await addDoc(collection(db, "products"), product);
      console.log("Product added with ID: ", docRef.id);
    } catch (e) {
      console.error("Error adding product: ", e);
    }
  }
  ```

## 5. Handling Non-Existing Data
- When fetching data, check if documents exist.
- If a collection or document does not exist, Firestore will return empty results.
- You can create default documents or collections on app initialization if needed.

## 6. Authentication (Optional)
- Use Firebase Authentication for user login and JWT management.
- Integrate Firebase Auth SDK and protect your API routes accordingly.

## 7. Notifications
- Use Firestore to store notification documents.
- Use Firebase Cloud Functions (optional) to trigger email or SMS notifications for products nearing expiration.

## 8. Summary
- Replace your current backend API with Firestore CRUD operations.
- Store all product and supplier data in Firestore collections.
- Use Firebase SDK in your frontend or backend to interact with Firestore.
- Ensure proper security rules in Firebase Console to protect your data.

---

This setup will allow your web app to use Firebase as the backend database, storing all inventory and supplier data, and enabling real-time updates and notifications.
