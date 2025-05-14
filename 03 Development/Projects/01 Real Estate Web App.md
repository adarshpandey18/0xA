
# 🚀 Mahalaxmi Developers

## 🧭 Overview
A Web app powered by Firebase for property management. 

---

## 🎯 Objective
- What problem does this project solve?  
  → It's easier for the company to track and list properties and interact with customers.  
- Why did you build it?  
  → To learn basic CRUD and chat features.  
- Is it personal, academic, freelance, or a clone?  
  → Academic / Freelance  

---

## 🛠️ Tech Stack
- **Frontend**: Flutter  
- **Backend**: Firebase  
- **Database**: Firebase Firestore  
- **State Management**: Provider  
- **Tools/Services**: Git  

---

## ✨ Features
- ✅ Authentication - Normal user / Admin  
- ✅ Admin Panel - Add / Remove property / Chat with user  
- ✅ User chat with admin  
- ✅ Categorization of property  

---

## 📷 Screenshots / Demo

![[Mahalaxmi-Developers-Auth-Landing-Page.png]]  

![[Mahalaxmi-Developers-Categories-Page.png]]   
![[Mahalaxmi-Developers-Admin-Panel.png]]

---

## 🧠 Key Learnings
- Firebase, Firestore, Admin Panel  
- Built logic for the admin panel  

---

## 🗒️ Future Improvements
- UI for categories page  
- WebSockets implementation  
- Test Cases, Clean Architecture  

---

## 🔗 Links
- [GitHub Repo](https://github.com/adarshpandey18/mahalaxmi-developers#)  
- [Live Site / Demo](https://mahalaxmi-developer.web.app/#/splash_screen)  

---

## 🔍 Logic Snippets

### 🔐 Authentication
```dart
import 'package:firebase_auth/firebase_auth.dart';
import 'package:flutter/material.dart';
import 'package:google_sign_in/google_sign_in.dart';
import 'package:mahalaxmi_developers/services/databse_service.dart';
import 'package:mahalaxmi_developers/widgets/alert_box.dart';

class AuthService {
  final _databaseService = DatabaseService();

  // Sign Up user with email and passowrd
  signUp(
      {required String name,
      required String email,
      required String password,
      required BuildContext context}) async {
    try {
      final userCredential = await FirebaseAuth.instance
          .createUserWithEmailAndPassword(email: email, password: password);
      // Saving user data to firestore
      await _databaseService.saveUserData(
          userCredential.user!.uid, name, email, password);
      // Scaffold Message
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('User Registered Successfully')),
      );

      // navigation to home screen
      Navigator.pushReplacementNamed(context, '/home');
    } on FirebaseAuthException catch (e) {
      if (e.code == 'email-already-in-use') {
        AlertBox.alertBox(
          title: 'Email Already Exists',
          content: 'The provided email is already in use by an existing user.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else if (e.code == 'invalid-email') {
        AlertBox.alertBox(
          title: 'Invalid Email',
          content: 'The provided value for the email user property is invalid.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else if (e.code == 'weak-password') {
        AlertBox.alertBox(
          title: 'Weak Password',
          content: 'The password entered is too weak.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      }
    } catch (e) {
      AlertBox.alertBox(
        title: 'Exception',
        content: e.toString(),
        buttonText: 'Try Again',
        function: () => {},
        context: context,
      );
    }
  }

  signIn(String email, String password, BuildContext context) async {
    try {
      // signing in user with email and passowrd
      await FirebaseAuth.instance
          .signInWithEmailAndPassword(email: email, password: password);
      // Scaffold Message
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('User Sign In Successfully')),
      );

      // on successfull signing in the user will be redirected to home screen.
      Navigator.pushNamed(context, '/home');
    } on FirebaseAuthException catch (e) {
      if (e.code == 'user-not-found') {
        AlertBox.alertBox(
          title: 'User Not Found',
          content: 'There is no existing user record corresponding to $email.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else if (e.code == 'invalid-email') {
        AlertBox.alertBox(
          title: 'Invalid Email',
          content: 'The provided value for the email user property is invalid.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else if (e.code == 'wrong-password') {
        AlertBox.alertBox(
          title: 'Invalid Password',
          content: 'The password entered is invalid.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else if (e.code == 'invalid-credential') {
        AlertBox.alertBox(
          title: 'Incorrect email id or password',
          content: 'The enterd credentials is incorrect.',
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      } else {
        AlertBox.alertBox(
          title: 'Error',
          content: e.toString(),
          buttonText: 'Try Again',
          function: () => {},
          context: context,
        );
      }
    } catch (e) {
      AlertBox.alertBox(
        title: 'Exception',
        content: e.toString(),
        buttonText: 'Try Again',
        function: () => {},
        context: context,
      );
    }
  }

  signOut(BuildContext context) async {
    try {
      // signing out user
      await FirebaseAuth.instance.signOut();

      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('User Sign Out Successfully')),
      );

      Navigator.pushReplacementNamed(context, '/auth_landing');
    } catch (e) {
      AlertBox.alertBox(
        title: 'Exception',
        content: e.toString(),
        buttonText: 'Try Again',
        function: () => {},
        context: context,
      );
    }
  }

  forgotPassword(BuildContext context, String email) async {
    try {
      // sending forgot password link to the email
      await FirebaseAuth.instance.sendPasswordResetEmail(email: email);
      AlertBox.alertBox(
        title: 'Check your email',
        content: 'Password reset link has been sent to your email.',
        buttonText: 'Ok',
        function: () => {},
        context: context,
      );
    } catch (e) {
      AlertBox.alertBox(
        title: 'Exception',
        content: e.toString(),
        buttonText: 'Try Again`',
        function: () => {},
        context: context,
      );
    }
  }

  /// Sign Up method using Google
  googleSignIn({required BuildContext context}) async {
    try {
      // Trigger the authentication flow
      final GoogleSignInAccount? googleUser = await GoogleSignIn().signIn();
      // Obtain the auth details
      final GoogleSignInAuthentication? googleAuth =
          await googleUser?.authentication;
      // Create an credentials
      final credentials = GoogleAuthProvider.credential(
        accessToken: googleAuth?.accessToken,
        idToken: googleAuth?.idToken,
      );
      final userCredential =
          await FirebaseAuth.instance.signInWithCredential(credentials);
      // Scaffold Message
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('User Sign In Successfully')),
      );

      // Saving user data to Firestore without password
      await _databaseService.saveUserData(
        userCredential.user!.uid,
        userCredential.user?.displayName ?? 'Google User',
        userCredential.user?.email ?? 'no-email@example.com',
        'Google User',
      );

      Navigator.pushNamed(context, '/home');
    } catch (e) {
      AlertBox.alertBox(
        title: 'Exception',
        content: e.toString(),
        buttonText: 'Try Again',
        function: () => {},
        context: context,
      );
    }
  }
}
```

### 💬 Chat
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:mahalaxmi_developers/models/agent.dart';
import 'package:mahalaxmi_developers/models/message.dart';
import 'package:mahalaxmi_developers/models/user.dart';

class ChatService {
  // getting list of agents
  Future<List<Agent>> getAgents() async {
    final querySnapShot =
        await FirebaseFirestore.instance.collection('admin').get();
    List<Agent> agentList =
        querySnapShot.docs.map((doc) => Agent.fromFirestore(doc)).toList();

    return agentList;
  }

  Future<List<Users>> getUser() async {
    final querySnapshot =
        await FirebaseFirestore.instance.collection('users').get();
    List<Users> userList =
        querySnapshot.docs.map((doc) => Users.fromFirestore(doc)).toList();
    return userList;
  }

  // sending messages
  Future<void> sendMessage({
    required String senderUID,
    required String senderEmail,
    required String receiverUID,
    required String message,
  }) async {
    Timestamp timeStamp = Timestamp.now();
    Message msg = Message(
        senderUID: senderUID,
        senderEmail: senderEmail,
        receiverUID: receiverUID,
        message: message,
        timeStamp: timeStamp);
    List<String> uid = [senderUID, receiverUID];
    uid.sort();
    String roomId = uid.join('_');

    try {
      // Adding message to Firestore
      await FirebaseFirestore.instance
          .collection('chat_rooms')
          .doc(roomId)
          .collection('messages')
          .add(msg.toMap());

      // Optionally, add a small delay to ensure data is written and available
      await Future.delayed(const Duration(milliseconds: 500));
    } catch (e) {
      print('Error sending message: $e');
    }
  }

  Stream<QuerySnapshot> getMessages({
    required String senderUID,
    required String receiverUID,
  }) {
    List<String> uid = [senderUID, receiverUID];
    uid.sort();
    String roomID = uid.join('_');

    return FirebaseFirestore.instance
        .collection('chat_rooms')
        .doc(roomID)
        .collection('messages')
        .orderBy('timeStamp', descending: false)
        .snapshots();
  }
}

```

