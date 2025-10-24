```text
 _  _  ____                 _                        _        _ _            
| || ||___ \ _    __ _  ___| |_      _ __   _____  _| |_     | (_)_ __   ___ 
| || |_ __) (_)  / _` |/ _ \ __|____| '_ \ / _ \ \/ / __|____| | | '_ \ / _ \
|__   _/ __/ _  | (_| |  __/ ||_____| | | |  __/>  <| ||_____| | | | | |  __/
   |_||_____(_)  \__, |\___|\__|    |_| |_|\___/_/\_\\__|    |_|_|_| |_|\___|
                 |___/                                                                              
```

### **Overview**

A utility function that reads a text file line by line.

---

### **Key Learnings**
- Using static variables to preserve data across function calls
- Managing heap memory

---

### **About**

👉 [**Project requirement**](https://github.com/Mecha-Coder/42-get-next-line/blob/main/demo/en.subject.pdf)

From the title is sounds simple. But is not!

```C++
read (int fd, void *buf, size_t size)
```

Above is the system call used for reading file. The 2nd argument `void *buf` is a memory buffer where the kernel copies the raw bytes it reads. If the buffer is small, multiple reads are needed to complete one line. If it’s large, it might read multiple lines at once — meaning we must store the extra data somewhere and remembers it in the next function call. The challenge here is we don’t know the line length, and still return one line per function call.

![figure1](https://github.com/Mecha-Coder/42-get-next-line/blob/main/demo/figure1.png)

Here is an example of a text file:

```text
Hello world
Nice day
Good night
```

Lets clarify what a **line** is. A line is a sequence of characters ending with the newline character `\n`. This file contains 3 lines: "Hello world\n", "Nice day\n", and "Good night\n"


So the get_next_line() function must:
- Read raw data from the file descriptor using read()
- Accumulate characters until a newline \n is found
- Return that line, and
- Store the remaining text for the next call — without using global variables

This is where static variables come in. A static variable retains its value between function calls but remains private to the function’s scope. This allows us to remember leftover data between reads

![figure2](https://github.com/Mecha-Coder/42-get-next-line/blob/main/demo/figure2.png)

---

### **Resource**
