The previous article introduced the use of RandLA-Net to train the Semantic 3D dataset in the tensorflow 2.0 environment. Here we document how to train the S3DIS dataset with RandLA-Net in the tensorflow 2.0 environment. 

 Since the code provided by the author is based on tensorflow 1.11, some modifications are required to run the program in the 2.0 environment. The modification method has been given in the training Semantic3D dataset. 

#  Training the S3DIS dataset 

 1, download the dataset, the author used Stanford3dDataset_v1, the entire compressed package downloaded is 4.79G, after decompression there are 30 G. 

 2, data set preprocessing, data set download decompression, there is a certain error in the original data source, Area_5\ office_19\ Annotations\ ceiling_1 there is a line of data contains characters, resulting in data operation failure, see the detailed process of using NumPy to load txt file prompt ValueError: could not convert string to float. 

 Then execute the following statement 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 3. 60% off cross-training, first modify your data path, and then execute the following code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 4. Verify, copy all ply files in the test folder to the/data/S3DIS/results folder 

 ![avatar]( 8d692fc848b2425ebb154607e4a96967.png) 

 Run script 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573789636
  ```  
 ![avatar]( d0f980a9a34d4fe9921dfddc46335c53.png) 

 The final evaluation result is that I can see that the miou trained by myself is 68.4%, and the result of the author's training is 70.0%. The other types of scores are compared as follows:  

