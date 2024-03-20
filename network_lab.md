
## Network Commands
| Command | Usage | Windows | Linux |
|---------|-------|---------------------|-------------------|
| IPCONFIG | Displays all current TCP/IP network configuration values | `ipconfig /all` | `ifconfig` or `ip addr show` |
| NSLOOKUP | Queries DNS for IP address or domain information | `nslookup <domain>` | `dig <domain>` or `host <domain>` |
| HOSTNAME | Displays the name of the current host | `hostname` | `hostname` |
| PING | Tests the reachability of a host on an IP network | `ping <hostname/IP>` | `ping <hostname/IP>` |
| TRACERT | Traces the route taken by packets across an IP network | `tracert <hostname/IP>` | `traceroute <hostname/IP>` |
| NETSTAT | Displays active TCP/IP connections and listening ports | `netstat` | `netstat` or `ss` |
| ARP | Displays and modifies entries in the ARP cache | `arp -a` | `arp -a` |
| SYSTEMINFO | Displays detailed configuration information about a computer | `systeminfo` | `uname -a` or `cat /etc/*release` |


## Programs

### 1) Write a Shell program to check the given number is even or odd.

     read -p "Enter a number: " num
    ((num % 2 == 0)) && echo "$num is even." || echo "$num is odd."

### 2) Write a Shell program to check a leap year.

    read -p "Enter a year: " year
    if (( (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0) )); then
        echo "$year is a leap year."
    else
        echo "$year is not a leap year."
    fi

### 3) Write a Shell program to find the area and circumference of a circle.

    read -p "Enter radius: " radius
    area=$(echo "scale=2; 3.14 * $radius * $radius" | bc)
    circumference=$(echo "scale=2; 2 * 3.14 * $radius" | bc)
    echo "Area: $area"
    echo "Circumference: $circumference"

### 4) Write a Shell program to check the given number and its reverse are same.

    read -p "Enter a number: " num
    echo "$num" | rev | grep -q "^$num$" && echo "$num is same." || echo "$num is not same."

### 5) Write a Shell program to check the given string is palindrome or not.

    read -p "Enter a string: " str
    echo "$str" | rev | grep -q "^$str\$" && echo "$str is palindrome." || echo "$str is not palindrome."

### 6) Write a Shell program to find the sum of odd and even numbers from a set of numbers.

    read -p "Enter numbers separated by spaces: " nums
    sum_even=$(grep -oE '\b[0-9]*[02468]\b' <<< "${nums[@]}" | paste -sd+ | bc)
    sum_odd=$(grep -oE '\b[0-9]*[13579]\b' <<< "${nums[@]}" | paste -sd+ | bc)
    echo "Sum of even numbers: $sum_even"
    echo "Sum of odd numbers: $sum_odd"

### 7) Write a Shell program to find the roots of a quadratic equation.

    read -p "Enter coefficients (a b c): " a b c
    d=$((b*b-4*a*c))
    echo "Roots are $( [ $d -gt 0 ] && echo "dist." || [ $d -eq 0 ] && echo "equ." || echo "complex." )"
    [ $d -gt 0 ] && bc -l <<< "scale=2; (-$b + sqrt($d)) / (2 * $a)"
    [ $d -gt 0 ] && bc -l <<< "scale=2; (-$b - sqrt($d)) / (2 * $a)"

