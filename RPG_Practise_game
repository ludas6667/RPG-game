import os, random, math

run = True
menu = True
play = False
rules = False
key = False
fight = False
standing = True
buy = False
speak = False
boss = False
guard = False

HP = 50
HPMAX = HP
Level = 1
XP = 0
XPNEED = 10
ATK = 3
pot = 2
elix = 1
gold = 0
x = 0
y = 0

    #   x = 0        x = 1       x = 2       x = 3       x = 4       x = 5         x = 6
map = [ ["plains",   "plains",     "plains",   "plains",   "forest",   "mountain", "cave"], # y = 0
        ["forest",   "forest",   "forest",   "forest",   "forest",   "hills",  "mountain"], # y = 1
        ["forest",   "fields",   "bridge",   "plains",    "hills",    "castle",   "hills"], # y = 2
        ["plains",    "shop",    "town",    "mayor",    "plains",   "hills",   "mountain"], # y = 3
        ["plains",   "fields",   "fields",   "plains",  "hills",  "mountain",  "mountain"]] # y = 4

y_len = len(map)-1
x_len = len(map[0])-1


biom = {
    "plains": {
        "t": "PLAINS",
        "e": True},
    "forest": {
        "t": "WOODS",
        "e": True},
    "fields": {
        "t": "FIELDS",
        "e": False},
    "bridge": {
        "t": "BRIDGE",
        "e": True},
    "town": {
        "t": "TOWN CENTER",
        "e": False},
    "shop": {
        "t": "SHOP",
        "e": False},
    "mayor": {
        "t": "MAYOR",
        "e": False},
    "cave": {
        "t": "CAVE",
        "e": False},
    "mountain": {
        "t": "MOUNTAIN",
        "e": True},
    "hills": {
        "t": "HILLS",
        "e": True},
    "castle": {
            "t": "CASTLE",
            "e": False}

}

e_list = ["Goblin", "Orc", "Slime"]

mobs = {
    "Goblin": {
        "hp": 15,
        "at": 3,
        "go": 8,
        "xp": 2
    },
    "Orc": {
        "hp": 35,
        "at": 5,
        "go": 18,
        "xp": 5
    },
    "Slime": {
        "hp": 30,
        "at": 2,
        "go": 12,
        "xp": 3
    },
    "Werewolf": {
        "hp": 65,
        "at": 9,
        "go": 40,
        "xp": 15},
    "guard": {
        "hp": 40,
        "at": 4,
        "go": 20,
        "xp": 5}

}
def clear():
    os.system("clear")
if os.name == 'posix':
    os.environ['TERM'] = 'xterm'

def draw():
    print("Xx---------------------xX")

def save():
    list =  [
        name,
        str(HP),
        str(ATK),
        str(pot),
        str(elix),
        str(gold),
        str(x),
        str(y),
        str(key),
        str(Level),
        str(XP),
        str(XPNEED)
    ]


    f = open("load.txt", "w")

    for item in list:
        f.write(item + "\n")
    f.close()

def heal(amount):
    global HP
    if HP + amount < HPMAX:
        HP += amount
        print(name + " was healed to " + str(HP) + "hp!")
    else:
        HP = HPMAX
        print(name + " was healed to " + str(HP) + "hp!")

def levelup():
    global XP, XPNEED, HP, HPMAX, ATK, Level

    if XP >= XPNEED:
        print("You have leveled up")
        XP = 0
        XPNEED = math.ceil(XPNEED * 1.2)
        HP = HP + 5
        HPMAX = HPMAX + 5
        ATK = ATK + 1
        Level = Level + 1



