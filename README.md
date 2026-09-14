<div align=center><h1>Bash Utils</h1></div>

<img src="https://github.com/user-attachments/assets/3c7262a2-7962-4082-9588-d65e18bbcf4a" alt="img" width="450" />

<div align=center>A tool for shell scripts. Leverage the power of Bubbles and Lip Gloss in your scripts and aliases without writing any Go or Shell code!</div>

## Customization

You can customize `bash-utils` options and styles with --flags. See `bash-utils` <command> --help for a full view of each command's customization and configuration options.

```bash 
bash-utils input --prompt.foreground "212" \
          --placeholder "What's up?" \
          --prompt "* " \
          --width 80 \
          --value "Not much, hby?"
```

## Input 

Prompt for input with a simple command.

```bash
bash-utils input > answer.txt 
bash-utils input --password > password.txt
```

<img width="1000" height="500" alt="input" src="https://github.com/user-attachments/assets/494bdc8d-b7dd-4dc1-9e7b-639cb9bffc71" />

## Write

Prompt for some multi-line text (ctrl+d to complete text entry).

```bash 
bash-utils write \
    --line-numbers \
    --line-numbers.current.foreground=yellow \
    --line-numbers.current.bold \
    --line-numbers.current.italic \
    --cursorline \
    --line-numbers.current-left \
    --cursor.mode="blink" > story.txt
```

<img width="1000" height="500" alt="write" src="https://github.com/user-attachments/assets/c9c45fed-ec1e-45b5-aa40-51dbe45ca724" />

## Filter

Filter a list of values with fuzzy matching:

```bash 
echo Strawberry >> flavors.txt
echo Banana >> flavors.txt
echo Cherry >> flavors.txt
./bash-utils filter < flavors.txt > selection.txt 
```

<img width="1000" height="500" alt="filter" src="https://github.com/user-attachments/assets/10f835aa-33be-47e4-bf89-30bf47d16763" />


Select multiple options with the `--limit` flag or `--no-limit` flag. Use `tab` or `ctrl+space` to select, enter to confirm.

```bash 
cat flavors.txt | bash-utils filter --limit 2
cat flavors.txt | bash-utils filter --no-limit
```

## Choose

Choose an option from a list of choices.

```bash 
echo "Pick a card, any card..."
CARD=$(./bash-utils choose --height 15 {{A,K,Q,J},{10..2}}" "{♠,♥,♣,♦})
echo "Was your card the ${CARD:?}?"
```

<img width="1000" height="500" alt="choose" src="https://github.com/user-attachments/assets/2e276f6f-6b72-4433-9de9-0cfe35f0ba1e" />


You can also select multiple items with the --limit or --no-limit flag, which determines the maximum of items that can be chosen.

```bash
cat songs.txt | bash-utils choose --limit 5
cat foods.txt | bash-utils choose --no-limit --header "Grocery Shopping"
```

## Confirm

Confirm whether to perform an action. Exits with code 0 (affirmative) or 1 (negative) depending on selection.

```bash 
./bash-utils confirm && rm file.txt || echo "File not removed"
```

<img width="1000" height="500" alt="confirm" src="https://github.com/user-attachments/assets/b4759f3e-2a5a-44a5-ae29-64e19c60a562" />

## File

Prompt the user to select a file from the file tree.

```bash 
bash-utils file \
    --file-size.foreground=yellow \
    --permissions.custom="read.foreground=green,write=yellow,exec=red,dir=blue,socket.foreground=5,pipe.foreground=yellow,pipe.background=#45475a,sticky.foreground=#cba6f7,setuid.foreground=#cba6f7,none.foreground=brightblack" \
    --symlink.foreground=green \
    --directory.foreground=blue \
    --pipe.background=#45475a \
    --pipe.foreground=yellow \
    --socket.foreground=5 \
    --setuid.foreground=37 \
    --setuid.background=41 \
    --icons=eza \
    -a
```

<img width="1000" height="500" alt="file" src="https://github.com/user-attachments/assets/8f27ed23-f4d2-45c5-b625-3baa40b129e0" />


## Pager

Scroll through a long document with line numbers and a fully customizable viewport.

```bash 
 bash-utils pager \
  --input.type="floating" \
  --theme="ansi" \
  --cursor.mode="blink" \
  --show-line-numbers \
  --border.foreground="blue" \
  --line-number.foreground="yellow" \
  --match.background="blue" \
  --match.foreground="clear" \
  --floatinginput.title=" Input " \
  < README.md
```

<img width="1000" height="500" alt="pager" src="https://github.com/user-attachments/assets/3a66758a-8e9d-40be-9466-de3e3f4ad0d2" />


## Spin

Display a spinner while running a script or command. The spinner will automatically stop after the given command exits.

To view or pipe the command's output, use the --show-output flag.

```bash 
bash-utils spin --spinner dot --title "Buying Bubble Gum..." -- sleep 5
```

<img width="1000" height="500" alt="spin" src="https://github.com/user-attachments/assets/8b55486c-a781-4426-8ba8-a36763eb1b23" />


Available spinner types include: `dot`,`line`,`minidot`,`jump`,`pulse`,`points`,`globe`,`moon`,`monkey`,`meter`,`hamburger`,`standard`,`bar`,`process`.

