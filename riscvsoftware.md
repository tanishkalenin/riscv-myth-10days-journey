## Step 1: Setting Up Ubuntu in VirtualBox (VMBox)

1. Install **Oracle VirtualBox**
![VirtualBox Setup](images/virtualbox.png)




2. Install **Ubuntu Linux**
![Ubuntu Installation](images/ubantuiso.png)




3.Launch **VirtualBox** and click on the **New** button to create a new virtual machine. Fill
up the details as shown in the image below
![Creating a new virtual machine](images/virtualmachin.png)




4. Start the Ubuntu virtual machine and open the **Terminal**.
![Terminal view](images/terminalscr.png)



---

## Step 2: Installing Leafpad Text Editor

Install the lightweight text editor **Leafpad**, which is used to write C programs:

```bash
$ sudo apt install leafpad
```
Navigate to the home directory:
```
$ cd
```
```
$ leafpad sum1ton.c &
```

![image](images/1stcprog.png)

## Step 3: Compile and Run the C Code
Compile the C code:

```

$ gcc sum1ton.c

```
Run the compiled program:
```
$ ./a.out
```
![image](images/1stoutput.png)


## Step 4: Compile C Code with RISC-V Compiler
Compile the C code using the RISC-V compiler:
```
$ riscv64-linux-gnu-gcc -O1 -march=rv64gc -o sum1ton.o sum1ton.c
```
List the compiled object file:

```
$ ls -ltr sum1ton.o
```
## Step 5: Display Assembly Code

Display the optimized assembly code for the main function:

```
$ riscv64-linux-gnu-objdump -d sum1ton.o
```

![image](images/outwrisv.png)

```
$ riscv64-linux-gnu-objdump -d sum1ton.o |less
```

![image](images/outwrisvless.png)

# signed and unsigned integers and spike and debug

compile the unsignedHighest.c program using RISC-V compiler
```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c
```

![image](images/9.png)

```
$ spike pk unsignedHighest.o

```

![image](images/10.png)

```
**2**
```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c

![image](images/11.png)

```
$ spike pk unsignedHighest.o

```

![image](images/12.png)

```
**3**
```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o unsignedHighest.o unsignedHighest.c


![image](images/13.png)

```
$ spike pk unsignedHighest.o
```

![image](images/14.png)

```

**signed**

$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o signedHighest.o signedHighest.c
```

![image](images/15.png)

```
$ spike pk signedHighest.o

```
![image](images/16.png)
