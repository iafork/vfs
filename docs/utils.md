# utils

---


```go
    import "github.com/c2fo/vfs/v5/utils"
```

#### Error Constants

```go
const (
	// ErrBadAbsFilePath constant is returned when a file path is not absolute
	ErrBadAbsFilePath = "absolute file path is invalid - must include leading slash and may not include trailing slash"
	// ErrBadRelFilePath constant is returned when a file path is not relative
	ErrBadRelFilePath = "relative file path is invalid - may not include leading or trailing slashes"
	// ErrBadAbsLocationPath constant is returned when a file path is not absolute
	ErrBadAbsLocationPath = "absolute location path is invalid - must include leading and trailing slashes"
	// ErrBadRelLocationPath constant is returned when a file path is not relative
	ErrBadRelLocationPath = "relative location path is invalid - may not include leading slash but must include trailing slash"
)
```

#### func  EnsureLeadingSlash

```go
func EnsureLeadingSlash(dir string) string
```
EnsureLeadingSlash is like EnsureTrailingSlash except that it adds the leading
slash if needed.

#### func  EnsureTrailingSlash

```go
func EnsureTrailingSlash(dir string) string
```
EnsureTrailingSlash is like AddTrailingSlash but will only ever use / since it's
use for web uri's, never an Windows OS path.

#### func  GetFileURI

```go
func GetFileURI(f vfs.File) string
```
GetFileURI returns a File URI

#### func  GetLocationURI

```go
func GetLocationURI(l vfs.Location) string
```
GetLocationURI returns a Location URI

#### func  RemoveLeadingSlash

```go
func RemoveLeadingSlash(path string) string
```
RemoveLeadingSlash removes leading slash, if any

#### func  RemoveTrailingSlash

```go
func RemoveTrailingSlash(path string) string
```
RemoveTrailingSlash removes trailing slash, if any

#### func  TouchCopy
 
```go
func TouchCopy(writer, reader vfs.File) error
```
TouchCopy is a wrapper around [io.Copy](https://godoc.org/io#Copy) which ensures that even empty source files
(reader) will get written as an empty file. It guarantees a Write() call on the target file.

#### func  UpdateLastModifiedByMoving

```go
func UpdateLastModifiedByMoving(file vfs.File) error
```
UpdateLastModifiedByMoving is used by some backends' Touch() method when a file
already exists.

#### func  ValidateAbsoluteFilePath

```go
func ValidateAbsoluteFilePath(name string) error
```
ValidateAbsoluteFilePath ensures that a file path has a leading slash but not a
trailing slash

#### func  ValidateAbsoluteLocationPath

```go
func ValidateAbsoluteLocationPath(name string) error
```
ValidateAbsoluteLocationPath ensure that a file path has both leading and
trailing slashes

#### func  ValidateRelativeFilePath

```go
func ValidateRelativeFilePath(name string) error
```
ValidateRelativeFilePath ensures that a file path has neither leading nor
trailing slashes

#### func  ValidateRelativeLocationPath

```go
func ValidateRelativeLocationPath(name string) error
```
ValidateRelativeLocationPath ensure that a file path has no leading slash but
has a trailing slash

### type Authority

```go
type Authority struct {
	User, Pass, Host string
}
```

Authority represents host, port and userinfo (user/pass) in a URI

#### func  NewAuthority

```go
func NewAuthority(authority string) (Authority, error)
```
NewAuthority initializes Authority struct by parsing authority string.

#### func (Authority) String

```go
func (a Authority) String() string
```
String() returns a string representation of authority. It does not include
password per https://tools.ietf.org/html/rfc3986#section-3.2.1:

    Applications should not render as clear text any data after the first colon (":") character found within a userinfo
    subcomponent unless the data after the colon is the empty string (indicating no password).
