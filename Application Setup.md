## Sites to host
* `Admin Settings`
* `ARCONAPIGateway`
* `ARCONMicroservicesStack`
* `ARCONPAMAPI`
* `ARCONUI`
* `ARCOSClientManagerOnline`
* `ARCOSUserAccessLogViewerWeb`


* Add website
	* `ARCOSClientManagerOnline`







* Add license key in `C:\Arcon Solutions\ARCOSClientManagerOnline\DBSetting\ARCONLicenseApp`
```txt
# PAM 1 [4.8.5.0](http://4.8.5.0 "http://4.8.5.0/") U10 and above License (id: 1744631475774)  
b9e4ab1e4f25529b7763d2c4356f65039ec76163f737adb5bdb6ac913988  
ba9646c6ad3ed1bf60312e42e60bbf7cd5d0f9a585bf131e23197cd9fcb7  
3238937c623068b1d7bdecc76c1b208bf14a7742c81c1ec7fcd2f731dc85  
81a7ff7aa5459332f26d08a1b5e7b1bfc00b2bf170dbfc6bd014ee873fc2  
410172916ad73c2c2667fd369d45dbca116c89c6342fd3a1286dd2e757a1  
2618c9ee2f39e5986aa05715bb7d9822c4f22f0508017b155438177daba0  
5fa5a4b41b3f8e0131236a2957e5ba7c183e91e246d3f55e88cb78578801  
73641c6a4372589ef0ad0fae8075c52b17630b46462f36bddca6bf08dc9f  
371017709c796c9c28e1da30346304c20a1d2fbca87eb4b80bfe23b67016  
0d6d7a796ed653b855b145f5fa6b045a9d548ddde87c29bacd1187bedefb  
b6c19e895373c4c3bbc825a7c6d53c3391ff0055f7fe2245a5fed86d68ed  
9ae39ef3efeecd334ba2d27ce5a6765768e0242ae3821443730a9465d4d8  
48053b07e09f56ccd56611ede9abed2dcd88ddae3041b342a376d2065c49  
e4e4f840f20cc198ac5aaf735783b42161751d0039ac81e93f732a99f0d0  
4b7150fe3ce0815243965bc1af701a42e840aa17165f1a2cdffc97cfbd8f  
813f53e2f670db4016a56ef04b0aaa58f8904e823f2c4f2d10b61eef891a  
77b9579ef08467e6c0b4565a1e6e866d7b64a0e3916c037e365e336678b4  
9a0368db12de772b16d8545b5f836f389e08e9549d46ce5c00df6590bb14  
146fd9bdd0b146bf69144e0526d5c6be372e386a7131c296266954b3ee91  
1e475d79b42ddb0a043685f2b39164ed0b60603a52a1850e559325acb496  
447e357c0147f97a5bfa4932531e77a6fe27d440645a45861e23d448b446  
fa699393b29943459253da8c33f322302ddf8cf497b960a348f9341ae4f2  
2b563f400d91fec7dcf53a625df9d2e650317a7a84a9a5b35dd0274beb45  
20a060cc0412162de5b7f06373760a7e6597cb5845fd8734d2ee9944a9a1  
e5e9c0252c05d1e190f046b99e637c852dfdace433452661cc3c4d70c37f  
34f965c0b34d52c73cbfde4ef44cbe3732eb705806ac0900f64f
```

* To host and run web applications install these files in `C:\Newfolder\U16_SP2_B35.8.24_OCI\Tools` 
	* `dotnet-hosting`
	* `dotnet-sdk`
	* `NDP47-KB3186497-x86-x64-AllOS-ENU`
	* `rewrite_amd64`
	* `vc_redist.x64`
	* `vc_redist.x86`

* For login we have to add URL in `C:\Arcon Solutions\ARCOSClientManagerOnline\web.config`
	* Search "domain" by pressing `ctrl + F`
		* Replace `.arconnet.com` with `hardik.local.com` in `value` field.
	* Save the file.
* For accessing `ARCONAPIGateway`
	* Go into `C:\Arcon Solutions\ARCONAPIGateway\ocelot.json`
		* Replace Port `865` with Port `8080` which is assigned to `ARCONMicroservicesStack`.
		* Replace default host URL with `localhost`. 
		* Replace `https` with `http`.
* For accessing password module, make changes in the following files:
	* Go into `C:\ArconSolutions\ARCONMicroservicesStack\commonAPI\auth\appsettings`
		* Replace this line
			* `"XWDWEBURL": "https://hardik.local.com/ARCONAPIGateway/xwdui/#/dashboard"`
	* Go into `C:\Arcon Solutions\ARCONUI\XWDUI\assets`
		* Replace `"UslcBWKfTo9T6NZ1I+IdEg==": "https://u16hf.arconnet.com:1302/frmLoginACMO.aspx"` with 
		* Replace `"8SLE9u6FkJgVqJBAaGU//Q==": "https://u16hf.arconnet.com:1302/ARCONAPIGateway"` with `"8SLE9u6FkJgVqJBAaGU//Q==": "https://hardik.local.com/:1302/ARCONAPIGateway",`
	* Go into `C:\Arcon Solutions\ARCOSClientManagerOnline\SAML\samlSPEntities`
		* Replace `"ConsumerServiceUrl": "https://u16hf.arconnet.com:1302/ARCONAPIGateway/auth/api/saml/Auth"` with `"ConsumerServiceUrl": "https://hardik.local.com/ARCONAPIGateway/auth/api/saml/Auth"`
		* Replace `"TargetUrl": "https://u16hf.arconnet.com:1302/ARCONAPIGateway/auth/api/saml/Auth"` with `"TargetUrl": "https://hardik.local.com/ARCONAPIGateway/auth/api/saml/Auth"`
* To create users:
	* Add new applications in application list in `ACMO`
		* `ARCON MS API`: `https://hardik.local.com/ARCONAPIGateway/`
		* `ARCON Internal API`: `	https://api.hardik.local.com:8443/`
		* 
`