def battle():
    global fight, play, run, HP, pot, elix, gold, standing, boss, guard, Level, XP, XPNEED, map
    if map[y][x] == "cave":
        enemy = "Werewolf"
    elif map[y][x] == "castle":
        enemy = "guard"
    else:
        enemy = random.choice(e_list)
    hp = mobs[enemy]["hp"]
    hpmax = hp
    atk = mobs[enemy]["at"]
    go = mobs[enemy]["go"]
    xp = mobs[enemy]["xp"]

    while fight:
        clear()
        draw()
        print("Defeat the " + enemy + "!")
        draw()
        print(enemy + "'s HP: " + str(hp) + "/" + str(hpmax))
        print(name + "'s HP: " + str(HP) + "/" + str(HPMAX))
        print("Potions: " + str(pot))
        print("Elixirs: " + str(elix))
        draw()
        print("1 - Attack")
        if pot > 0:
            print("2 - Use POTION (30hp)")
        if elix > 0:
            print("3 - Use ELIXIR " + "(" + str(HPMAX) + "HP)")
        draw()

        choice = input("#  ")

        if choice == "1":
            hp -= ATK
            print(name + " dealt " + str(ATK) + " Damage to " + enemy + ".")
            if hp > 0:
                HP -= atk
                print(enemy + " dealt " + str(atk) + " Damage to " + name + ".")
                input(">  ")
        elif choice == "2":
            if pot > 0:
                pot -= 1
                heal(30)
                HP -= atk
                print(enemy + " dealt " + str(atk) + " Damage to " + name + ".")
            else:
                print("You have no potions left")
            input(">   ")

        elif choice == "3":
            if elix > 0:
                elix -= 1
                heal(HPMAX)
                HP -= atk
                print(enemy + " dealt " + str(atk) + " Damage to " + name + ".")
            else:
                print("You have no elixir left")
            input(">   ")

        if HP <= 0:
            print("The " + enemy + " has defeated " + name)
            run = False
            play = False
            fight = False
            print("GAME OVER")
            input(">   ")

        if hp <= 0:
            draw()
            print(name + " has defeated " + enemy)
            fight = False
            gold += go
            print("You have found " + str(go) + " gold")
            XP += xp
            print(f"You have gained {xp} xp")
            if random.randint(0,100) <= 20:
                pot += 1
                print("You have found a potion")
            if enemy == "Werewolf":
                print("Congratulations! You have defeated the werewolf and saved the village.")
                boss = False
                play = False
                run = False
            if enemy == "guard":
                clear()
                draw()
                print("Congratulations! You have killed the guard. Your reward is a potion or an Elixir")
                draw()
                print("1 - POTION")
                print("2 - ELIXIR")

                choice = input("#  ")

                if choice == "1":
                    pot += 1
                    print("You have gained 1 POTION")
                    guard = False
                elif choice == "2":
                    elix += 1
                    print("You have gained 1 ELIXIR")
                    guard = False
            input(">  ")
            standing = True
            clear()
            levelup()

def shop():
    global buy, gold, pot, elix, ATK, HP, HPMAX

    while buy:
        clear()
        draw()
        print("Welcome to the store")
        draw()
        print("GOLD: " + str(gold))
        print("POTIONS: " + str(pot))
        print("ELIXIRS: " + str(elix))
        print("ATK: " + str(ATK))
        draw()
        print("1 - Buy POTION (30HP) - 5 GOLD")
        print("2 - Buy ELIXIR (" + str(HPMAX) + "HP) - 8 GOLD")
        print("3 - Upgrade Weapon (+2 ATK) - 10 GOLD")
        print("4 - Silver Heart (+25 HP) - 10 GOLD")
        print("5 - LEAVE")
        draw()

        choice = input("#  ")

        if choice == "1":
            if gold >= 5:
                pot += 1
                gold -= 5
                print("You have bought a potion")
            else:
                print("You do not have enough gold")
            input(">  ")
        elif choice == "2":
            if gold >= 8:
                elix += 1
                gold -= 8
                print("You have bought an elixir")
            else:
                print("You do not have enough gold")
            input(">  ")
        elif choice == "3":
            if gold >= 10:
                ATK += 2
                gold -= 10
                print("You have upgraded your weapon")
                input(">  ")
            else:
                print("You do not have enough gold")
                input(">  ")
        elif choice == "4":
            if gold >= 10:
                HP += 25
                HPMAX += 25
                gold -= 10
                print("You have bought a silver heart upgrade")
                input(">  ")
            else:
                print("You do not have enough gold")
                input(">  ")
        elif choice == "5":
            buy = False
            print("You have left the shop")


def mayor():
    global speak, key
    while speak:
        clear()
        draw()
        print("Hello there " + name + "!")
        if ATK < 5:
            print("You are not strong enough to face the werewolf that terrorises our town, you will need atleast 5 ATK")
            key = False
        else:
            print("If you would like to help us kill the werewolf then head to the cave and kill him for us. Here is the key for the werewolf's lair.")
            key = True
        draw()
        print("1 - LEAVE")
        draw()

        choice == input("#  ")

        if choice == "1":
            speak = False

