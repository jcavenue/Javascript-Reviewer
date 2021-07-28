
# Ang mahirap na bahagi ng Object Oriented Javascript - Taglish Version ng the Hard Parts

## Creating objects

### Technique 1
* Object literal

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

There is some corner case about this kasi kapag ginamit natin ang ganitong proseso hindi natin nasusunod ang rule ng **DRY Principle** na ang ibig sabihin ay **"do not repeat yourself"**. As you can see the following code above, inuulit lang natin ang method increment which means nagiging redundant na. Iniiwasan lang natin na humaba ang bilang ng ating code at ang Goal is to create an object na ma-rereused ang method or function without hard coding ng paulit-ulit. For example gusto nating gumawa ng 500 user? Baka mawalan kana ng gana mag code.

---
## Ano ba ang dapat nating gawin?


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

Pero sa pamamagitan ng ganitong proseso nasusunod pa ba natin ang rule ng **DRY principle**? hindi, dahil sa bawat pag-gawa natin ng bagong Object, patuluy pa rin nating inuulit ang function declaration sa bawat isang object na ginawa natin.

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

	const user6 = new generateUser('Trisha', 25);
	user6.increment();
```

As soon as we create a new object newUser there is a hidden property created along side with it, which is what we called "**__ proto __**" under the hood there is a linked to the userFunctionStore Object that we can use to access the method inside it. Our end goal is now established when creating an object and this is very simple and straight forward.





