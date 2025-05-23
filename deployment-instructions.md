# Deployment Instructions for Inventory Management Web App

## 1. Prerequisites
- Node.js and npm installed on your deployment server.
- Firebase project set up with Firestore enabled.
- Firebase configuration details ready (apiKey, authDomain, projectId, etc.).

## 2. Environment Setup
- Clone the repository to your deployment server.
- Navigate to the project directory.
- Install dependencies:
  ```
  npm install
  ```
- Ensure the Firebase configuration in `src/lib/firebase.ts` matches your Firebase project settings.

## 3. Build the Application
- Run the build command:
  ```
  npm run build
  ```

## 4. Start the Application
- Start the production server:
  ```
  PORT=8000 npm start
  ```
- The app will be accessible at `http://localhost:8000`.

## 5. Configure Environment Variables (Optional)
- For production, consider moving Firebase config to environment variables for security.
- Update `src/lib/firebase.ts` to read from environment variables.

## 6. Firebase Security Rules
- Configure Firestore security rules in the Firebase Console to restrict access appropriately.

## 7. Additional Notes
- Monitor logs for errors and performance.
- Set up HTTPS and domain configuration as needed.
- For scaling, consider deploying on cloud platforms like Vercel, Firebase Hosting, or others.

---

This guide covers the essential steps to deploy the inventory management web app connected to Firebase.
