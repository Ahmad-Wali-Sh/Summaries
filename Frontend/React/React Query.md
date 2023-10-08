# React Query

`Summary by Ahmad Wali Sharify`

    React Query is a library for Get, Post, Update, Delete Data with caching, preloading, configurations, and more performance, less code!

Install:
```
npm i @tanstack/react-query
npm i -D @tanstack/eslint-plugin-query
npm i @tanstack/react-query-devtools
```
3 Core Concepts of React Query:
- *Queries*
- *Mutations*
- *Query Invalidation*


# `Queries:`
    A query is a declarative dependency on an an asynchronous source of data that is tied to a unique key.
    - recommended for GET.
```jsx
import { useQuery } from '@tanstack/react-query' 

function App () {
  const info = useQuery({queryKey: ['todos'], queryFn: fetchTodoList})
}

// queryKey is for refecthing, caching and sharing.
// queryKey can be one Indexed Array, or anything else like = ['todos', entrance, status], if your query depend on a variable, use it.

// info has lots of important details.
// isLoading, isError, isSuccess, isFetching 
```
Sufficient way to write a query is: 
```jsx
function Todos(){
  const {isLoading, isError, data, error, fetchStatus} = useQuery({
  queryKey: ['apiCall'],
  queryFn: fetchTodoList
  )}
}

// fetchStatus can be fetching, paused, idle 
// Query Function can be literally any function that returns a promise, resolve data or throw error
```

## Dependent Query:

is a way to tell query if a value exist, run!

add this to `useQuery({})`
```
enabled: !!data;
```

## Window Focus Refetching:
```jsx
// can be disabled globally:
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      refetchOnWindowFocus: false, // default: true
    },
  },
})

//or
useQuery({
  queryKey: ['todos'],
  queryFn: fetchTodos,
  refetchOnWindowFocus: false,
})
```

## Disabling/Pausing Queries:
if you ever want to disable query from automatically running, you can use the enabled=false option.

`refetch()` is the function to use it manually.
```jsx
  const { isInitialLoading, isError, data, error, refetch, isFetching } =
    useQuery({
      queryKey: ['todos'],
      queryFn: fetchTodoList,
      enabled: false,
    })
<button onClick={() => refetch()}>Fetch Todos</button>

// or Lazy query:
```

## Paginated Queries:

using keepPreviousData to true
```jsx
function Todos() {
  const [page, setPage] = React.useState(0)

  const fetchProjects = (page = 0) => fetch('/api/projects?page=' + page).then((res) => res.json())

  const {
    isLoading,
    isError,
    error,
    data,
    isFetching,
    isPreviousData,
  } = useQuery({
    queryKey: ['projects', page],
    queryFn: () => fetchProjects(page),
    keepPreviousData : true
  })

// changing page number will make a query again with another page.
```

## Default Query Function: 

```jsx
use a global function for your queries!
const defaultQueryFn = async ({ queryKey }) => {
  const { data } = await axios.get(
    `https://jsonplaceholder.typicode.com${queryKey[0]}`,
  )
  return data
}

// provide the default query function to your app with defaultOptions
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      queryFn: defaultQueryFn,
    },
  },
})

function Posts() { 
const { status, data, error, isFetching } = useQuery({ queryKey: ['/posts'] 
}
```

<br>

<br>


# `Mutations:`

mutations are for create/update/delete data or perform server side-effects. useMutation.

```jsx
function App() {
  const mutation = useMutation({
    mutationFn: (newTodo) => {
    return axios.post('/todos', newTodo)
    },
    onSuccess: (data, variable, context) => {
    }
    onError: (error, variable, context) => {
    }
    retry: 3,
  })
}

// <butto onClick={mutation.mutate({id: new Date(), title: "Nothing"})}></button>
// has isIdle, isLoading,isError, isSuccess
```
## Persisting Offline Mutation:

If you want to resume posts when online, you can use persistQueryClient Plugin.

```jsx
const persister = createSyncStoragePersister({
  storage: window.localStorage,
})
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      cacheTime: 1000 * 60 * 60 * 24, // 24 hours
    },
  },
})

// we need a default mutation function so that paused mutations can resume after a page reload
queryClient.setMutationDefaults(['todos'], {
  mutationFn: ({ id, data }) => {
    return api.updateTodo(id, data)
  },
})

export default function App() {
  return (
    <PersistQueryClientProvider
      client={queryClient}
      persistOptions={{ persister }}
      onSuccess={() => {
        // resume mutations after initial restore from localStorage was successful
        queryClient.resumePausedMutations()
      }}
    >
      <RestOfTheApp />
    </PersistQueryClientProvider>
  )
}
```


## Updates from Mutation Responses:

use post response data to update your queries.
const queryClient = useQueryClient()

```jsx
const mutation = useMutation({
  mutationFn: editTodo,
  onSuccess: data => {
    queryClient.setQueryData(['todo', { id: 5 }], data)
  }
})


mutation.mutate({
  id: 5,
  name: 'Do the laundry',
})
```

<br>


# `Query Invalidation:`
for data that you confirm that is invalid cause of user entry, Waiting for stale time is not the case. use queryClient.invalidateQueries()

```jsx
// Invalidate every query in the cache
queryClient.invalidateQueries()
// Invalidate every query with a key that starts with `todos`
queryClient.invalidateQueries({ queryKey: ['todos'] })

// More important is invalidtion on mutation:
import { useMutation, useQueryClient } from '@tanstack/react-query'

const queryClient = useQueryClient()

// When this mutation succeeds, invalidate any queries with the `todos` or `reminders` query key
const mutation = useMutation({
  mutationFn: addTodo,
  onSuccess: () => {
    queryClient.invalidateQueries({ queryKey: ['todos'] })
    queryClient.invalidateQueries({ queryKey: ['reminders'] })
  },
})
```
Network Modes:
- Online: queries fire when you are online. 
- Always: will always do its job, offline or online. refetchOnReconnect is false.
- OfflineFist: this is in middle, run queryFn, but then pause, pausing retries.