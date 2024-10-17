# D-FLIP-FLOP

Design code:

module Dflipflop (
    input D,        
    input clk,  
    input rst,   
    output reg Q   
);

always @(posedge clk) begin
    if (rst)
        Q <= 1'b0;  
    else
        Q <= D;     
end
endmodule

Test bench :

module tb_D_flipflop;

    // Inputs to the flip-flop
    reg D;
    reg clk;
    reg rst;
    
    // Output of the flip-flop
    wire Q;
    
    // Instantiate the D flip-flop module
    D_flipflop uut (
        .D(D),
        .clk(clk),
        .rst(rst),
        .Q(Q)
    );
    initial begin
        clk = 0;
        forever #5 clk = ~clk;
    end
    initial begin
        D = 0;
        rst = 0;
        #10 
        rst = 1;  
        #10 
        rst = 0;   
        #10 
        D = 1;     
        #10
        D = 0;     
        #10 
        D = 1;     
        #10 
        rst = 1;  
        #10 
        rst = 0;  
        #10 
        D = 0;    
        #20 $stop;    
    end
    initial begin
        $monitor("At time %t: D = %b, rst = %b, Q = %b", $time, D, rst, Q);
    end
endmodule

