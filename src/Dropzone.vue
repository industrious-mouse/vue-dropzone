<template>
  <form action="{{url}}" class="dropzone" id="{{id}}"></form>
</template>

<script>
  var Dropzone = require('dropzone')
  Dropzone.autoDiscover = false

  export default {
    props: {
      id: {
        type: String,
        required: true
      },
      url: {
        type: String,
        required: true
      },
      clickable: {
        type: Boolean,
        default: true
      },
      acceptedFileTypes: {
        type: String
      },
      thumbnailHeight: {
        type: Number,
        default: 200
      },
      thumbnailWidth: {
        type: Number,
        default: 200
      },
      showRemoveLink: {
        type: Boolean,
        default: true
      },
      maxFileSizeInMB: {
        type: Number,
        default: 2
      },
      maxNumberOfFiles: {
        type: Number,
        default: 5
      },
      autoProcessQueue: {
        type: Boolean,
        default: true
      },
      useCustomDropzoneOptions: {
        type: Boolean,
        default: false
      },
      dropzoneOptions: {
        type: Object
      }
    },
    events: {
      removeAllFiles: function () {
        this.dropzone.removeAllFiles(true)
      },
      processQueue: function () {
        this.dropzone.processQueue()
      }
    },
    ready () {
      var element = document.getElementById(this.id)
      if (!this.useCustomDropzoneOptions) {
        this.dropzone = new Dropzone(element, {
          clickable: this.clickable,
          thumbnailWidth: this.thumbnailWidth,
          thumbnailHeight: this.thumbnailHeight,
          maxFiles: this.maxNumberOfFiles,
          maxFilesize: this.maxFileSizeInMB,
          dictRemoveFile: 'Remove',
          addRemoveLinks: this.showRemoveLink,
          acceptedFiles: this.acceptedFileTypes,
          autoProcessQueue: this.autoProcessQueue,
          dictDefaultMessage: '<i class="material-icons">cloud_upload</i><br>Drop files here to upload',
          previewTemplate: '<div class="dz-preview dz-file-preview">  <div class="dz-image" style="width:' + this.thumbnailWidth + 'px;height:' + this.thumbnailHeight + 'px"><img data-dz-thumbnail /></div>  <div class="dz-details">    <div class="dz-size"><span data-dz-size></span></div>    <div class="dz-filename"><span data-dz-name></span></div>  </div>  <div class="dz-progress"><span class="dz-upload" data-dz-uploadprogress></span></div>  <div class="dz-error-message"><span data-dz-errormessage></span></div>  <div class="dz-success-mark"> <i class="material-icons">done</i> </div>  <div class="dz-error-mark"><i class="material-icons">error</i></div></div>'
        })
      } else {
        this.dropzone = new Dropzone(element, this.dropzoneOptions)
      }

      // Handle the dropzone events
      var vm = this
      this.dropzone.on('addedfile', function (file) {
        vm.$parent.$emit('vdropzone-fileAdded', file)
      })

      this.dropzone.on('removedfile', function (file) {
        vm.$parent.$emit('vdropzone-removedFile', file)
      })

      this.dropzone.on('success', function (file) {
        vm.$parent.$emit('vdropzone-success', file)
      })

      this.dropzone.on('error', function (file) {
        vm.$parent.$emit('vdropzone-error', file)
      })
    }
  }

</script>

<style>
  @import url('../node_modules/dropzone/dist/dropzone.css');
  @import 'https://fonts.googleapis.com/css?family=Roboto';

  .dropzone {
    border: 2px solid #E5E5E5;
    font-family: 'Roboto', sans-serif;
    color: #777;
    transition: background-color .2s linear;
  }
  .dropzone:hover {
    background-color: #F6F6F6;
  }

  i {
    color: #CCC;
  }

  .dropzone .dz-preview .dz-image {
    border-radius: 0px;
  }

  .dropzone .dz-preview:hover .dz-image img {
    transform: none;
    -webkit-filter: none;
  }

  .dropzone .dz-preview .dz-details {
    bottom: 0px;
    top: 0px;
    color: white;
    background-color: rgba(33, 150, 243, 0.8);
    transition: opacity .2s linear;
    text-align: left;
  }
  .dropzone .dz-preview .dz-details .dz-filename span,
  .dropzone .dz-preview .dz-details .dz-size span {
    background-color: transparent;
  }
  .dropzone .dz-preview .dz-details .dz-filename:not(:hover) span {
    border: none;
  }

  .dropzone .dz-preview .dz-details .dz-filename:hover span {
    background-color: transparent;
    border: none;
  }

  .dropzone .dz-preview .dz-remove {
    position: absolute;
    z-index: 30;
    color: white;
    margin-left: 15px;
    padding: 10px;
    top: inherit;
    bottom: 15px;
    border: 2px white solid;
    text-decoration: none;
    text-transform: uppercase;
    font-size: 0.8rem;
    font-weight: 800;
    letter-spacing: 1.1px;
    opacity: 0;
  }

  .dropzone .dz-preview:hover .dz-remove {
    opacity: 1;
  }

  .dropzone .dz-preview .dz-success-mark, .dropzone .dz-preview .dz-error-mark {
    margin-left: -40px;
    margin-top: -50px;
  }

  .dropzone .dz-preview .dz-success-mark i, .dropzone .dz-preview .dz-error-mark i {
    color: white;
    font-size: 5rem;
  }
</style>