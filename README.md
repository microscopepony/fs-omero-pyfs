# OMERO PyFileSystem2 implementation

A [Python filesystem abstraction](https://www.pyfilesystem.org/) layer that stores files in [OMERO](https://www.openmicroscopy.org/omero/).

This is pre-alpha software.
Breaking changes may be made.


## Example

```python
import fs
root = fs.open_fs('omero://{username}:{password}@{omerohost}')
```


## Development notes

Directories are stored as `TagAnnotation`s in a dedicated namespace.
Sub-directories are linked by an `AnnotationAnnotationLink` to the parent directory.

The sub-directory has the full (absolute) path of the directory as its `textValue` so that lookups are faster.
This may change before the first non-development release and would be an incompatible breaking change.

Files are stored as `OriginalFile`s, linked by an `OriginaFileAnnotationLink` to the parent directory.
The `path` property of the `OriginalFile` is ignored, only `name` is used.
