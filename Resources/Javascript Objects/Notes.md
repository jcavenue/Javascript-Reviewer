
# Ang mahirap na bahagi ng Object Oriented Javascript 

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

There is some corner case about this kasi kapag ginamit natin ang ganitong proseso masiado rin siyang matrabaho at hindi natin nasusunod ang rule ng **DRY Principle** na ang ibig sabihin ay **"do not repeat yourself"**. As you can see the following code above, if we want to create 500+ new user masiadong matrabaho at hindi ganun kasimple.

---
## Ano ba ang dapat nating gawin?
Ang end goal lang natin is to bundle all this, na kapag nag create tayo ng new object ay magawa parin nating mareused ung mga function or methods na hindi kaylangang na ilagay natin sa loob ng object na ginawa pero kaya parin nating maaccess ung mga methods to reused this.


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

As soon as we create a new object newUser there is a hidden property created along side with it, which is what we called "**__ proto __**". Itong properties na to ay nakaset ang value sa object.prototype na isang linked para maaccess ung mga properties sa parent object or function.





