#fsu (fs unique)
Unique filenames with streams support

**Checking if a file exists before opening is an anti-pattern that leaves you vulnerable to race conditions: another process can remove the file between the calls to fs.exists() and fs.open(). This functions doesn't use fs.exists functionality. If file doesn't exist this will work like usual fs module methods**

##Instalation
`npm install fsu`

## openUnique(path, [mode], callback)
Same as [fs.open](http://nodejs.org/api/fs.html#fs_fs_open_path_flags_mode_callback) but open for writing and creates unique filename.

```js
var fsu = require('fsu');

fsu.openUnique("text{_###}.txt", function(err, fd) {
    //now we can use file descriptor as usual
});
```

## writeFileUnique(path, data, [options], callback)
Same as [fs.writeFile](http://nodejs.org/api/fs.html#fs_fs_writefile_filename_data_options_callback) but creates unique filename.

```js
var fsu = require('fsu');

fsu.writeFileUnique("text{_###}.txt", "test", function(err) {
    console.log("Done");
});
```

## createWriteStreamUnique(path, [options])
Same as [fs.createWriteStream](https://nodejs.org/api/fs.html#fs_fs_createwritestream_path_options) but returns writable stream for unique file.

```js
var fsu = require('fsu');
var stream = fsu.createWriteStreamUnique("text{_###}.txt");
```

## force path creation
Add `force = true` to options, and it will recursively create directories if they are not exist.

## pattern
You must use `{#}` pattern in filename and path. All `#` characters will be change with counter for existing files. Number of `#` means padding for unique counter. **With no pattern in the filename works as usual 'fs' module.**

If we run second example several times filenames will be
```
text.txt
text_001.txt
text_002.txt
```


License: MIT
