# React Toastify

`Summary by Ahmad Wali Sharify`

```
npm install --save react-toastify
```

```jsx
//it has a Container and Emitter.
import { ToastContainer, toast} from 'react-toastify';
import 'react-toastify/dist/ReactToastify.css';

  const notify = () => toast('Wow It is Awesome');
<App>
  <button onClick={notiry}>Click To Show!</button>
  <ToastContainer />
</App>

<ToastContainer postition autoClose hidProgressBar newestOnTop cloneOnClick rtl pauseOnFocusLoss draggable pauseOnHover theme />
// are Default Props For ToastContainer.
toast('', {
  position:'top-right'
  ...
}) 
//you can specify anything special in toast emitter.
```