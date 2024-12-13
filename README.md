**VSLI and RISC-V Workshop**,
conducted by [Kunal Ghosh](https://www.bing.com/ck/a?!&&p=2de3e48401de7d6dd3f119d2c2e40a7f16af2d22630c475ff714bdbf4b5a172eJmltdHM9MTczNDA0ODAwMA&ptn=3&ver=2&hsh=4&fclid=1f22b90d-2986-6283-39ce-aabb2813638e&psq=kunal+ghosh+vlsi&u=a1aHR0cHM6Ly9pbi5saW5rZWRpbi5jb20vaW4va3VuYWwtZ2hvc2gtdmxzaXN5c3RlbWRlc2lnbi1jb20tMjgwODQ4MzY&ntb=1) (Co-founder, VSD Corp. Pvt. Ltd.) along with his interns Nahusha and Vignesh.

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
The following will be seen in the screen:

![image (7)](https://github.com/user-attachments/assets/259bf9d2-1cac-4663-a360-b13d574d0cc0)
Now the directory is changed to openlane flow directory with the help of the following command.
```
cd Desktop/work/tools/openlane_working_dir/openlane
```
We write the following command to open the Openlane
```
docker
```
To execute the Openlane we write the following command:
```
./flow.tcl -interactive
```
This command will execute and launch the Openlane as shown in the figure below:

![image (9)](https://github.com/user-attachments/assets/777d065d-f39a-4c0b-8c97-3407a3c79d67)

Now write the following command in the terminal.
```
package require openlane 0.9
```
We need to create the base for our chip. This chip has gates made of atlest four mosfests which is again made of silion which sits on the centre of the chip which is surroundes by the Pads. The language used here is **verlog**. To create the base of our pico sized 32 bit RV chip we use the following command.
```
prep -design picorv32a
```

![Screenshot 2024-12-13 121808](https://github.com/user-attachments/assets/7d224dc0-0637-4a64-b1f8-a716e49d132f)

Now once the base is created we synthesize the chip.
```
run_synthesis
```

![Screenshot 2024-12-13 122538](https://github.com/user-attachments/assets/a5184682-0525-4f3a-b6fe-f2acdaad8034)

The synthesis was sucessful.
Now further we will create the Floorplan of our chip that will give us the idea of where the gates will sit.
the following code is used to execute the Floorplan.
```
run_floorplan
```

![Screenshot 2024-12-13 123727](https://github.com/user-attachments/assets/ff2b2cb4-2e63-4710-ac7c-895b63ccfe39)

Once the Floorplan is created we can open a new tab and use the following code to see the Floorplan:
```
eog designs/picorv32a/runs/13-12_07-00/results/floorplan/picorva32a.floorplan.def.png
```

![Screenshot 2024-12-13 124027](https://github.com/user-attachments/assets/4fc7ff7b-5e2a-40fe-9d5e-34f0170dbbca)![Screenshot 2024-12-13 124049](https://github.com/user-attachments/assets/8a15bcf0-e9f4-44ae-82e9-9d9ffd8d6322)

Now we need to plaace our chips in their designated places. The following code is written in the preceding Tab to execute it.
```
run_placement
```
To view the Placements, we can open a new Tab and write the following command:
```
eog designs/picorv32a/runs/13-12_07-00/results/placement/picorva32a.placement.def.png
```

![Screenshot 2024-12-13 140655](https://github.com/user-attachments/assets/9d5b00a4-6f1c-486b-857f-ec9a6be2ac55)![Screenshot 2024-12-13 140957](https://github.com/user-attachments/assets/39243ca4-d7d3-499b-9885-80f826d3f0e7)

The following is the figure which shows the Placement of the Gates: 

![Screenshot 2024-12-13 141332](https://github.com/user-attachments/assets/1620eeb8-5b77-4106-9bda-ff95c8d790b2)

Now Clock Tree Synthesis is a technique for distributing the clock equally among all sequential parts of a VLSI design. The purpose of Clock Tree Synthesis is to reduce skew and delay. Clock Tree Synthesis is provided with the placement data as well as the clock tree limitations as input. For this we use the following code:
```
run_cts
```

![Screenshot 2024-12-13 142331](https://github.com/user-attachments/assets/1d5f8848-32ac-463f-8e32-38eb3bfe48cc)![Screenshot 2024-12-13 142229](https://github.com/user-attachments/assets/c0937df1-f0d9-41ef-af73-fe5f822c45f4)

The Skew and the delay is shown above in the figure.After this we need to undergo Routing. The routing mechanism establishes the specific pathways for interconnections. This contains the regular cell and macro pins, block boundary pins, and chip boundary pads. The tool includes information about the exact placements of blocks, pins of blocks, and I/O pads at chip borders after placement and CTS.
The following code is used:
```
run_routing
```

![Screenshot 2024-12-13 144215](https://github.com/user-attachments/assets/1652d16a-02be-492f-baa1-8112b030014c)

Hence our microprocessor chip is ready.
WE CAN RUN THE FOLLOWING EXAMPLE CODES IN THE VS CODE AFTER CONNECTING THE RISC-V BOARD.
1) To make the LED Blink:
```
#include <ch32v00x.h>
#include <debug.h>

#define BLINKY_GPIO_PORT GPIOD
#define BLINKY_GPIO_PIN GPIO_Pin_6
#define BLINKY_CLOCK_ENABLE RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE)

void NMI_Handler(void) __attribute__((interrupt("WCH-Interrupt-fast")));
void HardFault_Handler(void) __attribute__((interrupt("WCH-Interrupt-fast")));
void Delay_Init(void);
void Delay_Ms(uint32_t n);

int main(void)
{
	NVIC_PriorityGroupConfig(NVIC_PriorityGroup_1);
	SystemCoreClockUpdate();
	Delay_Init();

	GPIO_InitTypeDef GPIO_InitStructure = {0};

	BLINKY_CLOCK_ENABLE;
	GPIO_InitStructure.GPIO_Pin = BLINKY_GPIO_PIN;
	GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
	GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
	GPIO_Init(BLINKY_GPIO_PORT, &GPIO_InitStructure);

	uint8_t ledState = 0;
	while (1)
	{
		GPIO_WriteBit(BLINKY_GPIO_PORT, BLINKY_GPIO_PIN, ledState);
		ledState ^= 1; // invert for the next run
		Delay_Ms(100);
	}
}

void NMI_Handler(void) {}
void HardFault_Handler(void)
{
	while (1)
	{
	}
}

```
2) To make the LED dim and glow:
```
#include "debug.h"
#define TIME_PERIOD 1000
#define PRESC       0
#define PULSE       632
#define STEP_SIZE   10
volatile u16 val;
volatile u8 dir;
void TIM1_PWMOut_Init(void){
    GPIO_InitTypeDef GPIO_InitStructure={0};
    TIM_OCInitTypeDef TIM_OCInitStructure={0};
    TIM_TimeBaseInitTypeDef TIM_TimeBaseInitStructure={0};
    //RCC_APB2PeriphClockCmd( RCC_APB2Periph_GPIOC | RCC_APB2Periph_TIM1, ENABLE );
    RCC_APB2PeriphClockCmd( RCC_APB2Periph_GPIOD | RCC_APB2Periph_AFIO, ENABLE );
    RCC_APB1PeriphClockCmd( RCC_APB1Periph_TIM2, ENABLE );
    GPIO_PinRemapConfig(GPIO_FullRemap_TIM2, ENABLE);
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_AF_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init( GPIOD, &GPIO_InitStructure);
    TIM_TimeBaseInitStructure.TIM_Period = TIME_PERIOD;
    TIM_TimeBaseInitStructure.TIM_Prescaler = PRESC;
    TIM_TimeBaseInitStructure.TIM_ClockDivision = TIM_CKD_DIV1;
    TIM_TimeBaseInitStructure.TIM_CounterMode = TIM_CounterMode_Up;
    TIM_TimeBaseInit( TIM2, &TIM_TimeBaseInitStructure);
    TIM_OCInitStructure.TIM_OCMode = TIM_OCMode_PWM2;
    TIM_OCInitStructure.TIM_OutputState = TIM_OutputState_Enable;
    TIM_OCInitStructure.TIM_Pulse = PULSE;
    TIM_OCInitStructure.TIM_OCPolarity = TIM_OCPolarity_High;
    TIM_OC3Init( TIM2, &TIM_OCInitStructure );
    TIM_CtrlPWMOutputs(TIM2, ENABLE );
    //TIM_OC3PreloadConfig( TIM1, TIM_OCPreload_Disable );
    //TIM_ARRPreloadConfig( TIM1, ENABLE );
    TIM_Cmd( TIM2, ENABLE );
}
int main(void)
{
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_1);
    SystemCoreClockUpdate();
    Delay_Init();
    TIM1_PWMOut_Init();
    val = 0;
    dir = 0;
    // Loop
    while(1){
        val += (dir) ? -STEP_SIZE : STEP_SIZE;
        TIM_SetCompare3(TIM2, val);
        dir ^= (val == 1000 || val == 0) ? 1 : 0;
        Delay_Ms(15);
    }
}
```
