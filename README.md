# Private Storage Adapter Extension

A private file storage adapter for PyroCMS Files Module.

## Description

This extension provides a secure, private file storage adapter that stores files in a non-publicly accessible location within your application's storage directory. Files stored using this adapter cannot be directly accessed via URL, making it ideal for sensitive documents, user uploads that require access control, or any files that should not be publicly accessible.

## Features

- **Private Storage**: Files are stored outside the public web directory
- **Local Filesystem**: Uses Laravel's local filesystem adapter under the hood
- **Automatic Directory Management**: Automatically creates storage directories based on disk slug
- **Seamless Integration**: Works with PyroCMS Files Module out of the box

## Installation

This extension is typically included with PyroCMS. If you need to install it separately:

```bash
composer require anomaly/private_storage_adapter-extension
```

## Usage

### Creating a Private Disk

1. Navigate to Files > Disks in the PyroCMS control panel
2. Click "Create Disk"
3. Select "Private" as the adapter
4. Configure your disk settings
5. Save

### Storage Location

Files are stored in:
```
storage/files-module/{disk-slug}/
```

Where `{disk-slug}` is the slug you assigned to your disk.

### Accessing Private Files

Since private files are not directly accessible via URL, you'll need to serve them through your application:

```php
use Anomaly\FilesModule\File\Contract\FileRepositoryInterface;

// Get the file
$file = app(FileRepositoryInterface::class)->find($id);

// Stream or download
return response()->download($file->path());
// or
return response()->stream(function() use ($file) {
    echo $file->read();
});
```

## Configuration

No additional configuration is required. The extension automatically:
- Creates the storage directory structure
- Registers the filesystem driver
- Integrates with the Files Module

## Use Cases

- **User Documents**: Store sensitive user documents that require authentication
- **Private Media**: Images or videos that should only be accessible to certain users
- **Administrative Files**: Internal documents and resources
- **Protected Downloads**: Files that require purchase or subscription to access
- **Confidential Data**: Any files containing sensitive information

## Security

Files stored with this adapter are:
- Stored outside the public web root
- Not directly accessible via URL
- Protected by your application's authentication and authorization
- Served only through controlled application endpoints

## Requirements

- PyroCMS 3.x
- Anomaly Streams Platform ^1.6
- Laravel 5.x+

## Support

- **Documentation**: https://pyrocms.com/documentation/private-storage-adapter-extension
- **Forum**: https://pyrocms.com/forum/channels/private-storage-adapter-extension
- **Issues**: [GitHub Issues](https://github.com/pyrocms/pyrocms/issues?q=is:issue+is:open+[private-storage-adapter-extension])
- **Slack**: https://pyrocms.com/slack

## License

This extension is open-sourced software licensed under the [MIT license](LICENSE.md).

## Authors

- **PyroCMS, Inc.** - [Website](http://pyrocms.com/)
- **Ryan Thompson** - [Website](http://ryanthepyro.com/)
