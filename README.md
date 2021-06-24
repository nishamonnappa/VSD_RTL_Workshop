# VSD_RTL_Workshop
A 5-Day RTL workshop with VSD
A Glimpse of “sky_fd_sc_hd_tt_025C_1v80.lib” file
Below is a snippet of a sky130_fd_sc_hd_tt_025C_1v80.lib file used for the Lab activity in the session. It refers to all the standard cells to be used in the design and connects accordingly during synthesis and simulation. It contains all the slow and fast cells.


 ![image](https://user-images.githubusercontent.com/86371082/123274481-2ec17700-d521-11eb-8199-8be83844fcb0.png)
 
 ![image](https://user-images.githubusercontent.com/86371082/123274590-4862be80-d521-11eb-9b15-b9ee05645cbb.png)
 
 ![image](https://user-images.githubusercontent.com/86371082/123274611-4d277280-d521-11eb-8155-b7837bc23413.png)



Details: -  sky130_fd_sc_hd_tt_025C_1v80.lib
-	Sky130- It’s a 130nm library
-	tt- Typical
-	025C- Temperature
-	1v80-indicates the Temperature
	**Basically, the standard cell library is designed around all the minimum, typical and maximum corner of PVT corner for manufacturing the IC.
	
Other Details: - The library file contains below :-
1.	Delay_model :”Look Up” ;
2.	Some of the units of the time, voltage, power, current, and resistance are mentioned as below: 


![image](https://user-images.githubusercontent.com/86371082/123274758-6c260480-d521-11eb-98ca-0d535ca42c89.png)


 
3.	The standard cells are mentioned for different gates (AND, OR, INVERTER, etc) as below: -

![image](https://user-images.githubusercontent.com/86371082/123274796-7516d600-d521-11eb-980d-3bb269a03082.png)

 
4.	The feature such as the leakage power of different cells are mentioned, for example for the cell “sky130_df_sc_hd_a210i_4” and its corresponding Verilog model which gives the logical operation for the cell is shown as below :-

![image](https://user-images.githubusercontent.com/86371082/123274864-7f38d480-d521-11eb-9979-2bbf39722a81.png)

 
Note here:-
A.	 a210i stands for 2 input A1 and A2 undergoes AND operation, the output of this operation will undergoes OR operation with B1 and the output of this entire operation is inverted as below:-
 
![image](https://user-images.githubusercontent.com/86371082/123274951-9081e100-d521-11eb-859d-39c5f53bae10.png)
![image](https://user-images.githubusercontent.com/86371082/123275010-9bd50c80-d521-11eb-90ba-cab3d02bdc27.png)

 

B.	 If you could observe above cell “sky130_df_sc_hd_a210i_4” has 3 input and hence there could be 8 possible inputs, hence for all the 8 possible inputs the leakage power is mentioned as below:-

 ![image](https://user-images.githubusercontent.com/86371082/123275054-a4c5de00-d521-11eb-8b9a-8958f725dab0.png)
 ![image](https://user-images.githubusercontent.com/86371082/123275083-ac858280-d521-11eb-877b-764c5a96049a.png)

 
5.	Library contains all the specification such as power, delay, capacitance with respect to each pin, example for pin A1 is shown below :-
![image](https://user-images.githubusercontent.com/86371082/123275190-bd35f880-d521-11eb-9494-b400722eca62.png)

 
6.	Below is the comparison of the area of the standard cells a210_1, a210_1, and a210_4. We can note here that:

A.	sky130_fd_sc_hd__a21o_2

![image](https://user-images.githubusercontent.com/86371082/123275236-c6bf6080-d521-11eb-8488-a05abcaeadb5.png)

![image](https://user-images.githubusercontent.com/86371082/123275273-cde66e80-d521-11eb-9390-b8803435e900.png)


   


B.	sky130_fd_sc_hd__a21o_1

![image](https://user-images.githubusercontent.com/86371082/123275337-dc348a80-d521-11eb-8833-27a91371ac89.png)
![image](https://user-images.githubusercontent.com/86371082/123275351-df2f7b00-d521-11eb-8f76-e583f7cd2aa2.png)


 
         

C.	sky130_fd_sc_hd__a210_4

![image](https://user-images.githubusercontent.com/86371082/123275388-e8204c80-d521-11eb-9b8a-21f46b9665fe.png)


 
       
The above observation can be summarized in the table below:-


![image](https://user-images.githubusercontent.com/86371082/123275667-261d7080-d522-11eb-967f-ec476c131e48.png)
