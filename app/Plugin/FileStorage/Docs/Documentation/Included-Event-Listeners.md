Included Event Listeners
========================

LocalFileStorageListener
------------------------

The file and folder structure it will generate looks like that:

```
basePath/files/xx/xx/xx/<uuid>/<uuid>.<extension>
```

ImageProcessingListener
-----------------------

This listener will create versions of images if Configure::read('Media.imageSizes.' . $model); is not empty. If no processing operations for that model were specified it will just save the image.

This adapter replaces LocalImageProcessingListener and currently supports the Local and AmazonS3 adapter.

The file and folder structure it will generate looks like that:

```
basePath/images/xx/xx/xx/<uuid>/<uuid>.<extension>
```

Versioned images will look like that

```
basePath/images/xx/xx/xx/<uuid>/<uuid>.<hash>.<extension>
```

 * For the Local adapter basePath is the value from Configure::read('Media.basePath').
 * For AmazonS3 the basePath will be the bucket and Amazon S3 URL prefix.

xx stands for a semi random alphanumerical value calculated based on the given file name if the Local adapter was used.

**Some important notes about the path the processor generates:**

The path stored to the database is **not** going to be the complete path, it won't add the filename for a reason.

The filename is generated by the processor on the fly when adding/deleting/modifying images because the versions are build on the fly and not stored to the database. See `ImageProcessingListener::_buildPath()`.

LocalImageProcessingListener (deprecated)
-----------------------------------------

The LocalImageProcessingListener is **deprecated**, use ImageProcessingListener.