# cors



https://github.com/axios/axios/issues/319

```javascript
const axiosConfig = {
headers: {
'content-Type': 'application/json',
"Accept": "/",
"Cache-Control": "no-cache",
"Cookie": document.cookie
},
credentials: "same-origin"
};
axios.defaults.withCredentials = true;
axios.get('/url',
axiosConfig)
.then((res) => {
// Some result here
})
.catch((err) => {
console.log(':(');
});
```




WorkingDirectory



