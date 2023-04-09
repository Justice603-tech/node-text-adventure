# node-text-adventure
A Text adventure made in `Node.js`!
Its a simple text adventure.
# Story
You wake up in an abandoned underground facility! you have to fight a monster and get out! Its very short and simple. just kill a monster and get out. see.. very simple.

# Source Code
Here is the source code! Modify it To Your Extent! But please credit me in your forked projects / scripts! the comment in the code has been put for easier.
in the comment put `Forked: true`.

The code Is Here:
```javascript
// Node Text Adventure! License: MIT License, By: justice603-tech
import inquirer from "inquirer";
import chalk from 'chalk';
function die(){
    console.log(chalk.redBright("You Died!s"))
}
console.log(chalk.greenBright("Node Text Adventure"))
console.log("================================================")
console.log("You wake up in a room inside an abandoned underground facility. You need to exit this underground facility. there are monsters. be careful. find the lab data and GET OUT!")
var playerhealth = 100
class Inventory{
    constructor(inventory){
        this.inventory = inventory;
    }

    AddItemToInventory(item){
        this.inventory.push(item);
    }

    UseItemFromInventory(item){
        this.inventory.pop(item)
    }

    ViewInventory(){
        console.log(this.inventory)
    }

    UseItemSelection(){
        inquirer
      .prompt([
        {
            type: 'list',
            name: 'inventory',
            message: "What Item do you want to use?",
            choices: [
                "Phone",
                "Pistol",
                "Empty USB Stick"
            ]
               
        }
      ])
      .then((answer) => {
        switch (answer.inventory) {
            case 'Phone':
                console.log(chalk.redBright("Phone Battery Died"));
                this.UseItemSelection()
                break;
            case 'Pistol':
                console.log(chalk.greenBright("You Use Gun!"));
                console.log(chalk.greenBright("You Shot Monster"));
                Entity_1.hurt()
                this.UseItemSelection()
                break;
        }
      })
    }
}

class Monster{
    constructor(name, monsternum, health, attack, defense){
        this.name = name;
        this.monsternum = monsternum;
        this.health = health;
        this.attack = attack;
        this.defense = defense;
    }

    attackfunc(){
        console.log(chalk.redBright(`${this.name} attacks!`))
        playerhealth = playerhealth - this.attack 
        if(playerhealth == 0){
            die()
        }
        console.log(chalk.redBright(`Your Health Reduced to: ${playerhealth}`))
    }

    hurt(){
        this.health =  10 - 10
        console.log(chalk.redBright(`You Damaged ${this.name}! [ENEMY HEALTH]: ${this.health}`))
        if(this.health == 0){
            console.log(chalk.redBright(`${this.name} died!`))
            this.health = 0
            ActionFinal()
        }
    }
}

var inv = new Inventory(['Phone', 'Pistol', 'Empty USB Stick'])
var Entity_1 = new Monster('The Smiler', 1, 34, 10, 10)
function Action(){
    inquirer
  .prompt([
    {
        type: "list",
        name: "action2",
        message: "What do you want to do?",
        choices: [
            "Go to the next room",
            "Go to the previous room",
            "Inventory",
            "Open the room [D-A1]"
        ]
    }
  ])
  .then((answer) => {
    switch (answer.action2) {
        case "Go to the next room":
            console.log("Go to the next room")
            break;
        case "Go to the previous room":
            console.log("Go to the previous room")
            break;
        case "Inventory":
            inv.ViewInventory()
            break;
        case "Open the room [D-A1]":
            console.log("Opened the room [D-A1]")
            console.log(chalk.redBright("The door locks Shut"))
            console.log(chalk.redBright("An entity named: " + Entity_1.name + " Is Coming to attack you"))
            inv.UseItemSelection()
            break;
    }
  })
}
function ActionMain(){
inquirer
 .prompt([
    {
        type: "list",
        name: "action",
        message: "What do you want to do?",
        choices: [
            "Go to the next room",
            "Inventory",
            "Check the drawer",
        ]
        
    }
 ])
 .then((answer) => {
    switch (answer.action) {
        case "Go to the next room":
            console.log("Go to the next room")
            Action()
            break;
        case "Inventory":
              inv.ViewInventory()
              ActionMain()
            break;
        case "Check the drawer":
            console.log(chalk.redBright("Nothing. you found nothing"))
    }
 })
}

function ActionFinal(){
    console.log(chalk.greenBright("You see the Elevator to exit!"))
    inquirer
    .prompt([
        {
            type: "list",
            name: "actionfinal",
            message: "What do you want to do?",
            choices: [
                "Go to the Elevator",
                "Inventory",
            ]
        }])
        .then((answer) => {
          switch(answer.actionfinal){
            case "Go to the Elevator":
                console.log("You Went to go to the Elevator and you Escaped! Congratulations! You Completed the text Adventure Game Made in node.js! Made By: Justice!")
                console.log(chalk.greenBright("You Won!"))
          }
        })
}

ActionMain()
```
