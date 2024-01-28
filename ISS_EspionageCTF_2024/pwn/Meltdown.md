# Meltdown

In the first pwn challenge, we must meltdown a reactor by bypassing its safety mechanism

## Recon

For this challenge we are given a service to connect to running at meltdown.ctf.issessions.ca on port 6666.
Luckily, we are given the source code to the service. Lets see what the service is actually doing.

## Source code review

Opening the meltdown.c file gives us the following

    #include <stdio.h>
    #include <stdlib.h>
    int BUFFER_SIZE = 256;

    int main(){
      char flag[BUFFER_SIZE];
      FILE *flagfp = fopen("./flag.txt", "r");
      fgets(flag, BUFFER_SIZE, flagfp);
      
        printf("Welcome to the reactor's admin interface!\n");
        int done = 0;
        int fTemp = 70;
        char input[BUFFER_SIZE];
        
        while(done == 0){
            int choice;
            int cTemp;
            printf("What temperature would you like to set the reactor to? (Celsius)\n");
            fflush(stdout);
            
            if (fgets(input, BUFFER_SIZE, stdin) == NULL) {
                perror("Error reading input");
                continue;
            }
            if (sscanf(input, "%d", &cTemp) != 1) {
                printf("Invalid input. Please enter a number.\n\n");
                continue;
            }
            
            
            if(cTemp < 500){
                //whose idea was it to take celsius input and then convert to fahrenheit??????????
                fTemp = cTemp * 2 + 32;
                if(fTemp > 2000000000){
                    printf("temperature is %d degress F\n\n", fTemp);
                    printf("AAAAAAAAAAAAAAAAAAAAH TOO HOT!!!!!!\n");
                    puts(flag);
                    done = 1;
                }else{
                    printf("temperature is %d degress F\n\n", fTemp);
                }
                    
                }else{
                    printf("Woah! Too hot, could not change\n\n");
                }
        }
        
        return 0;
    }

