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

![image](https://github.com/user-attachments/assets/1f6443e6-c0cb-43b0-8a76-5777b7b6f82c)


# Binary Neural Network in C
![image](https://github.com/user-attachments/assets/06fec611-7f1c-49eb-ac26-f5c0976c7e89)


```c
int main(int argc, char* argv[])
{
    srand(0); // Use a fixed random seed for debugging.

    // Initialize layers.
    Layer* linput = Layer_create(NULL, 2);
    Layer* lhidden = Layer_create(linput, 3);
    Layer* loutput = Layer_create(lhidden, 1);
    Layer_dump(linput, stderr);
    Layer_dump(lhidden, stderr);
    Layer_dump(loutput, stderr);

    // Run the network.
    double rate = 1.0;
    int nepochs = 10000;
    for (int i = 0; i < nepochs; i++) {
        double x[2];
        double y[1];
        double t[1];
        x[0] = rnd();
        x[1] = rnd();
        t[0] = f(x[0], x[1]);
        Layer_setInputs(linput, x);
        Layer_getOutputs(loutput, y);
        Layer_learnOutputs(loutput, t);
        double etotal = Layer_getErrorTotal(loutput);
        fprintf(stderr, "i=%d, x=[%.4f, %.4f], y=[%.4f], t=[%.4f], etotal=%.4f\n",
                i, x[0], x[1], y[0], t[0], etotal);
        Layer_update(loutput, rate);
    }

    // Dump the finished network.
    Layer_dump(linput, stdout);
    Layer_dump(lhidden, stdout);
    Layer_dump(loutput, stdout);

    // Free the memory.
    Layer_destroy(linput);
    Layer_destroy(lhidden);
    Layer_destroy(loutput);
    return 0;
}
```
![image](https://github.com/user-attachments/assets/4b4ac4ad-6e43-48a9-a1a1-1d0c1e68ae05)
![image](https://github.com/user-attachments/assets/faf45b2b-988e-4c3e-bccc-5a6b9d80b909)
![image](https://github.com/user-attachments/assets/ac528eb5-21c4-4e68-bc16-4320206bf7c9)
