# Pinakamasayang Bahagi ng ReactJS

## Ano nga ba ang ReactJS?

Ito ay isang Javascript Framework na minimaintain ng Facebook. Si __Jordan Walke__ ang nag-imbento nito na isang Software Engineer sa Facebook. Ang pangunahing layunin ng Framework na ito ay makagawa ng simple at functional User Interface na walang kahirap hirap. 

---


## Ano ba ang mga pangunahing requirements or prerequisites bago mag-simula at pag aralan ito? 


	- ES6/ES5 
	- Good to excellent understanding ng Object Oriented
	- Basic Understanding ng HTML and CSS
	- NPM or any package managers, kung may nodeJs na kayo don't worry kasi kasama na ang npm modules doon.
		* Download Link if wala pa kayong nodeJS
		* https://nodejs.org/en/download/
	- Basic knowledge of version control like GIT or 
		* https://git-scm.com/downloads - Download GIT
		* https://github.com/ - Create your account in Github

	* Warning lang kung hindi pa ganun ka lawak ang pagkakaintindi mo sa javascript wag ka munang mag jump dito, kasi on my own experience nahirapan ako kasi nagmadali akong matuto neto I dont want you to experience this. Wag ninyong i-rush ang sarili nyo hanggat wala kayong Good understanding sa react, and if may strong knowledge na kayo about javascript sobrang dali nalang magsimula dito.

---


## ReactJS Installation

Mayroon ibat ibang paraan para mag-create ng react Application pero ang ibibigay ko na example ay ang pinakamadaling paraan ng pag-install sa ating PC or laptops.

- Una magcreate kayo ng Folder or Directories sa PC or Laptop nyo kung saan gusto mo i-install ang iyong react app.

- After that mag open kayo ng Terminal nyo or Command prompt then I navigate nyo sa folder na ginawa nyo and type this command

```
	npx create-react-app my-app
```
	* NOTE lang ang "my-app" ay pwede nyong palitan ng any name na gusto nyo kasi ito ang magiging pangalan ng folder kung saan nya ilalagay ang mga installation.

Ang ginagawa ng command na ito ay mag install ng mga Bundlers, Compiler, Packages sa directory na na-specify natin. Para makapagfocus nalang tayo sa development process at hindi na natin intindihin ang mga javascript tool and configuration sa ating gagawing applications. 

Kapag natapos na ang installation mag-nanavigate tayo sa ating directory na "my-app"
```
	cd my-app
```

Mapupunta tayo sa current directory ng ating applications and may makikita tayong mga nakainstall dito, pero dont worry about this and Public and Src folder lang tayo magfofocus dito.

To start running your app sa local server just type this sa Terminal ng root directory nyo.
```
	npm run start
```

And it will automatically navigate you sa ating react Applications. Yey its our first React App.