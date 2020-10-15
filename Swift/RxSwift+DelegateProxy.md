# DelegateProxy

めっちゃ書くこと多い。
ASAuthorizationController.delegate = hogehogehogeをしなくていい。

```swift
@available(iOS 13.0, *)
extension ASAuthorizationController: HasDelegate {
  public typealias Delegate = ASAuthorizationControllerDelegate
  
}

@available(iOS 13.0, *)
extension Reactive where Base: ASAuthorizationController {
  var delegate: DelegateProxy<ASAuthorizationController, ASAuthorizationControllerDelegate> {
    return AuthorizationControllerDelegateProxy.proxy( for: base )
  }
  
  func performRequest() -> Observable<ASAuthorization> {
    let proxy = self.delegate as! AuthorizationControllerDelegateProxy
    
    self.base.delegate = proxy
    self.base.performRequests()

    return proxy.subject
    
  }
}


@available(iOS 13.0, *)
class AuthorizationControllerDelegateProxy: DelegateProxy<ASAuthorizationController, ASAuthorizationControllerDelegate>, DelegateProxyType, ASAuthorizationControllerDelegate {
  
  let subject: PublishSubject<ASAuthorization>
  
  static func registerKnownImplementations() {
    self.register{ AuthorizationControllerDelegateProxy(controller: $0 ) }
  }
  
  init( controller: ASAuthorizationController ) {
    subject = PublishSubject()
    
    super.init(parentObject: controller, delegateProxy: AuthorizationControllerDelegateProxy.self )
  }
  
  func authorizationController(controller: ASAuthorizationController, didCompleteWithAuthorization authorization: ASAuthorization){
    subject.on( .next( authorization ) )
  }

  func authorizationController(controller: ASAuthorizationController, didCompleteWithError error: Error){
    subject.onError( error )
  }
}

```
