```jsx
// useDebounce
import { useDebounce } from '@uidotdev/usehooks';
  const debounsedValue = useDebounce(value, 300);
// this hook is used to delay the use of a value.
// (value, delay) > debuoncedValue 
```

```jsx
// useLocalStorage
import { useLocalStorage } from '@uidotdev/usehooks';
  const [drawing, saveDrawing] = useLocalStorage('drawing', null)
// this hook is used to save values in local storage with specific key.
// (key, initialValue) > savedValue, setValue
```


```jsx
// useNetworkState()
import { useNetworkState } from '@uidotdev/usehooks'
  const { online, downlink, downlinkMax, effectiveType, rtt, saveData, type } = useNetworkState()
// this hook is used to retrieve network values from client
// () > online, donwlink, downlinkMax, effectiveType, rtt, saveData, type
```