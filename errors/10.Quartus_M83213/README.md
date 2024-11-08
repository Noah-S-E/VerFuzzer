

## The increment operation (++) will cause an error.

```
module test1 (
    input wire clk,          
    input wire reset,        
    output reg [7:0] y       
);

    reg [7:0] data [0:3];    
    integer i;               

    always @(posedge clk or posedge reset) begin
        if (reset) begin
            for (i = 0; i <= 3; i = i+1) begin
                data[i] <= 8'h00; 
            end
            y <= 8'h00;
        end else begin
            for (i = 0; i <= 3; i = i++) begin  
                data[i] <= i * 8'h11;
            end
            y <= data[0] + data[1]; 
        end
    end
endmodule

```
