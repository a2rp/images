<style>
    pre {
        padding: 15px;
        background-color: #eee;
        margin: 20px;

        white-space: pre-wrap;
        /* Since CSS 2.1 */
        white-space: -moz-pre-wrap;
        /* Mozilla, since 1999 */
        white-space: -pre-wrap;
        /* Opera 4-6 */
        white-space: -o-pre-wrap;
        /* Opera 7 */
        word-wrap: break-word;
        /* Internet Explorer 5.5+ */
    }
</style>
<pre>
    reactjs: to allow refresh/reload of web page in reactjs
    file: root > firebase.json
    {
        "hosting": {
          "public": "build",
          "rewrites": [
              {
                "source": "**",
                "destination": "/index.html"
              }
            ],
          "ignore": [
            "firebase.json",
            "**/.*",
            "**/node_modules/**"
          ]
        }
      }
    ---------------------------------------------------------------------------------------
    

    reactjs: to hide code from browser source map
    file: root > package.json
    "build": "set \"GENERATE_SOURCEMAP=false\" && react-scripts build",
    ---------------------------------------------------------------------------------------

    
    reactjs: firbase authentication and firestore
    file: client side
    cmd: install firebase
    import firebase from "firebase/compat/app";
    import "firebase/compat/firestore";
    import "firebase/compat/auth";
    firebase.initializeApp({
        apiKey: ...,
        authDomain: ...,
        projectId: ...,
        storageBucket: ...,
        messagingSenderId: ...,
        appId: ...
    });
    const firestore = firebase.firestore();
    export {firebase};
    -----------------------------------------------------
    import {firebase} from "../firebase-config";
    firebase.auth().createUserWithEmailAndPassword(creds.email,creds.password).then((userCredential)=>{
        const user = userCredential.user;
        const userId = user.uid;
        creds.uid = userId;
        creds.dateTime = new Date().toString();
        await firebase.firestore().collection("users").doc(creds.uid).set(creds).then((response)=>{
            setRegisterDetails("data updated successfully" + response);
            window.location.reload();
        }).catch((error)=>{
            setRegisterDetails(error);
        });
    }).catch((error)=>{
        const errorCode = error.code;
        const errorMessage = error.message;
        setRegisterDetails(errorMessage);
    }).finally(()=>{
        setSubmitResponse(true);
    });
</pre>
