---
title: Generating custom urls
---

When `getUrl` is called, the task of generating that URL is passed to an implementation of `Spatie\MediaLibraryUrlGenerator`.

The package contains a `LocalUrlGenerator` that can generate URLs for a media library that is stored inside the public path. An `S3UrlGenerator` is also included for when you're using S3 to store your files.

If you are storing your media files in a private directory or are using a different filesystem, you can write your own `UrlGenerator`. Your generator must adhere to the `Spatie\MediaLibraryUrlGenerator` interface. If you'd extend `Spatie\MediaLibraryUrlGenerator\BaseGenerator` you only need to implement one method: `getUrl`, which should return the URL. You can call `getPathRelativeToRoot` to get the relative path to the root of your disk.

The code of the included `S3UrlGenerator` should help make things more clear:

```php
namespace Spatie\MediaLibrary\UrlGenerator;

class S3UrlGenerator extends BaseUrlGenerator
{
    /**
     * Get the url for the profile of a media item.
     *
     * @return string
     */
    public function getUrl() : string
    {
        return config('laravel-medialibrary.s3.domain').'/'.$this->getPathRelativeToRoot();
    }
}
```
