# ALU-using-VHDL code and testbench
MODULE:-
module ALU(
	input [7:0] A,
	input [7:0] B,
	input [2:0] ALUop,
	output reg [7:0] Result,
	output reg CarryOut 
 );
	always @(*) begin 
		case (ALUop) 
			3'b000: {CarryOut, Result} = A + B; 
			3'b001: {CarryOut, Result} = A-B; 
			3'b010: Result = A & B; 
			3'b011: Result = A | B; 
			3'b100: Result = A^B; 
			3'b101: Result = ~A; 
			3'b110: Result = A << 1; 
			3'b111: Result = A >> 1; 
			default: Result = 8'b00000000; 
endcase 
	end 
endmodule



testcase:-
module ALUtest;
	// Inputs
	reg [7:0] A;
	reg [7:0] B;
	reg [2:0] ALUop;

	// Outputs
	wire [7:0] Result;
	wire CarryOut;

	// Instantiate the Unit Under Test (UUT)
	ALU uut (
		.A(A), 
		.B(B), 
		.ALUop(ALUop), 
		.Result(Result), 
		.CarryOut(CarryOut)
	);

	initial begin
		// Initialize Inputs
		A = 8'b00001101; B = 8'b00000011; ALUop = 3'b000; #10; // Addition 
		A = 8'b00001101; B = 8'b00000011; ALUop = 3'b001; #10; // Subtraction 
		A = 8'b00001101; B = 8'b00000011; ALUop = 3'b010; #10; // AND 
		A = 8'b00001101; B = 8'b00000011; ALUop = 3'b011; #10; // OR 
		A = 8'b00001101; ALUop = 3'b101; #10;  
		A = 8'b00001101; ALUop = 3'b110; #10;  
		A = 8'b00001101; ALUop = 3'b111; #10;
$finish;		


	end
      
endmodule


