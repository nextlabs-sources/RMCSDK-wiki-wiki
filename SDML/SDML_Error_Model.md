[HOME](Home.md)

# Error Code #


```swift
public enum SDMLError: Error {
    
    case undefine
    
    public enum FetchRMSFailureReason {
        case cannotChangeTenantAfterLogin
        case invalidRouterTenant
    }
    
    public enum LoginFailureReason {
        case missingRequiredParameters
        case incorrectUsernamePassword
        case accountNotExist
        
        case noTenant
        case loadDBFailed(error: Error?)
    }
    
    public enum ProtectFailureReason {
        case getTokenFailed
        case storeDBFailed
        case encyptFailed
    }
    
    public enum UploadFailureReason {
        case getFileContentFailed(error: Error?)
        case serverFailed(error: Error?)
    }
    
    public enum CacheFailureReason {
        case invaildParentPath
        case searchFileFailed
        case deleteFileFailed(error: Error?)
        case getDecyptTokenFailed
        case decyptFailed(error: Error?)
        case updateRecipientFailed(error: Error?)
    }
    
    public enum logFailureReason {
        case noLocalList
        case saveLogFailed
    }
    
    public enum myvaultFailureReason {
        case getUsageFailed
    }
    
    public enum CommonFailedReason {
        case networkUnreachable
        case fileNotFound
        case notLogin
        case createFolderFailed(error: Error?)
        case invalidEmail
    }
    
    case fetchRMSFailed(reason: FetchRMSFailureReason)
    case loginFailed(reason: LoginFailureReason)
    case protectFailed(reason: ProtectFailureReason)
    case uploadFailed(reason: UploadFailureReason)
    case cacheFailed(reason: CacheFailureReason)
    case activityLogFailed(reason: logFailureReason)
    case logoutFailed
    case myvaultFailed(reason: myvaultFailureReason)
    
    case commonFailed(reason: CommonFailedReason)
}

```
