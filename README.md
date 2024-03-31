# How to download a file using this library
First, take the file `activedl.htc` from this repository and put it in the directory containing your HTA, then follow these steps:

1. Specify an `xmlns:c` attribute in the `<html>` element.

```
<html xmlns:c>
...
</html>
```

2. Add the following Import statement to the `<head>` section.

```
<?import namespace="c" implementation="activedl.htc" ?>
```

3. Also add a `<c:activedl>` element to the `<head>` section. You must assign an `id` to this element so you can access this element in script, call its methods, and read/write its properties.

```
<c:activedl id="lib" />
```

4. In script, call the `download` method, passing it the URL from which you want to download the file. Then the file starts downloading, and the `download` method returns immediately.

```
lib.download("https://www.rarlab.com/rar/winrar-x32-700.exe");
```

5. Define a handler for the `oncomplete` event. When the download completes, this event fires, the resulting file is stored in the **Temporary Internet Files** directory, and the `event.filePath` property returns its full path, which can be used by the event handler to copy the file to any desired location. Moreover, if the file contains text (not binary data), the `event.fileContent` property returns its text content.

```
lib.oncomplete = function() {
    var fso = new ActiveXObject("Scripting.FileSystemObject");
    fso.CopyFile(event.filePath, "D:\\winrar-setup.exe");
};
```