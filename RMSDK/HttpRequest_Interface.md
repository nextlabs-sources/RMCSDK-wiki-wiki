[HOME](Home)
# RMCCore SDK HTTPRequest Interface #

## HTTPRequest Interface class definition ##
```
#!c++
namespace RMSDK {
    class HTTPRequest
    {
    public:
        HTTPRequest();
        virtual ~HTTPRequest(); {}
        
        inline const std::string& GetMethod();
        inline const std::string& GetURL();
        inline const http::headers& GetHeaders();
        inline const http::accept_types& GetAcceptTypes();
        inline const http::cookies&GetCookies();
        inline const size_t GetBodyLength() ;
        inline const std::string& GetBody();  

        HTTPRequest& operator = (const HTTPRequest& rhs);
    public:
        bool AddHeader(http::header header);
        bool RemoveHeader(std::string headername);
        bool AddCookie(http::cookie cookie);
        bool RemoveCookie(std::string cookiename);
    };
}
```

## RestfulBase Interface Functions ##
```
#!c++
	const std::string& GetMethod();/// Get HTTP request Method
	/**
        * @return
        *    string of method
	*/

See RMSDK::http::methods for list of HTTP method defines.
```
  

```
#!c++
	const std::string& GetURL();/// Get HTTP request full URL
	/**
        * @return
        *    string of Full URL of HTTP Request
	*/
```

```
#!c++
	const http::headers& GetHeaders();/// Get HTTP Request Headers
	/**
        * @return
        *    vector of HTTP headers if any
	*/
See RMSDK::http::header_names for list of HTTP header name defines. 
```
 

```
#!c++
	const http::accept_types& GetAcceptTypes();/// Get HTTP Request accept Types
	/**
        * @return
        *    vector string of HTTP types 
	*/
See RMSDK::http::mimi_types for list of HTTP types defines. 
```
 

```
#!c++
	const http::cookies&GetCookies();/// Get HTTP request cookies
	/**
        * @return
        *    vector of HTTP cookies if any
	*/
```

```
#!c++
	const size_t GetBodyLength();/// Get length of Body
	/**
        * @return
        *    length of HTTP body
	*/
```

```
#!c++
	const std::string& GetBody();/// Get HTTP Body content
	/**
        * @return
        *    string of HTTP Body.
	*/
Note: HTTPRequest class only return string for HTTP body. 
```
```
#!c++
	bool AddHeader(http::header header);/// Add header into the list
	/**
        * @param
        *    header  header want to add in list
        * @return
        *    true if header is added
	*/
Note: if the header name already exists, the header will be replaced with new value
```
	
```
#!c++
	bool RemoveHeader(std::string headername);/// remove header in the list by name
	/**
        * @param
        *    headername  name of header want to be deleted
        * @return
        *    true if the header is deleted
	*/

```
	
```
#!c++
	bool AddCookie(http::cookie cookie);/// Add cookie into the list
	/**
        * @param
        *    cookie  cookie want to add in list
        * @return
        *    bool if cookie is added
	*/
Note: if the cookie name already exists, the cookie will be replaced with new value
```
	
```
#!c++
	bool RemoveCookie(std::string cookiename);/// remove cookie in the list by name
	/**
        * @param
        *    cookiename  name of the cookie want to be deleted
        * @return
        *    true if the cookie is deleted
	*/
```