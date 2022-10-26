SDWL Files Interface for local Files Information

```C++

```

## Local Files Class ##

ISDRFiles: local files manager. This class will store all the files information under working/user id directory.

```
#!c++

class ISDRFiles
{
public:
	ISDRFiles() { };
	virtual ~ISDRFiles() { };
	virtual void AddFile(ISDRmNXLFile& file) = 0;
	virtual std::vector<std::wstring> GetList() = 0;
        virtual size_t GetListNumber() = 0;
	virtual ISDRmNXLFile* GetFile(int index) = 0;
	virtual ISDRmNXLFile* GetFile(std::wstring& filename) = 0;
        virtual bool RemoveFile(ISDRmNXLFile* file) = 0;
};


```

## Local Files Interface ##

```
#!c++
void AddFile(ISDRmNXLFile& file);
/// Save File 
/**
* @param
*    file		ISDRmNXLFile class
* @return
*			none
*/
```

```
#!c++
std::vector<std::wstring> GetList();
/// Get files list
/**
* This function should be called only once. It will remove previous saved files information.
* @return array of files
*/
```

```
size_t GetListNumber();
/// Get files list number. Need call GetList() first.
/**
* @return size of files
*/

```

```
#!c++
ISDRmNXLFile* GetFile(int index);
/// Get NXL file class by index
/**
* @param
*    index		index to file list
* @return NXL file class
*/
```

```
#!c++
ISDRmNXLFile* GetFile(std::wstring& filename);
/// Get NXL file class by name
/**
* @param
*    filename		file name
* @return NXL file class
*/
```

```
#!c++
bool RemoveFile(ISDRmNXLFile* file);
/// Remove file by class reference
/**
* @param
*    file		ISDRmNXLFile class reference
* @return true if file removed success or return fail.
*
*/
```