### 8) Write a Shell program to check the given integer is Armstrong number or not.

    read -p "Enter a number: " num
    s=0; for ((i=0;i<${#num};i++)); do ((s+=(${num:i:1})**${#num})); done
    echo $s | grep -q "$num" && echo "$num is Armstrong." || echo "$num is not Armstrong."

### 9) Write a Shell program to check the given integer is prime or not.

    read -p "Enter a number: " num
    is_prime=true
    for (( i=2; i<num; i++ )); do
        [ $((num % i)) -eq 0 ] && is_prime=false && break
    done
    $is_prime && echo "$num is prime." || echo "$num is not prime."

### 10) Write a Shell program to generate prime numbers between 1 and 50.

    echo "Prime numbers between 1 and 50:"
    for num in $(seq 2 50); do
        if [ $(factor $num | wc -w) -eq 2 ]; then
            echo $num
        fi
    done

### 11) Write a Shell program to find the sum of square of individual digits of a number.

    read -p "Enter a number: " num
    sum=$(echo "$num" | grep -o . | awk '{s+=$1^2} END {print s}')
    echo "Sum of squares of digits: $sum"

### 12) Write a Shell program to count the number of vowels in a line of text.

    read -p "Enter a line of text: " text
    vowel_count=$(echo "$text" | grep -io '[aeiou]' | wc -l)
    echo "Number of vowels: $vowel_count"

### 13) Write a Shell program to display student grades.

    while read -r name marks; do
        grade=$(awk -v m="$marks" 'BEGIN{ grades="FDCBA"; print (m>=90) ? "A" : (m>=80) ? "B" : (m>=70) ? "C" : (m>=60) ? "D" : "F" }')
        echo "$name has received grade $grade."
    done < input.txt

   **input.txt**
    
    John 85
    Alice 92
    Bob 78
    Emily 65
    Michael 70
**or** ( instead of txt, you can pass data directly )

    done <<<"John 85
    Alice 92
    Bob 78
    Emily 65
    Michael 70"

### 14) Write a Shell program to find the smallest and largest numbers from a set of numbers.

    read -p "Enter numbers separated by spaces: " -a nums
    echo "Smallest number: $(printf "%s\n" "${nums[@]}" | sort -n | head -n 1)"
    echo "Largest number: $(printf "%s\n" "${nums[@]}" | sort -rn | head -n 1)"

### 15) Write a Shell program to find the smallest digit from a number.

    read -p "Enter a number: " num
    smallest=$(echo "$num" | grep -o '[0-9]' | sort -n | head -n 1)
    echo "Smallest digit in $num is $smallest"

### 16) Write a Shell program to find the sum of all numbers between 50 and 100, which are divisible by 3 and not divisible by 5.

    sum=$(seq 50 100 | awk '{if($1%3==0 && $1%5!=0) sum+=$1} END{print sum}')
    echo "Sum of numbers between 50 and 100 divisible by 3 and not by 5: $sum"

### 17) Write a Shell program to find the second highest number from a set of numbers.

    read -p "Enter numbers separated by spaces: " -a nums
    second_highest=$(printf '%s\n' "${nums[@]}" | sort -rn | awk 'NR==2{print $1}')
    echo "Second highest number: $second_highest"

### 18) Write a Shell program to find the sum of digits of a number using function.

     sum_digits() {
        echo $1 | grep -o '.' | paste -sd+ | bc
    }
    read -p "Enter a number: " num
    result=$(sum_digits $num)
    echo "Sum of digits of $num is $result"

### 19) Write a Shell program to print the reverse of a number using function.

    reverse_number() {
        echo $1 | grep -o . | tac | tr -d '\n'
    }
    read -p "Enter a number: " num
    result=$(reverse_number $num)
    echo "Reverse of $num is $result"

### 20) Write a Shell program to find the factorial of a number using for loop.

    read -p "Enter a number: "  num
    factorial=1
    for (( i=1; i<=num; i++ )); do
        factorial=$((factorial * i))
    done
    echo "Factorial of $num is $factorial"
**or** 

    read -p "Enter a number: " num
    factorial=$(seq -s "*" 1 $num | bc)
    echo "Factorial of $num is $factorial"


## Unix/Linux Commands
### File Commands
| Command | Description |
|---------|-------------|
| `ls` | List directory contents |
| `cd` | Change the current directory |
| `pwd` | Print the current working directory |
| `cp` | Copy files/directories |
| `mv` | Move/rename files/directories |
| `rm` | Remove files/directories |
| `mkdir` | Create a new directory |
| `rmdir` | Remove an empty directory |

### Process Management
| Command | Description |
|---------|-------------|
| `ps` | Display information about active processes |
| `top` | Display and update sorted information about CPU processes |
| `kill` | Terminate processes by PID or name |
| `killall` | Terminate processes by name |
| `pgrep` | List processes based on name |
| `pkill` | Signal processes based on name |

### File Permission
| Command | Description |
|---------|-------------|
| `chmod` | Change file permissions |
| `chown` | Change file ownership |
| `chgrp` | Change group ownership |

### Searching
| Command | Description |
|---------|-------------|
| `grep` | Search text patterns |
| `find` | Search for files/directories |
| `locate` | Search for files/directories in a database |
| `whereis` | Locate the binary, source, and manual page files for a command |

### System Info
| Command | Description |
|---------|-------------|
| `uname` | Print system information |
| `hostname` | Print the name of the current host system |
| `uptime` | Show how long the system has been running |
| `df` | Display disk space usage |
| `du` | Display directory space usage |

### Compression
| Command | Description |
|---------|-------------|
| `tar` | Archive files |
| `gzip` | Compress or decompress files |
| `zip` | Package and compress files |
| `unzip` | Extract compressed files |

### Network
| Command | Description |
|---------|-------------|
| `ifconfig` | Configure network interfaces |
| `ip` | Show/manipulate routing, devices, policy routing, and tunnels |
| `ping` | Send ICMP ECHO_REQUEST packets to network hosts |
| `traceroute` | Print the route packets take to network host |
| `netstat` | Display network connections, routing tables, interface statistics |