## Table


Show data into terminal with beautifiul output.

```bash 
bash-utils table < flavors.csv | cut -d ',' -f 1 
# Or using files 
ls -lh \
  | awk 'NR>1 {print $1 "," $3 "," $9}' \
  | bash-utils table \
      --columns "Permisos,Propietario,Archivo" \
      --border-foreground=212
```

<img width="1000" height="500" alt="table" src="https://github.com/user-attachments/assets/cf39f4c1-1039-430a-8f11-a0d54495b99a" />


## Style

Pretty print any string with any layout with one command.

```bash 
./bash-utils style \
	--foreground 212 --border-foreground 212 --border double \
	--align center --width 50 --margin "1 2" --padding "2 4" \
	'Bubble Gum (1¢)' 'So sweet and so fresh!'
```

<img width="1000" height="500" alt="style" src="https://github.com/user-attachments/assets/9919b075-5ac5-4d70-87af-cc808f4cbd76" />


## Format

format processes and formats bodies of text. bash-utils format can parse markdown and named emojis.

```bash 
bash-utils format -- """# Bash Utils Formats 

- Markdown 
- Emoji 
- End 
"""
```

This tool can render some HTML

```bash 
bash-utils format -- """<h1>Bash Utils Formats</h1>

<ul>
  <li>Markdown</li>
  <li>Emoji</li>
  <li>End</li>
</ul>"""
```

And render emojis 

```bash 
echo ":flag_pe: :girl: :joy: :cat:" | bash-utils format -t "emoji"
```

<img width="1000" height="500" alt="format" src="https://github.com/user-attachments/assets/6a752e49-016b-4dfa-b9f2-9726ff2d2e2e" />


## Log

logs messages to the terminal at using different levels

```bash 
# Log some debug information.
./bash-utils log --level debug "Creating file..." name file.txt
# DEBUG Unable to create file. name=temp.txt

# Log some error.
./bash-utils log --level error "Unable to create file." name file.txt
# ERROR Unable to create file. name=temp.txt

# Include a timestamp.
./bash-utils log --time rfc822 --level error "Unable to create file."
```

<img width="1000" height="500" alt="log" src="https://github.com/user-attachments/assets/dc9d9be8-cd7f-49de-a5da-22288da74f64" />


## Messagebox 

logs message into box 

```bash 
./bash-utils messagebox \
  --title=" Warn " \
  --type="Warning" \
  --title.align=center \
  --preffix.pad="1 0" \
  --message="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum." \
  --border="rounded" \
  --bold \
  --italic \
  --title.foreground="" \
  --title.background=0 \
  --preffix.background=0 \
  --preffix.foreground=""
```

<img width="1000" height="500" alt="messagebox" src="https://github.com/user-attachments/assets/b9a46ac2-da24-4fe5-99c6-a1c84cbf870e" />


## Text 

Show beautifiul text in terminal, with gradient effect! 

```bash 
bash-utils text "[fg.grad=#AA6EE6,#5A3C96]♥ https://yoodreamer.github.io[end]" --bold --align=center 
```

<img width="1000" height="500" alt="text" src="https://github.com/user-attachments/assets/fdb5f9ef-2cc1-45f8-8355-576694c8ace3" />


## Join

Combine text vertically or horizontally. Use this command with `bash-utils` style to build layouts and pretty output.

```bash 
I=$(bash-utils style --padding "1 5" --border double --border-foreground 212 "I")
LOVE=$(bash-utils style --padding "1 4" --border double --border-foreground 57 "LOVE")
BUBBLE=$(bash-utils style --padding "1 8" --border double --border-foreground 255 "Bubble")
GUM=$(bash-utils style --padding "1 5" --border double --border-foreground 240 "Gum")

I_LOVE=$(bash-utils join "$I" "$LOVE")
BUBBLE_GUM=$(bash-utils join "$BUBBLE" "$GUM")
bash-utils join --align center --vertical "$I_LOVE" "$BUBBLE_GUM"
```

<img width="1000" height="500" alt="join" src="https://github.com/user-attachments/assets/65302bed-01cf-4108-918e-3d053fc887ec" />

---

## Examples

How to use **bash-utils** in your daily workflows:

- Write a commit message:
```bash 
git commit -m "$(bash-utils input --width 50 --placeholder "Summary of changes")" 
```

- Open files in your **$EDITOR**

```bash 
"${EDITOR:?}" $(bash-utils filter)
```

- Pick a commit hash from git history

```bash 
./bash-utils filter <<< $(git log --oneline) | cut -d' ' -f1 
```

- Update packages **(Debian)**

```bash 
apt list --upgradable 2>/dev/null | grep '/' | tail -n10 | awk -F'/' '{print $1}' | ./bash-utils filter --placeholder="Selecciona paquete para actualizar..." --indicator="→"
```
- `sudo` replacement

```bash 
alias please='bash-utils input --password --placeholder "Contraseña para sudo..." --password.toggle-mode="on" | sudo -S ${@}'
```

---

<div align="center">
    A tool inspired by <a href="https://github.com/charmbracelet/gum">gum</a>, I hope you like it!! ^^
</div>
