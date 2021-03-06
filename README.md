# Angular Firebase Use
### Project settings and imports
```sh
$ npm install @angular/cli
$ ng new-app
$ cd new-app
$ npm install @angular/fire firebase --save
$ ng serve
```
##### environment.ts

     production: false,
       firebase: 
       //when creating new firebase project you can get these options for angular
       {
                apiKey: "",
                authDomain: "",
                databaseURL: "",
                projectId: "",
                storageBucket: "",
                messagingSenderId: ""
       }
   
##### app.module.ts
    import { environment } from '../environments/environment';
    import { AngularFireModule } from '@angular/fire';
    import { AngularFirestoreModule } from '@angular/fire/firestore';
    import { AngularFireStorageModule } from '@angular/fire/storage';
    import { AngularFireAuthModule } from '@angular/fire/auth';
    
    imports: [
        BrowserModule,
        AngularFireModule.initializeApp(environment.firebase),
        AngularFirestoreModule, // imports firebase/firestore, only needed for database features
        AngularFireAuthModule, // imports firebase/auth, only needed for auth features,
        AngularFireStorageModule // imports firebase/storage only needed for storage features
      ],
       
##### app.component.ts
    import { AngularFirestore } from '@angular/fire/firestore';
    constructor(private db: AngularFirestore) {}
## Functions
#### Getting all documents
    this.db.collection('users').get().subscribe(querySnapshot => {
      querySnapshot.forEach(doc => {
        console.log(doc.id, " => ", doc.data());
      });
    }); 
#### Add document to collection
    //Basic document adding
    //if document exits it will overwrite 
    //else it will create new document with id of new-city-id
    this.db.collection("cities").doc("new-city-id").set(data);
    
    // Add a new document with a generated id.
    this.db.collection("cities").add({
        name: "Tokyo",
        country: "Japan"
    })
    .subscribe(docRef => {
        console.log("Document written with ID: ", docRef.id);
    });
#### Delete or add new data to document
    this.db.collection('users').doc('sampleDocumentID').set(
      {name:'mark',age:21 }    
    );
#### Find spesific documents
    this.db.collection('cities').where('capital', '==', 'course1')
    .get(querySnapshot => {
      querySnapshot.forEach(doc => {
        console.log(doc.id, ' => ', doc.data());
      })
    })
### Data Types
    var docData = {
        stringExample: "Hello world!",
        booleanExample: true,
        numberExample: 3.14159265,
        dateExample: firebase.firestore.Timestamp.fromDate(new Date("December 10, 1815")),
        arrayExample: [5, true, "hello"],
        nullExample: null,
        objectExample: {
            a: 5,
            b: {
                nested: "foo"
            }
        }
    };
    this.db.collection("users").doc("one").set(docData).subscribe(()=>{
        console.log("Document successfully written!");
    });