### 🧱 Database
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import 'package:flutter/foundation.dart';

class DatabaseService {
  saveUserData(String uid, String name, String email, String password) async {
    try {
      await FirebaseFirestore.instance.collection("users").doc(uid).set({
        'uid': uid,
        'name': name,
        'email': email,
        'password': password,
      });
    } catch (e) {
      if (kDebugMode) {
        print("Error saving user data: $e");
      }
    }
  }

  saveAdminData(String uid, String name, String email, String password) async {
    try {
      await FirebaseFirestore.instance.collection('admin').doc(uid).set({
        'uid': uid,
        'name': name,
        'email': email,
        'password': password,
      });
    } catch (e) {
      if (kDebugMode) {
        print('Error saving user data $e');
      }
    }
  }
}

```

### 🏘️ Property
```dart
import 'package:cloud_firestore/cloud_firestore.dart';

class PropertyService {
  Future<void> addProperty(Map<String, dynamic> property) async {
    try {
      await FirebaseFirestore.instance.collection('properties').add({
        'name': property['name'],
        'description': property['description'],
        'category': property['category'],
        'bhkConfig': property['bhkConfig'],
        'squareFeet': property['squareFeet'],
        'price': property['price'],
        'address': property['address'],
        'latitude': property['latitude'],
        'longitude': property['longitude'],
        'amenities': property['amenities'],
        'contactNumber': property['contactNumber'],
        'whatsappNumber': property['whatsappNumber'],
        'imageLink': property['imageLink'],
        'createdAt': FieldValue.serverTimestamp(),
      });
    } catch (e) {
      rethrow;
    }
  }

  Future<void> deleteProperty(String propertyId) async {
    try {
      await FirebaseFirestore.instance
          .collection('properties')
          .doc(propertyId)
          .delete();
    } catch (e) {
      rethrow;
    }
  }
}

```

---

## 📑 Tags
#Flutter #Firebase #AcademicProject #InterviewReady