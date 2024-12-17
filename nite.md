Contributions made but not solved it fully myself (did later) (no points, won't happen again)

# Challenge U ARe The detective
## nite{n0n_std_b4ud_r4t3s_ftw}

UART protocol, but with a nonstandard baud rate. First step, figuring out baud rate with the help of pulseview. 
Zoomed in on the signal and looked for the smallest bit. Baud rate = 1/(time of the smallest bit) 

![UART1]{Uart1.png}

The baud rate was `5405405`. Used that in the `add protocol detector` with `UART` and got the hex data. Converting that gives us the flag. 

![UART2]{Uart2.png}
