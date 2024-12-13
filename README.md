**VSLI and RISC-V Workshop**,
conducted by [@Kunal Ghosh](https://www.bing.com/ck/a?!&&p=2de3e48401de7d6dd3f119d2c2e40a7f16af2d22630c475ff714bdbf4b5a172eJmltdHM9MTczNDA0ODAwMA&ptn=3&ver=2&hsh=4&fclid=1f22b90d-2986-6283-39ce-aabb2813638e&psq=kunal+ghosh+vlsi&u=a1aHR0cHM6Ly9pbi5saW5rZWRpbi5jb20vaW4va3VuYWwtZ2hvc2gtdmxzaXN5c3RlbWRlc2lnbi1jb20tMjgwODQ4MzY&ntb=1) (Co-founder, VSD Corp. Pvt. Ltd.) along with his interns Nahusha and Vignesh.

The first thing that was done during this workshop which we term as 'roadshow' was to install the vsdsquadron.vdi file along with the virtual box and VC_redist. After these were successfully installed, the ubuntu was launched in the virtualbox.
![image (1)](https://github.com/user-attachments/assets/0c3e71a8-ff6c-40bb-8d86-248685dd745d)
After the ubuntu was opened, we open the terminal and install gedit using the following code:
```
  sudo apt install gedit
```
The following will be shown:
![image (2)](https://github.com/user-attachments/assets/b53112da-9357-4be6-abec-1a3307ad2fc5)
Now we launch the gedit by typing "gedit" in the terminal. A blank page pops where we can code which is executed in the terminal and save it as a ".c" file. An example code to find the sum of numbers from 1 to a selected number is shown below.
```
#include<stdio.h>  
int main(){  
    int sum = 0, i, n;  
    printf("Enter the value of n = ");  
    scanf("%d",&n);  
    for(i = 1;i <= n;i++){  
       sum = sum + i;  
    }  
    printf("The Sum of numbers from 1 to %d is %d\n",n,sum);  
    return 0;  
}
```
This code was saved as 'Puspa_vlsi_code.c' and was executed by tying the following code in the terminal:
```
gcc Puspa_vlsi_code.c
```
However after this we need to write the following code to launch the 'Puspa_vlsi_code.c':
```
./a.out
```
![image (5)](https://github.com/user-attachments/assets/62fd1eca-a661-479a-b219-0883be0bc915)

After the following code was executed.
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o Puspa_vlsi_code.o Puspa_vlsi_code.c
```
Then the following code was typed in the terminal.
```
riscv64-unknown-elf-objdump -d Puspa_vsli_code.o
```
The following will be seen in the screen
![image (7)](https://github.com/user-attachments/assets/259bf9d2-1cac-4663-a360-b13d574d0cc0)
Now the directory is changed to openlane flow directory with the help of the following command.
```
cd Desktop/work/tools/openlane_working_dir/openlane
```
By the help of this command, openlane is opened as shown below:
![image (9)](https://github.com/user-attachments/assets/777d065d-f39a-4c0b-8c97-3407a3c79d67)
Now write the following command in the terminal.
```
package require openlane 0.9
```


