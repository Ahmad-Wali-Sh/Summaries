`Summary by Ahmad Wali Sharify`

Axios is an HTTP client Library that allows you to make requests to a given endpoint.

```
// installation
npm i axios
```
```jsx
axios.get(url, { headers: {}}).then().catch()
axios.post(url, {data}, { headers: {}}).then().catch()
axios.put(url, {data}, {headers: {}}).then().catch()
axios.delete(url, {headers: {}}).then().catch()

const client = axios.create({
  baseURL: 'http://here-there/'
})

async function deletePost () {
  await client.delete('/1');
  alert('post Deleted')

  client.get('/1')
}
```