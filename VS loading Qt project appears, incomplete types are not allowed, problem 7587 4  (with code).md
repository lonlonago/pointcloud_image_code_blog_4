 Recently working on a project using Qt + Cmake + VS: Use Cmake to compile a Qt project and then develop it in VS. 

 The project structure is as follows: 

 ![avatar]( a8f2c7ebbbe44ae388593fc2ac49c286.png) 

  After compiling with Cmake, open the project, and the following problem occurs: 

 ![avatar]( f6e3c0e3da3f4adbabe0194b9c4a95f3.png) 

  The reason is simple. VS did not find the UI header file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309573725528
  ```  
 As can be seen in VS, there are four ui_mainwindow files with the same name: 

 ![avatar]( 01d38d090ad34ee8b12e5e64b04d7270.png) 

  But only one of them can be opened, and the other double-clicking to open will cause an error: 

 ![avatar]( 0799db0d5e6c4f1c9b19bd3bbd4710fb.png) 

 Remove the error file to solve the problem: 

 ![avatar]( 4b7a1b112d6e4e26a7661bec1ea4ccca.png) 

