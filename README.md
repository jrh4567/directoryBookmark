# Directory Bookmark  
### aka dbm

dbm is an addition to your .bashrc or .zshrc that adds the ability to bookmark directories. 

dbm stores this list of directories as a plaintext file at `~/.dbmlist`. 

### Installation:
Copy and paste the following code into your .zshrc or similar:
```
dbm() {
	case $1 in
	-h)
		echo "usage:"
		echo "dbm -h\tdisplay this message"
		echo "dbm -m [path]\tadd a mark to the list"
		echo "dbm -p\tshow path to file containing the list of directories"
		echo "dbm -l list all bookmarks"
		echo "dbm [bookmark index]\tcd to that index"
		;;
	-p)
		echo "~/.dbmList"
		;;
	-m)
		echo "$2" >> ~/.dbmList
		;;
	-l)
		i=0
		while read -r line; do
			echo "${i}: $line"
			i+=1
		done < ~/.dbmList
		;;
	[0-99])
		i=0
		while read line; do
			case $i in $1) echo "$line"; cd "$line"; break;; esac
			i=$(( i + 1 ))
		done < ~/.dbmList
	esac
}

```

### Usage:
dbm -h	display this message  
dbm -m [path]	add a mark to the list  
dbm -p	show path to file containing the list of directories  
dbm -l list all bookmarks  
dbm [bookmark index]	cd to that index  