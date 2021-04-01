# ScopedStorage: localStorage & sessionStorage per page

A simple wrapper around localStorage and sessionStorage that mimics **storage per scope** such as a single web page.
This is done via a key prefix that is passed when constructing a ScopedStorage.

Value **types are preserved** by default (unlike localStorage and sessionStorage).

No key prefix (`scope`) can be a substring of another key prefix so generally URLs should not be used as-is;
for example, clearing the ScopedStorage of `/project/` will also clear that of `/project/foo/`
(unless this is what you would like).
If the current URL is `/project/foo/`, you could use key prefix `project-foo/`
(i.e. remove any leading or trailing `/`, replace each remaining `/` with `-` and end with a `/`).

```js
// Initiate a storage (underlying type is sessionStorage by default)
var storage = new ScopedStorage('project-foo/');

// To specify localStorage as the underlying type
var lastingStorage = new ScopedStorage('project-bar/', StorageTypes.LOCAL_STORAGE);

// For a behaviour that only returns string values (like localStorage and sessionStorage)
var allStringValueStorage = new ScopedStorage('project-bar/', StorageTypes.SESSION_STORAGE, true);

/* use the object the same way you would with localStorage or sessionStorage with these methods:
setItem, getItem, removeItem, clear
*/

storage.setItem('pi', 3.14);
console.log(storage.getItem('pi'));   // 3.14

storage.setItem('bar', '1.05e-34');
console.log(storage.getItem('bar'));  // '1.05e-34'

storage.removeItem('pi');

storage.clear();
```

## TODO

- [ ] Add tests
- [ ] `length` property
- [ ] `key` method
- [ ] Benchmark against:
  - [ ] raw localStorage and sessionStorage
  - [ ] [macmcmeans/localDataStorage](https://github.com/macmcmeans/localDataStorage)