def cave():
    global boss, key, fight
    while boss:
        clear()
        draw()
        print("You stand before the werewolf's den. What will you do?")
        draw()
        if key:
            print("1 - Use the key to open the door to the lair")
        print("2 - Turn back and leave")

        choice = input("#  ")
        if choice == "1":
            if key:
                fight = True
                battle()
            else:
                print("You do not have the key")

        elif choice == "2":
            boss = False

def castle():
    global fight, guard
    while guard:
        clear()
        draw()
        print("You should not be here, prepare to die")
        draw()
        input(">  ")
        fight = True
        battle()





while run:
    while menu:
        clear()
        draw()
        print("1, NEW GAME")
        print("2, LOAD GAME")
        print("3, RULES")
        print("4, QUIT GAME")
        draw()

        if rules:
            print("Your goal is to kill the werewolf in the cave")
            rules = False
            choice = ""
            input(">")


        choice = input("#  ")

        if choice == "1":
            clear()
            name = input("# Welcome dear traveler, what is your name? ")
            menu = False
            play = True
        elif choice == "2":
            try:
                clear()
                f = open("load.txt", "r")
                load_list = f.readlines()
                if len(load_list) == 12:
                    name = load_list[0][:-1]
                    HP = int(load_list[1][:-1])
                    ATK = int(load_list[2][:-1])
                    pot = int(load_list[3][:-1])
                    elix = int(load_list[4][:-1])
                    gold = int(load_list[5][:-1])
                    x = int(load_list[6][:-1])
                    y = int(load_list[7][:-1])
                    key = bool(load_list[8][:-1])
                    Level = int(load_list[9][:-1])
                    XP = int(load_list[10][:-1])
                    XPNEED = int(load_list[11][:-1])
                    print("# Welcome back " + name)
                    input(">  ")
                    menu = False
                    play = True
                else:
                    print("#  Corrupt save file")
                    input(">  ")
            except OSError:
                print("#  No loadable file found")
                input(">  ")


        elif choice == "3":
            clear()
            rules = True
        elif choice == "4":
            quit()

    while play:
        save() # autosave
        clear()
        if not standing:
            if biom[map[y][x]]["e"]:
                if random.randint(0,100) <= 30:
                    fight = True
                    battle()

        if play:
            draw()
            print("LOCATION: " + biom[map[y][x]]["t"])
            draw()
            print("Name: " + name)
            print(f"Level: {str(Level)}")
            print("HP: " + str(HP) + "/" + str(HPMAX))
            print(f"XP: {str(XP)}/{str(XPNEED)}")
            print("ATK:" + str(ATK))
            print("POTIONS: " + str(pot))
            print("ELIXIRS: " + str(elix))
            print("GOLD: " + str(gold))
            print("COORDS: ", x, y)
            draw()
            print("0 - SAVE AND QUIT")
            if y > 0:
                print("1 - NORTH")
            if x < x_len:
                print("2 - EAST")
            if y < y_len:
                print("3 - SOUTH")
            if x > 0:
                print("4 - WEST")
            if pot or elix > 0:
                draw()
                print("         HEALING")
            if pot > 0:
                print("5 - Use POTION (30HP)")
            if elix > 0:
                print("6 - Use ELIXIR " + "(" + str(HPMAX) + "HP)")

            if map[y][x] == "shop" or map[y][x] == "mayor" or map[y][x] == "cave" or map[y][x] == "castle":
                print("7 - Enter")
            draw()




            dest = input("#  ")

            if dest == "0":
                menu = True
                play = False
                save()
            elif dest == "1":
                if y > 0:
                    y -= 1
                    standing = False

            elif dest == "2":
                if x < x_len:
                    x += 1
                    standing = False
            elif dest == "3":
                if y < y_len:
                    y += 1
                    standing = False

            elif dest == "4":
                if x > 0:
                    x -= 1
                    standing = False
            elif dest == "5":
                if pot > 0:
                    heal(30)
                    pot -= 1
                else:
                    print("You have no Potions left")
                    standing = True
            elif dest == "6":
                if elix > 0:
                    heal(HPMAX)
                    elix -= 1
                else:
                    print("You have no Elixir left")
                    standing = True
            elif dest == "7":
                if map[y][x] == "shop":
                    buy = True
                    shop()
                if map[y][x] == "mayor":
                    speak = True
                    mayor()
                if map[y][x] == "cave":
                    boss = True
                    cave()
                if map[y][x] == "castle":
                    guard = True
                    castle()


            else:
                standing = True
