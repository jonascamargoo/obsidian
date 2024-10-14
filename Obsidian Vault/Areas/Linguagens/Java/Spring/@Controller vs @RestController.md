
O @Controller retorna um html, quanto o @RestController retorna um xml ou JSON. Na verdade, para retornarmos um JSON ou XML usando apenas o @Controller, deveriamos declarar um @ResponseBody em cada método http. O @RestController é a combinação de ambo


Exemplo do @Controller
```java
@Controller 
public class MyController {  
  
	@Autowired  
	private MyService myService;  
	  
	@RequestMapping("/hello")  
	public String sayHello(Model model) {  
		model.addAttribute("message", myService.getHelloMessage());  
		return "hello";  
	}  
}
```

Exemplo do @RestController
```java
@RestController  
public class MyRestController {  
  
	@Autowired  
	private MyService myService;  
	  
	@RequestMapping("/greeting")  
	public Greeting getGreeting() {  
		return myService.getGreeting();  
	}  
}
```