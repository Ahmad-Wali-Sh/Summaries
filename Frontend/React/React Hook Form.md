# React Hook Form

`Summary by Ahmad Wali Sharify`

    A Manager For Forms Submit and Value.
    import { useForm } from "react-hook-form"


```jsx
export default function App() {
  const {
    register,
    handleSubmit,
    watch,
    formState: { errors },
  } = useForm()

  const onSubmit = (data) => console.log(data)

  console.log(watch("example")) // watch input value by passing the name of it

  return (
    /* "handleSubmit" will validate your inputs before invoking "onSubmit" */
    <form onSubmit={handleSubmit(onSubmit)}>
      {/* register your input into the hook by invoking the "register" function */}
      <input defaultValue="test" {...register("example")} />

      {/* include validation with required or other standard HTML validation rules */}
      <input {...register("exampleRequired", { required: true })} />
      {/* errors will return when field validation fails  */}
      {errors.exampleRequired && <span>This field is required</span>}

      <input type="submit" />
    </form>
  )
}

// const { register, handleSubmit, watch, reset, setFocus, getValues, formState: {errors} } = useForm()
```

1. `Register Fields:` Each Input is required to have a unique Key to be registerd

```html
      <input type='text' {...register('example')}/>
```

2. `Apply Validation:` You Can use Validation in React hook Form
  :required - min - max - minLength - maxLength - pattern - validate

```html
      <input type='text' {...register('example'), {required: true, maxLength: 20}} />
```
3. `Handle Errors`:
  - an object of all errors

```jsx
      <input type='text' {...register('example'), {required: true, maxLength: 20}} />
      {errors.example && 'Do Better job at writing!'}
```
4. `watch` is for seeing an individual input value. 
```
    watch('example')
```
5. `reset` is for reseting Form like
```
    reset({example: ''})
```
6. `setFocus`
  is For Focusing on Registered Input
```
    setFocus('example')
```
7. `getValues()` is for Getting All Form Values

8. `handleSubmit(SubmitFunction)()` is for submiting all Form Data with A Submit Function.

