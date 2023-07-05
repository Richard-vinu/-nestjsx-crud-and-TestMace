import cognitoConfig from "../config/cognitoConfig.json";
import Amplify, { Auth } from "aws-amplify";
// import {CustomChromeStorage} from '../utils/customChromeStorage'

Amplify.configure({
    Auth: {
        userPoolId: cognitoConfig.userPool,
        userPoolWebClientId: cognitoConfig.clientId,
        region: cognitoConfig.region,
        oauth: {
            domain: cognitoConfig.userPoolUri,
            scope: cognitoConfig.tokenScopes,
            redirectSignIn: cognitoConfig.callbackUri,
            redirectSignOut: cognitoConfig.signoutUri,
            responseType: "code",
        },
        // storage: CustomChromeStorage
    },
});




async function federatedSignIn(provider) {
    return await Auth.federatedSignIn({ provider });
}


import React from "react";
import { federatedSignIn } from "../../utils/cognitoAuth";

export default function GoogleSignIn() {
    return (
        <>
            <h3>Google Sign In</h3>
            <button onClick={() => federatedSignIn("Google")}>
                Login/Register with Google
            </button>
        </>
    );
}
