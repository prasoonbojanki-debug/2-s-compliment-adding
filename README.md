# 2-s-compliment-adding
Assume that you have two 8-bit 2's complement numbers, a[7:0] and b[7:0]. These numbers are added to produce s[7:0]. Also compute whether a (signed) overflow has occurred.
module top_module (
    input [7:0] a,
    input [7:0] b,
    output [7:0] s,
    output overflow
); 
    wire [8:0]w;
    assign w[0]=1'b0;
    genvar i;
    generate
        for(i=0;i<=7;i=i+1) begin : h_ga
            assign s[i]=a[i]^b[i]^w[i];
            assign w[i+1]=(a[i]&b[i])|(w[i]&(a[i]^b[i]));
        end
    endgenerate
    assign overflow=w[7]^w[8];
endmodule
