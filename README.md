# GmailLogout

Solved Error 
java.lang.IllegalStateException: Already managing a GoogleApiClient with id 0

@Override
public void onStop() {

    if (mGoogleApiClient != null && mGoogleApiClient.isConnected()) {
    
        mGoogleApiClient.stopAutoManage(getActivity());
        mGoogleApiClient.disconnect();
    }
    super.onStop();
}


//For signIn with Gmail

private void signIn() {

        if (mGoogleApiClient == null || !mGoogleApiClient.isConnected()) {
            try {

                GoogleSignInOptions gso = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)
                        .requestEmail()
                        .build();

                mGoogleApiClient = new GoogleApiClient.Builder(this)
                        .enableAutoManage(this, this)
                        .addApi(Auth.GOOGLE_SIGN_IN_API, gso)
                        .build();

                Intent signInIntent = Auth.GoogleSignInApi.getSignInIntent(mGoogleApiClient);
                startActivityForResult(signInIntent, RC_SIGN_IN);
            } catch (Exception e) {
            }
        }
    }
