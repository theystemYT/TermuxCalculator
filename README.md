>[!IMPORTANT]
> Please do notice that this script is copyrighted, and that any part of it being used in anyone else's scripts are not allowed. You can view the [copyright license](https://github.com/theystemYT/TermuxCalculator/blob/main/LICENSE.md) for more information.

>[!TIP]
> Need a tutorial? We got you covered. Press the [blue](example.com) tutorial text!

>[!IMPORTANT]
> Please make sure to exit your current Termux session and make a new one before executing this script. Also, do NOT add spaces when using key words and then adding your equation! When using this script, use a key word, and a equations, but the symbol and equation must not have spaces! (Example: add 1+1), it should be like this, not (add 1 + 1)! Or else, it will return as a invaild function. If you do not understand, you will when executing the script, since it has info about how to use the calculator, and you will encounter "key words".

> Make sure you have notifications enabled on your device with Termux so that Termux always shows a notification when your in a session (and if you close it, it won't pop up again until you close the app and reopen it since the notification shows up only when opening the app), where you can exit the session, by touching Exit on the notification.
> Images of the notification:

>[!TIP]
>Scroll down more to find more information about this script, and other stuff

# Termux Calculator
Welcome to the _Termux Calculator_, an amazing script for people trying to cheat in school. This script is basically just a calculator.
I do not need to explain all the information about this script, since it will be shown when executed. 
The reason why I made this for Termux is because school chromebooks with GoGuardian have Termux able to install, as the Google Play store is very limited on school chromebooks.

Here is the script to run.
```bash
#!/bin/bash
cat << 'EOF' > Calculator.sh
#!/bin/bash
YELLOW="\e[33m"
GREEN="\e[32m"
RED="\e[31m"
BLUE="\e[34m"
RESET="\e[0m"

convert() {
v="$1"
if [[ "$v" =~ ^([0-9]+)\ ([0-9]+)/([0-9]+)$ ]]; then
echo "scale=10; ${BASH_REMATCH[1]} + (${BASH_REMATCH[2]}/${BASH_REMATCH[3]})" | bc
elif [[ "$v" =~ ^[0-9]+/[0-9]+$ ]]; then
echo "scale=10; $v" | bc
else
echo "$v"
fi
}

clear
echo -e "${YELLOW}Running...${RESET}"
sleep 3
clear
echo -e "${GREEN}Welcome to the Termux Calculator by theystemYT!${RESET}"
echo
echo -e "${YELLOW}To use this calculator, use a key word from our list, then the equation. (Example: add 1+1) Then, the answer will show up.
List of key words
Use 'add' for adding
Use 'sub' for subtraction
Use 'multiply' for multiplication
Use 'divide' for division${RESET}"
echo -e "${RED}Notice: If you ever close Termux or you plan to close Termux, please exit the session first! When trying to reexecute the script, it will fail!${RESET}"
echo -e "${BLUE}Notice 2: If this script isn't working, then the script is outdated. You can find the latest version of the script at https://github.com/theystemYT/TermuxCalculator/tree/main${RESET}"
echo

while true; do
echo -ne "${BLUE}> ${RESET}"
read input

op=$(echo "$input" | awk '{print $1}')
expr=$(echo "$input" | sed 's/^[^ ]*//')
expr=$(echo "$expr" | tr -d ' ')
expr=$(echo "$expr" | sed 's/+/ + /;s/-/ - /;s/\*/ * /;s/x/ * /;s/÷/ \/ /;s/\// \/ /')

a=$(echo "$expr" | awk '{print $1}')
b=$(echo "$expr" | awk '{print $3}')
sym=$(echo "$expr" | awk '{print $2}')

if [[ -z "$a" || -z "$b" || -z "$sym" ]]; then
echo -e "${RED}Sorry, this function is invaild!${RESET}"
continue
fi

a=$(convert "$a")
b=$(convert "$b")

case "$op" in
add) res=$(echo "scale=10; $a + $b" | bc) ;;
sub) res=$(echo "scale=10; $a - $b" | bc) ;;
multiply) res=$(echo "scale=10; $a * $b" | bc) ;;
divide)
if [[ "$b" == "0" ]]; then
echo -e "${RED}Sorry, this function is invaild!${RESET}"
continue
fi
res=$(echo "scale=10; $a / $b" | bc)
;;
*)
echo -e "${RED}Sorry, this function is invaild!${RESET}"
continue
;;
esac

echo -e "${GREEN}Answer: $res${RESET}"
done
EOF
chmod +x Calculator.sh
./Calculator.sh
```
If you are interested, here are all the features in this script

<details>
  <summary>Features</summary>

- Addition can be done as well with subtraction, multiplication, and division 
- Decimals can be added, subtracted, multiplied, and divided
- Fractions may work, but it is uncertain 
</details>

# Credits
theystemYT - Ideas and 'fixing' ideas

ChatGPT - Scripter
