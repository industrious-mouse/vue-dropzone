# vue-dropzone

A Vue component for file uploads, powered by [Dropzone.js](http://www.dropzonejs.com/). [Check out the demo](https://rowanwins.github.io/vue-dropzone/dist/index.html).

## Usage
1. Import the module
2. Register it as a component as you would any other Vue component
3. Use it within your template

### Example
````
<template>
  <div id="app">
    <p>Welcome to your Vue.js app!</p>

    <dropzone id="myVueDropzone" url="https://httpbin.org/post"></dropzone>

  </div>
</template>

<script>
  import Dropzone from 'vue-dropzone/lib/Dropzone'

  export default {
    name: 'MainApp',
    components: {
      Dropzone
    },
    events: {
      'vdropzone-success': function (file) {
        console.log('A file was successfully uploaded')
      }
    }
  }
</script>
````

## Props
Many of these props are inherited from [dropzone configuration so see their doco](http://www.dropzonejs.com/#configuration-options) for further details.

| Prop Name | Type | Description |
|----------|------|--------------|
| id | String | A string by which to identify the component, can be anything. **Required**|
| url | String | Url to post the upload to. **Required**|
| clickable | Boolean | Whether the dropzone area is clickable, if false then users can only drag items on to the area.|
| acceptedFileTypes | String | A comma separated string of accepted file types eg 'image/*,application/pdf,.psd' .|
| thumbnailHeight | Number | The height of thumbnails in pixels.|
| thumbnailWidth | Number | The width of thumbnails in pixels.|
| showRemoveLink | Boolean | Whether the Remove link is shown on items.|
| maxFileSizeInMB | Number |The maximum file size for a single upload in MB.|
| maxNumberOfFiles | Number | The maximum number of files to allow the user to upload.|
| autoProcessQueue | Boolean | Whether the files are automatically uploaded or not.|
| useCustomDropzoneOptions | Boolean | If you want to define your own Dropzone config set this to true and define a dropzoneOptions.|
| dropzoneOptions | Object | A custom set of rules to define your dropzone object, use anything available in the [dropzone config](http://www.dropzonejs.com/#configuration-options).|

## Events
Events to send to the component.

| Event Name | Description |
|------------|-------------|
| removeAllFiles() | Empties the dropzone area.|
| processQueue() | Uploads the files, required if autoProcessQueue is set to false.|

Events emitted by the component to the parent.

| Event Name | Description |
|------------|-------------|
| vdropzone-fileAdded(file) | File added to the dropzone.|
| vdropzone-success(file) | File successfully uploaded.|
| vdropzone-error(file) | File uploaded encountered an error.|
| vdropzone-removedFile(file) | A file was removed from the dropzone.|


## Development

``` bash
# install dependencies
npm install

# serve example at localhost:8080
npm run dev

# build any changes made
npm run build
```
