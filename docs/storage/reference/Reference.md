# Storage Reference

A  reference represents a reference to a Google Cloud Storage object.

You can upload, download, and delete objects, as well as get/set object metadata  for a file via this reference.

## Properties

 TODO

## Methods

### child
[method]child(path) returns [ref storage.Reference];[/method]

Returns a reference to a relative path from this reference.

| Parameter |         |
| --------- | ------- |
| path  | **string**  |

Path is the relative path from this reference. Leading, trailing, and consecutive slashes are removed.

### delete
[method]delete() returns Promise<void>;[/method]

Deletes the object at this reference's location.

**Returns:** A Promise that resolves if the deletion succeeded and rejects if it failed, including if the object didn't exist.

[collapse Example]
```js
const ref = firebase.storage().ref('path/to/image.jpg');

ref.delete()
   .then(() => {
       // deleted
   })
   .catch((deleteError) => {
       // deletion error
   });
```
[/collapse]

### getDownloadURL
[method]getDownloadURL() returns Promise<string>;[/method]

Fetches a long lived download URL for this object.

**Returns:** A Promise that resolves with the download URL or rejects if the fetch failed, including if the object did not exist.

[collapse Example]
```js
const ref = firebase.storage().ref('path/to/image.jpg');

ref.getDownloadURL()
   .then((url) => {
       console.log(url);
   });
```
[/collapse]

### getMetadata
[method]getMetadata() returns Promise<[FullMetaData](https://firebase.google.com/docs/reference/js/firebase.storage.FullMetadata)>;[/method]

Fetches metadata for the object at this location, if one exists.

**Returns:** A Promise that resolves with the [metadata](https://firebase.google.com/docs/reference/js/firebase.storage.FullMetadata),
or rejects if the fetch failed, including if the object did not exist.

[collapse Example]
```js
const ref = firebase.storage().ref('path/to/image.jpg');

ref.getMetadata()
   .then((metadata) => {
       console.log(metadata.name);
       console.log(metadata.size);
       console.log(metadata.contentType);
       // etc
   });
```
[/collapse]


### updateMetadata
[method]updateMetadata([settableMetadata](https://firebase.google.com/docs/reference/js/firebase.storage.SettableMetadata)) returns Promise<[FullMetaData](https://firebase.google.com/docs/reference/js/firebase.storage.FullMetadata)>;[/method]

Updates the metadata for the object at this location, if one exists.

| Parameter |         |
| --------- | ------- |
| metadata  | **[SettableMetadata](https://firebase.google.com/docs/reference/js/firebase.storage.SettableMetadata)**  |

**Returns:** A Promise that resolves with the updated [metadata](https://firebase.google.com/docs/reference/js/firebase.storage.FullMetadata),
or rejects if the fetch failed, including if the object did not exist.

[collapse Example]
```js
const ref = firebase.storage().ref('path/to/image.jpg');

const settableMetadata = {
    contentType: 'image/jpeg',
};

ref.updateMetadata(settableMetadata)
   .then((metadata) => {
       console.log(metadata.name);
       console.log(metadata.size);
       console.log(metadata.contentType);
       // etc
   });
```
[/collapse]

### downloadFile
[method]downloadFile(filePath) returns [ref storage.StorageTask];[/method]

**React Native Firebase only.**

Downloads the storage object for this reference to the device file path specified.

| Parameter |         |
| --------- | ------- |
| filePath  | **string**  |

**Returns:** A thenable `DOWNLOAD` [ref storage.StorageTask] to track download progress.

[collapse Promise Example]
```js
    firebase
      .storage()
      .ref('/uploadOk.jpeg')
      .downloadFile(
        `${firebase.storage.Native.DOCUMENT_DIRECTORY_PATH}/ok.jpeg`
      )
      .then(successCb)
      .catch(failureCb);
```
[/collapse]

[collapse Listener Example]
```js
    const path = `${firebase.storage.Native.DOCUMENT_DIRECTORY_PATH}/ok.jpeg`;
    const ref = firebase.storage().ref('/uploadOk.jpeg');

    const unsubscribe = ref.downloadFile(path).on(
      firebase.storage.TaskEvent.STATE_CHANGED,
      (snapshot) => {
        console.log(snapshot.bytesTransferred);
        console.log(snapshot.totalBytes);
        if (snapshot.state === firebase.storage.TaskState.SUCCESS) {
          // complete
        }
      },
      (error) => {
        unsubscribe();
        console.error(error);
      },
    );
```
[/collapse]

### putFile
[method]putFile(filePath) returns [ref storage.StorageTask];[/method]

**React Native Firebase only.**

Uploads the file path specified from the device into a storage object for this reference.

Path must be a full file path to a file on the device.

| Parameter |         |
| --------- | ------- |
| filePath  | **string**  |
| metadata  | **object** (optional)  |

**Returns:** A thenable `UPLOAD` [ref storage.StorageTask] to track upload progress.

[collapse Promise Example]
```js
    firebase
      .storage()
      .ref('/uploadOk.jpeg')
      .putFile(
        `${firebase.storage.Native.DOCUMENT_DIRECTORY_PATH}/ok.jpeg`
      )
      .then(successCb)
      .catch(failureCb);
```
[/collapse]

[collapse Listener Example]
```js
    const path = `${firebase.storage.Native.DOCUMENT_DIRECTORY_PATH}/ok.jpeg`;
    const ref = firebase.storage().ref('/uploadOk.jpeg');

    const unsubscribe = ref.putFile(path).on(
      firebase.storage.TaskEvent.STATE_CHANGED,
      (snapshot) => {
        console.log(snapshot.bytesTransferred);
        console.log(snapshot.totalBytes);
        if (snapshot.state === firebase.storage.TaskState.SUCCESS) {
          // complete
        }
      },
      (error) => {
        unsubscribe();
        console.error(error);
      },
    );
```
[/collapse]
