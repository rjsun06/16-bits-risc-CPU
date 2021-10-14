Name: Renjie Sun
SID: 918702982
1. ADDER15
This 15-b look-ahead adder builds on 3 5-b adders and 2 5-b remainderers.
the max propogation delay is p(5-b adder)+p(5-b remainderer).
2.ALU15
This ALU builds on a 15-b adder, 3 Logic handler for AND, OR, and XOR each, and a 15-b delay concerning shifter.
Output of each of the part are wire together to be selected.
3.FLAGS8
the falg register triggers on rising edge changing to the value selected by WM whether the original flags or NF.
4.IMM15
immediate gennerater is implemented directly in the main circuit in CPU15.
5.REGS15
8 15-bit registors.
ouput selected by SelA and SelB.
renewing values of registor selected by SelD to D on rising edge.
6.CPU15
() means "it just happens". without () means "CPU's action" 
LOAD: 
	1st rising edge: ("LOAD" instruction buffered) (RE=1)
	1st falling edge: address<-ALU (RE=0 to avoid keyboard read)
	2nd rising: (DATA<-data I want) (RE=1)
	2nd falling: feed REGS15 with DATA (RE=1)
	3nd rising: do nothing and output the previous address with RE=1 again(to trigger keyboard read.). 
	3nd falling: address<-next PC
	4th rising: next instruction buffered
WRITE:
	1st rising edge:( "WRITE" instruction buffered) (WE=0)
	1st falling edge: address<-ALU DATAOUT<-data to write(WE=1)
	2nd rising: do nothing (WE=1)
	2nd falling: address<-next PC
	3rd rising: next instruction buffered.
JUMP:
	1st rising: ("BRANCH" or "J" instruction buffered)
	1st falling: PC <- target address
	2nd rising: next instruction buffered
interrupt:
	1st rising: ("SWI" buffered or IQR*E=1)
	1st falling: address<-7fff
 	2nd rising: (DATA<- target address)
	2nd falling: PC<-target address
	3rd rising: next instruction buffered

