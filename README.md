Download Link: https://assignmentchef.com/product/solved-eec180-lab2-combinational-logic-design-using-verilog
<br>
<strong>LAB 2: Combinational Logic Design Using Verilog </strong>

<strong>Objective:</strong> The purpose of this lab is to use Verilog to design combinational arithmetic circuits.  You will also learn how to write self-checking testbenches.

<h1>I.          Ripple-carry Adder</h1>




A <em>full adder</em> (FA) has inputs a, b and c<sub>i</sub> (carry in) and produces outputs s (sum) and c<sub>0</sub> (carry out).  c<sub>0</sub> = a.b + a. c<sub>i</sub> + b.c<sub>i </sub>s= a Å  b  Å c<sub>i</sub>

<strong> </strong>

An n-bit ripple-carry adder can be designed by connecting full-adders in a chain with the carry in for a given stage being the carry out of the previous stage and the carry in of the least significant bit being a 0.

<strong> </strong>

Perform the following steps:

<ol>

 <li>Write a <strong>behavioral</strong> model for a full adder in Verilog. (Hint: an assign statement can describe each output equation.)</li>

 <li>Instantiate your full adder subcircuit in order to build an <em>8-bit ripple-carry adder.</em> Add logic to produce an <em>Overflow</em> output, which should be set to 1 whenever the sum produced by the adder does not provide the correct signed (twos complement) value.</li>

 <li>Write a testbench to simulate your design for all possible input combinations. Note that for an 8-bit adder there are 2<sup>16</sup> (256 x 256) possible inputs. See Appendix at the end of this document for an example of how to construct a testbench using a <strong>for loop</strong> in Verilog.</li>

</ol>




<h1>II.     Multiplication</h1>




Figure 2 shows the traditional procedure for performing the multiplication P=A x B, where A and B are 4-bit unsigned binary numbers. Since each bit in B is either 1 or 0, the summands are either shifted versions of A or 0000. The Boolean AND operation can be used to multiply any two binary bits. Figure 3 shows an array multiplier circuit that implements P = A x B, where A and B are 4-bit unsigned binary numbers.




<strong> </strong>

Figure 2. Multiplication of Unsigned Binary Numbers







Figure 3. Array Multiplier Circuit Block Diagram







Perform the following steps:




<ol>

 <li>Write a <strong>structural</strong> model in Verilog that describes an 4×4 unsigned array multiplier that can be implemented on the Altera DE10-Lite board. Use switches SW<sub>7-4</sub> to represent the number A and switches SW<sub>3-0</sub> to represent the number B. Display the hex value of A on HEX3 and the hex value of B on HEX2. Display the result P = A x B on HEX1-0.</li>

</ol>




<ol start="2">

 <li>Compile your design in Quartus. Download your design to the Altera DE10-Lite board and test your circuit. <strong><u>Demonstrate your circuit to your TA</u>.</strong></li>

</ol>







<ol start="3">

 <li>Estimate the performance of your circuit in terms of the critical path using the timing analysis tool. The following is a step by step procedure to obtain the propagation delay between the input and output ports of your design:</li>

</ol>




<h1>Step 1. Timing netlist</h1>

<em>In this section, we will create a timing netlist, specify the delay model and operating conditions for the multiplier design.  </em>




<ul>

 <li>Go to Netlist section on top and click on <strong>Create Timing Netlist. </strong>The corresponding Timing Netlist window will pop-up.</li>

</ul>




<ul>

 <li>Select Fast-corner delay model and click OK.</li>

</ul>




<ul>

 <li>Next, go to Netlist -&gt; Set Operating Conditions, select MIN-Fast1200mV-0c operating condition and click OK.</li>

</ul>




<h1>Step 2. Constraints</h1>

<em>In this section, we will set the maximum propagation delay constraints for the design.  </em>




<ul>

 <li>Go to Constraints -&gt; Set Maximum Delay and Set Maximum Delay window will pop-up.</li>

 <li>Click the name finder icon and that will open up the Name Finder window.</li>

</ul>




<ul>

 <li>Select <em>get_ports</em> in collection and click <em>List</em> to list out all I/O ports.</li>

</ul>




<ul>

 <li>First, select all input ports, SW0, SW1..SW7 and transfer them to the second column using ‘&gt;’, which locks all the selected ports. Next, click ok to complete the <em>From</em> section in <em>Set Maximum Delay</em></li>

</ul>




<ul>

 <li>Similarly, select all output ports HEX0[0:6] .. HEX3[0:6] and complete the <em>To</em> section in <em>Set Maximum Delay</em></li>

</ul>




<ul>

 <li>Next, set a <strong><em>Delay value of (say 30ns)</em></strong> and click</li>

