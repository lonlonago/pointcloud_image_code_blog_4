#  1. Pytorch version KPConv model github address 

 KPConv-PyTorch 

#  System environment 

 System: win10 torch: 1.7 cuda: 10.1 cudnn: 7.6.5 graphics card: 2080TI 

#  Third, bug modification 

 3.1, compile the sampling and nearest neighbor search module bug author to compile the method is, in the win10 system, compile cpp_neighbors and cpp_subsampling, respectively 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 and 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 I myself in the win10 system under the test found that the execution of build.bat will prompt no py command, if you also encounter the same problem, you can follow the following operation to compile, compile cpp_neighbors, under cmd into the cpp_warppers\ cpp_neighbors folder, execute the following statement 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 The method of compiling cpp_subsampling is the same as above. 

 3.2, read data using multithreading bug modify config file does not use multithreading, in line 62 of the train_S3DIS.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 3.3, the video memory is not enough, modify the batch size in the config file in line 153 of the train_S3DIS.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
 3.4、loss计算错误，提示Expected object of scalar type Long but got scalar type Int for argument #2 ‘target’ in call to _thnn_nll_loss2d_forward。 

 Error location on line 189 of utils\ trainer.py 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573757409
  ```  
