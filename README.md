# STM32
## STM32 Projects based on HAL functions


in main Function, inside the while loop


if(counter>0){
		  HAL_Delay(10);
	      HAL_UART_Transmit(&huart2, Rxdata, strlen(Rxdata),100);

//	      /*-----------------------------------------------------*/
	      int count_data,count_address;
	      HAL_FLASH_Unlock();

	      //FLASH_Erase_Sector(FLASH_SECTOR_11,VOLTAGE_RANGE_1);
	      HAL_FLASH_Program(((uint32_t)0x02U),0x0807FF00,*(uint32_t*)Rxdata);
	      HAL_FLASH_Program(((uint32_t)0x02U),0x0807FF10,*(uint32_t*)Rxdata);
	      HAL_FLASH_Lock();

//	      /*-----------------------------------------------------*/
	      counter=0;
	      memset(Rxdata,'\0',strlen(Rxdata));
	  }
    
    
    
    
    STM32L1xx_it.c is used for Interrupt Subroutine.
    
    it executes when UART data received
    In STM32L1xx_it.c
    
    unsigned char Rxdata[100],counter;
extern uint8_t Rx_data[100];


void USART2_IRQHandler(void)
{
  /* USER CODE BEGIN USART2_IRQn 0 */

  /* USER CODE END USART2_IRQn 0 */
  HAL_UART_IRQHandler(&huart2);
  /* USER CODE BEGIN USART2_IRQn 1 */
  HAL_UART_Receive_IT(&huart2, (uint8_t*)&Rx_data, 1);

  Rxdata[counter]=Rx_data[0];
  counter++;




  /* USER CODE END USART2_IRQn 1 */
}




