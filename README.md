# cmos-vlsi
module opamp(input positive_input, negative_input, output reg output);

  parameter GAIN = 100; // Open-loop gain
  parameter VDD = 5; // Supply voltage
  parameter VSS = 0; // Ground voltage
  parameter VTH = 0.5; // Threshold voltage

 reg opamp_output;

  always @ (positive_input, negative_input)
  begin
 
    if (positive_input > negative_input)
      opamp_output = (positive_input - negative_input) * GAIN;
    else
      opamp_output = (negative_input - positive_input) * GAIN;
      
    // Output clamping
    if (opamp_output > VDD)
      output = VDD;
    else if (opamp_output < VSS)
      output = VSS;
    else
      output = opamp_output;
  end

endmodule
