# React Auth Kit

`Summary by Ahmad Wali Sharify`

    React AUTH Kit is a Lightweight AUTH state management library for React.
```
npm install --save react-auth-kit
```
**app.jsx**
```jsx
import { AuthProvider, RequireAuth  } from 'react-auth-kit'

<AuthProvider authType={'localstorage'} authName='_auth'>
  <App />
    <RequireAuth loginPath='/login'>
        <SecuredComponent />
     </RequireAuth>
</AuthProvider>

//login.jsx
import { useSignIn, useSignOut } from 'react-auth-kit'
const signIn = useSignIn()
const signOut = useSignOut()
  if (signIn(
      {
        token: res.data.token
        expiresIn: res.data.expiresIn,
        tokenType: 'Token'
        authState: me_res.data
      }) {
          //Do Something
      }
   else {
          // Don't do Anything
  }

))
```
**component.jsx**

```jsx
import { useAuthUser, useIsAuthenticated } from 'react-auth-kit'
const auth = useAuthUser()
auth().user => is the actual name of user and more data.
const isAuthen = useIsAuthenticated()
isAuthen() can be true or false
```