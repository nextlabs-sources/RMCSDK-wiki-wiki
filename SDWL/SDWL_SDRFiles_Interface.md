SDWL Files Interface for local Files Information

```C++

```

## Local Files Class ##


```
#!c++

class ISDRFiles
{
public:
	ISDRFiles() { };
	virtual ~ISDRFiles() { };
	virtual size_t GetListNumber() = 0;
	virtual std::vector<std::wstring> GetList() = 0;
	virtual ISDRmNXLFile* GetFile(int index) = 0;
	virtual ISDRmNXLFile* GetFile(std::wstring& filename) = 0;
	virtual bool RemoveFile(ISDRmNXLFile* file) = 0;

};


```


## Local Files Interface ##

```
#!c++
size_t GetListNumber();
/// Get files list number
/**
* @return size of files
*/
```

```
#!c++
std::vector<std::wstring> GetList();
/// Get files list
/**
* @return array of files
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
*     file		ISDRmNXLFile class reference
* @return true if file removed success or return fail.
*/
```