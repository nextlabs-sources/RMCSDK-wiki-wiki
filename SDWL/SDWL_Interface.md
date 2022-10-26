[HOME](Home)
# SDWL Library Interface #


## Interfaces ##
```
#!c++
DWORD SDWLibGetVersion(void);
/// Return the version number of the module.
/**
* @return
*    The format of version is AABBCCCC major.minor.build.
*/
```

```
#!c++
SDWLResult SDWLibCreateSDRmcInstance(const WCHAR * sdklibfolder, const WCHAR * tempfolder, ISDRmcInstance ** pInstance, char * clientid = NULL, uint32_t id = 0);
/// Create an ISDRmcInstance instance.
/**
 * @param
 *    sdklibfolder      fullpath of top folder of RMD SDK library files
 *    tempfolder        fullpath of temporary folder for RMD SDK library
 *    pInstance         return ISDRmcInstance pointer.  If ISDRmcInstance pointer is NULL, check return result;
 *    clientid          internal use only
 *    id                internal use only
 * @return
 *          SDWL_NOT_ENOUGH_MEMORY      not enough memory
 * @post
 *    SDWLibDeleteRmcInstance must be called to delete this instance.
 *
 * Note: One ISDRmcInstance instance should be used for one user only.  It should not be re-used for a different user.
 */
```

```
#!c++
SDWLResult SDWLibCreateSDRmcInstance(const CHAR * productName, uint32_t productMajorVer, uint32_t productMinorVer, uint32_t productBuild, const WCHAR * sdklibfolder, const WCHAR * tempfolder, ISDRmcInstance ** pInstance, char * clientid = NULL, uint32_t id = 0);
/// Create an ISDRmcInstance instance, and allow software update checking later.
/**
 * @param
 *    productName       name of product
 *    productMajorVer   major version number of product
 *    productMinorVer   minor version number of product
 *    productBuild      build number of product
 *    sdklibfolder      fullpath of top folder of RMD SDK library files
 *    tempfolder        fullpath of temporary folder for RMD SDK library
 *    pInstance         return ISDRmcInstance pointer.  If ISDRmcInstance pointer is NULL, check return result;
 *    clientid          internal use only
 *    id                internal use only
 * @return
 *          SDWL_NOT_ENOUGH_MEMORY      not enough memory
 * @post
 *    SDWLibDeleteRmcInstance must be called to delete this instance.
 *
 * Note: One ISDRmcInstance instance should be used for one user only.  It should not be re-used for a different user.
 */
```

```
#!c++
void SDWLibDeleteRmcInstance(ISDRmcInstance *pInstance);
///Delete an ISDRmcInstance instance.
/**
 * @pre
 *    SDWLibCreateSDRmcInstance must have been called to created this instance.
 * @param
 *    pInstance     ISDRmcInstance instance.
 */
```
