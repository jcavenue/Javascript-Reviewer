
# Ang Sekretong bahagi ng Object Oriented Javascript 

## Creating objects

### Technique 1
* Using Object literal

```
	const user1 = {
	name: 'John Carlo Fababeir',
	score: 4,
	increment: function () {
		user1.score++;
		}

	user1.increment(); // score = 5

```
---
### Technique 2
* Use Object dot Notations

```
	const user2 = {} //create an empty object

	user2.name = 'Lara Micaela Noga'; //assign properties to that object
	user2.score = 5;

	user2.increment = function () {
		user2.score++;
	}
```
---

### Technique 3
* Use Object.create

```
	const user3 = Object.create(null);

	user3.name = 'Elorde Fababeir'
	user3.score = 6;

	user3.increment = function () {
		user2.score++;
	}
```
There is some corner case about this kasi kapag ginamit natin ang ganitong mga proseso sa pag-gawa ng object hindi natin maiwasan na humaba ung code structure natin which is iniiwasan natin mangyari at para hindi repetitive ung mga function na ating ginagamit. May mga ilang solusyon para maiwasan natin ito.

---
## Ano ba ang dapat nating gawin?

Ang end goal lang natin is to bundle all this, na kapag nag create tayo ng new object ay magawa parin nating mareused ung mga function or methods na hindi kaylangang na ilagay natin sa loob ng object na ginawa natin, pero kaya parin nating maaccess ung mga methods to reused this. See some examples below.


### Solution 1
* Generate objects using a function

```
	function userCreator (name, score) {
		const newUser = {};
		newUser.name = name;
		newUser.score = score;
		newUser.increment = function(){
		newUser.score++;
		};
		return newUser;
	}

	const user4 = userCreator('Jenny', 10);
	const user5 = userCreator('Manny', 20);

```

Mag-dedeclare tayo ng function kung saan mag-a-accept sya ng dalawang arguments na gagamitin natin sa loob ng ating function. Una mag declare tayo ng const newUser at i-set ang value sa isang empty object sa loob ng ating function. Ngayon gamit ang Object dot notation kaya nating mag-dagdag ng propeties and value sa loob ng ating object. Ipapasa natin ngayon ang ating arguments sa values ng ating properties. Pagkatapos ay irereturn natin ang object na ginawa natin kung saan pwede nating ipasa ang return object sa variables na gusto natin. Ang prosesong ito ay simple lang.

Pero may corner case pa rin tayo. Hindi pa rin natin magawang mareused ung function natin. 

---

### Solution 2
* Using Prototype Chain

```
	function generateUser (name, score){
		const newUser = Object.create(userFunctionStore);
		newUser.name = name;
		newUser.score = score;
		return newUser; // returned out the value of newUser which is an object
	}

	const userFunctionStore = {
		increment: function(){this.score++},
		login: function(){console.log("You're LoggedIn");}
	};

	const user6 = generateUser('Trisha', 25);
	user6.increment();
```

As soon as we create a new object newUser there is a hidden property created along side with it, which is what we called "**__ proto __**". Itong properties na ay pinapalitan ng object.prototype to access functionStore.

---

### Solution 3
* Using the keyword that automate the hard work: new;

```
	function UserCreator(name, score){
		this.name = name;
		this.score = score;
	}

	UserCreator.prototype.increment = function(){
		this.score++;
	};

	UserCreator.prototype.login = function(){
		console.log('Login');
	}

	const user1 = new UserCreator("Eva",9);

	user1.increment();
```

Note: kapag nagdeclare tayo ng function ay hindi lang ito basta isang function dahil meron pa itong kasamang object. Sa loob ng object na to meron tayo regular property na tinatawag na prototype which is isang object. We can access this using dot notation to add some method.

Kapag gumamit tayo ng keyword na **new** mino-mutate nya ung ating execution context kung saan meron syang tatlong hakbang na ginagawa.

- Una it create an empty object call **this** 
- Pangalawa it creates a hidden property which is what we call __ proto __ kung saan nakaset ang values nito sa object.prototype na gumagawa ng bond or linkage sa nt object.prototpe.
- Pangatlo ay gumagawa ito ng automatic return statement that returns the object assigned to **this object**. 

---

### What if we want to organize our code inside one of our shared functions - perhaps by defining a new inner function
* this keyword scoping issues

```
	function UserCreator(name, score){
		this.name = name;
		this.score = score;
	}

	UserCreator.prototype.increment = function(){
		function add() {
			this.score++;
		};
		//const add = function(){this.score++}
		add()
	};

	UserCreator.prototype.login = function(){
		console.log('Login');
	}

	const user1 = new UserCreator("Eva",9);

	user1.increment();
```

Kapag gumawa tayo ng function inside our function and we use the keyword this. hindi siya maassign sa ating object since ang rule na ung nasa left handside ng dot notation dapat automatically na iaasign ang object pero this keyword will be assigned in window object. Ito ung scoping issues when we use this keyword function in functions. it will be misassigned.

To solve this issues we can use arrow function because it binds the function lexically. Where it was save will determine when it will be called. Meron rin ibang paraan para masolve ang issue na to using bind() or self object.

```
	function UserCreator(name, score){
		this.name = name;
		this.score = score;
	}

	UserCreator.prototype.increment = function(){
	
		const add = () => {this.score++};
		add()
	};

	UserCreator.prototype.login = function(){
		console.log('Login');
	}

	const user1 = new UserCreator("Eva",9);

	user1.increment();
```

---

### Solution 4
We're writing our shared methods separately from our object's constructor itself in the user.prototype object but in other languange do it in one place. So JS introduce the class keyword that construct our own object and everytime you list a function inside the class it will be automatically add to the object.prototype object. we can create function inside our class without using the 'function' keyword and without semicolon. The class keyword saved us from writing codes.

```
	class UserCreator{
		constructor(name, score) {
			this.name = name;
			this.score = score;
		}

		increment () {
			this.score++;
		}

		login (){
			console.log('login');
		}
	}

	const user1 = new UserCreator('Jc',10);

	user1.increment();
```

---
 
Ang **Javascript** ay hindi katulad ng ibang Object Oriented Languages dahil naiiba ang implementation nito sa mga counterpart languages. Ang nature ng javascript ay isang **prototypal feature** na kung saan ang *class* keyword are just faking the creation of object. Ang Class keyword ay ginamit dito upang ang manual na pag-gawa ng object and ang pag-insert ng method inside ng ating prototype object ay kusa na niyang ihahandle para satin.

Ano ang benefits nito:
- Emerging as a new standard
- Feels more like style of other language like python etc

Problems:
99% of developers have no idea how it works and therefore fail in the interview.

Sa javascript gumagamit tayo ng tinatawag natin na *dunder proto* which is a hidden propert sa ating objects, functions and array to link to a bunch of bonus functionality na pwede nating magamit some are (Object, Function etc.). This dunder proto has chaining property sa prototype object na kung saan dito nya muna hinahanap ung properties or method na kanyang gagamitin. Lahat ng objects by default ay mayroong dunder proto.

Notes:
- With **Object.create** we override the default __ proto __ to object.prototype and replace with functionStore.

- But functionStore is an object so it has a __ proto __ reference to
Object.prototype - we just intercede in the chain

---