</ul>

<em> </em>

<ul>

 <li>Finally, click on<em> Update Timing Netlist </em>in Tasks section to consider the timing constraint and re-generate timing reports. <em> </em></li>

</ul>

<em> </em>

<h1>Step 3. Reports</h1>

<em>In this section, we will generate and examine the timing reports.  </em>

<em>  </em>

<ul>

 <li>Go to<em> Tasks -&gt; Reports -&gt; Custom reports -&gt; Report Path </em></li>

</ul>

<em> </em>

<ul>

 <li>In Report Path window, fill up the I/O ports in <em>From </em>and<em> To </em>section like the previous section.</li>

</ul>




<ul>

 <li>Set Report number of paths as 50 and click on <em>Report Path</em>.</li>

</ul>




<ul>

 <li>Next, you can see the delay across each path and the critical path delay of the design being the top one in the list (e.g. 6.211ns for an example design as shown below with critical path being SW2 -&gt; HEX3[3])</li>

</ul>







<ul>

 <li>Next, go to Tasks -&gt; Reports -&gt; Slack -&gt; Report Set up Summary to see a <strong>Positive Slack</strong>, which indicates the design has met the timing constraint (Propagation delay) of 30ns.</li>

</ul>




<ul>

 <li>Finally, we can do an experiment to find whether the design considered for an example can meet a <strong>propagation delay timing constraint of 5ns</strong>. To do so, we can proceed with the steps listed earlier. However, to do things faster we can run some of the <strong>tcl</strong> commands on console as shown below.</li>

</ul>




<ul>

 <li><em>set_max_delay -from [get_ports {SW0 SW1 SW2 SW3 SW4 SW5 SW6 SW7}] -to </em></li>

</ul>

<em>[get_ports {HEX0[0] HEX0[1] HEX0[2] HEX0[3] HEX0[4] HEX0[5] HEX0[6] </em>

<em>HEX1[0] HEX1[1] HEX1[2] HEX1[3] HEX1[4] HEX1[5] HEX1[6] HEX2[0] </em>

<em>HEX2[1] HEX2[2] HEX2[3] HEX2[4] HEX2[5] HEX2[6] HEX3[0] HEX3[1] HEX3[2] HEX3[3] HEX3[4] HEX3[5] HEX3[6]}] 5 </em>

<em> </em>

<ul>

 <li><em>update_timing_netlist </em></li>

</ul>

<em> </em>

<ul>

 <li><em>create_timing_summary -setup -panel_name “Summary (Setup)” -multi_corner </em></li>

</ul>

<em> </em>

<ul>

 <li><em>report_path -from [get_ports {SW0 SW1 SW2 SW3 SW4 SW5 SW6 SW7}] -to </em></li>

</ul>

<em>[get_ports {HEX0[0] HEX0[1] HEX0[2] HEX0[3] HEX0[4] HEX0[5] HEX0[6] </em>

<em>HEX1[0] HEX1[1] HEX1[2] HEX1[3] HEX1[4] HEX1[5] HEX1[6] HEX2[0] HEX2[1] HEX2[2] HEX2[3] HEX2[4] HEX2[5] HEX2[6] HEX3[0] HEX3[1] </em>

<em>HEX3[2] HEX3[3] HEX3[4] HEX3[5] HEX3[6]}] -npaths 50 -panel_name </em>

<em>{Report Path} -multi_corner </em>

<em> </em>

<ul>

 <li>Running those commands generates the Path Reports and directly show the propagation delay of 6.211ns on the console with a message <strong><em>Timing requirement not met</em></strong> as shown below.</li>

</ul>




<ul>

 <li>The Set up summary notifies <strong>a negative slack of -1.22ns</strong> as shown below, which means that the design has not met the timing constraint</li>

</ul>

(Propagation delay of 5ns) and slack of -1.22ns is basically the difference of constrained propagation delay and actual propagation delay in the design.













<strong>Report the critical path and propagation delay for the 4×4 multiplier.  </strong>

<ol start="4">

 <li>Design and write a Verilog model for 8×8 unsigned array multiplier.</li>

 <li>Perform a functional simulation of your 8×8 array multiplier design and print the simulation results.</li>

</ol>

<h1>III.  Lab Report</h1>




For your lab report, include the following:

<ul>

 <li>Lab Cover Sheet with signed TA verification for successful simulations and implementation in the Altera board.</li>

 <li>Design and implementation of the overflow circuit in part I of the lab.</li>

 <li>Complete Verilog test bench for each part. The testbench should test your design exhaustively, i.e., for all possible input combinations and should be self-checking as shown in the appendix.</li>

</ul>


