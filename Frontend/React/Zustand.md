# Zustand 

`Summary by Ahmad Wali Sharify`

    A solution for global states.
    and client state management.

```jsx
import { create } from 'zustand'

export const usePrescription = create((set) => ({
        prescription: [],
        setPrescription: (state) => set((prev) =>           ({prescription: state})),
}))

const {prescription, setPrescription} = usePrescription()

//Zustand Minor Example.

// Create A Store and Bind it in Any Component You Want. That's it!
```