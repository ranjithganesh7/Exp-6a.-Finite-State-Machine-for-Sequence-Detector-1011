# Exp-6a.-Finite-State-Machine-for-Sequence-Detector-1011
# Aim 
To design and simulate a Finite-State-Machine-for-Sequence-Detector-1011 using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment. 

# Apparatus Required 

Vivado 2023.1 

# Procedure

Launch Vivado 2023.1 Open Vivado and create a new project.
Design the Verilog Code Write the Verilog code for the RAM,ROM,FIFO
Create the Testbench Write a testbench to simulate the memory behavior. The testbench should apply various and monitor the corresponding output.
Create the Verilog Files Create both the design module and the testbench in the Vivado project.
Run Simulation Run the behavioral simulation to verify the output.
Observe the Waveforms Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
Save and Document Results Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.
# Code
# Mealy 1011
// Verilog code
```
module mealy_fsm_1011(
            input clk,rst,xin,
            output reg zout
        );
        parameter [2:0] s1 = 3'b000,
                        s2 = 3'b001,
                        s3 = 3'b010,
                        s4 = 3'b011;
       reg [2:0] ps,ns;
 always@(posedge clk)
   begin
      if(rst)
          ps <= s1;
      else
          ps <= ns;
   end      
 always@(xin or ps)
     begin 
         case(ps)
           s1 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end 
           s2 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end             
           s3 : if(xin) begin
                     ns = s4;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end              
           s4 : if(xin) begin
                     ns = s1;
                     zout = 1;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end              
       endcase
    end
endmodule
```
// Test bench
```
module mealy_fsm_1011_tb;
        reg clk_t,rst_t,xin_t;
        wire zout_t;
        
        mealy_fsm_1011 dut(.clk(clk_t),.rst(rst_t),.xin(xin_t),.zout(zout_t));
           
     initial
        begin
            clk_t = 1'b1;
            rst_t = 1'b1;
          #100
            rst_t = 1'b0;
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1; 
          #100
           xin_t = 1'b1;              
      end
       always #50  clk_t = ~clk_t;                 
endmodule
```
// output Waveform
<img width="1919" height="1199" alt="Screenshot 2025-10-12 145410" src="https://github.com/user-attachments/assets/69a72780-32fb-4023-be27-cb9134aef627" />


# Moore 1011
```
module moore_fsm_1011(
            input clk,rst,xin,
            output reg zout
        );
        parameter [2:0] s1 = 3'b000,
                        s2 = 3'b001,
                        s3 = 3'b010,
                        s4 = 3'b011,
                        s5 = 3'b100; 
       reg [2:0] ps,ns;
 always@(posedge clk)
   begin
      if(rst)
          ps <= s1;
      else
          ps <= ns;
   end      
 always@(xin or ps)
     begin 
         case(ps)
           s1 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end 
           s2 : if(xin) begin
                     ns = s2;
                     zout = 0;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end             
           s3 : if(xin) begin
                     ns = s4;
                     zout = 0;
                 end             
                else  begin
                     ns = s1;
                     zout = 0;
                 end              
           s4 : if(xin) begin
                     ns = s5;
                     zout = 0;
                 end             
                else  begin
                     ns = s3;
                     zout = 0;
                 end              
           s5 : if(xin) begin
                     ns = s2;
                     zout = 1'b1;
                 end             
                else  begin
                     ns = s1;
                     zout = 1'b1;
                 end 
       endcase
    end
endmodule
``` 
// write verilog code for ROM using $random
```
module moore_fsm_1011_tb;
        reg clk_t,rst_t,xin_t;
        wire zout_t;
        
        moore_fsm_1011 dut(.clk(clk_t),.rst(rst_t),.xin(xin_t),.zout(zout_t));
           
     initial
        begin
            clk_t = 1'b1;
            rst_t = 1'b1;
          #100
            rst_t = 1'b0;
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b1;
          #100
            xin_t = 1'b0;
          #100
            xin_t = 1'b1; 
          #100
           xin_t = 1'b1;              
      end
       always #50  clk_t = ~clk_t;                 
endmodule
```
// Test bench
```
module moore_2_tb;
reg clk,rst,in;
wire out;
moore_2 uut(clk,rst,in,out);
initial
begin
    clk=0;
    forever #5clk=~clk;
end
initial
begin
rst=1;
in=0;
#10 rst=0;
#10 in=1;
#10 in=0;
#10 in=1;
#10 in=1;
#10 $finish;
end
endmodule
```
// output Waveform

<img width="1918" height="1199" alt="Screenshot 2025-10-10 161858" src="https://github.com/user-attachments/assets/240a0415-ebb2-4c9a-bca2-4145254505c7" />


Conclusion
The Mealy and Moore state machine for sequence 1011 was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the sequence operations and observing the output waveforms.
